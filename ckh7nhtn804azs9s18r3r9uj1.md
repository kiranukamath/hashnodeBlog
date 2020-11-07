## Make code Simple with DataBlock api part2

<span class="w"></span>

# Make code Simple with DataBlock api part2


July 11, 2020

# **Blog15**

This is part two of my series Make code Simple with DataBlock API. If you have not read part one, see [here](https://kirankamath.netlify.app/blog/fastais-datablock-api/). In it, we have seen what DataBlock as a whole means, what are the bricks that are put together to make datablock. In last blog, I had stopped showing code so, in this blog, we’ll be diving into code.

Welcome!!!

Let us dive directly into code


```
!pip install -q fastai2</span>
```


Depending on type of problem, blocks in datablock changes and rest are same. Lets see example first,


```
from fastai2.vision.all import *</span>
```


# Example 1


```
camvid = DataBlock(blocks=(ImageBlock, MaskBlock(codes = np.loadtxt(path/'codes.txt', dtype=str))),
    get_items=get_image_files,
    splitter=RandomSplitter(),
    get_y=lambda o: path/'labels'/f'{o.stem}_P{o.suffix}',
    item_tfms = Resize(224),
    batch_tfms=aug_transforms())</span><span id="81ff" class="de he hf ef hg b db if ig ih ii ij hi w hj">dls = camvid.dataloaders(path/"images") dls.show_batch()</span>
```


![Image for post](https://miro.medium.com/max/60/0*NvLdPIn3mGM4neky.png?q=20)

<noscript><img alt="Image for post" class="du io dv ip t" src="https://miro.medium.com/max/1024/0*NvLdPIn3mGM4neky.png" width="512" height="503" srcSet="https://miro.medium.com/max/552/0*NvLdPIn3mGM4neky.png 276w, https://miro.medium.com/max/1024/0*NvLdPIn3mGM4neky.png 512w" sizes="512px"/></noscript>

what did d<span id="rmm">o</span> different from above example which is different from part1 blog, just the `MaskBlock` in blocks, so thats how simple creating datablock is.

Depending on tasks blocks = () change. Block’s are used to help nest transforms inside of pre-defined problem domain.

So there are different types of blocks.

*   ImageBlock is used if the dataset is of images
*   CategoryBlock is for single-label categorical targets
*   MultiCategoryBlock is for multi-label categorical targets
*   RegressionBlock is for float targets
*   MaskBlock for segmentation masks, potentially with codes
*   PointBlock is for points in an image
*   BBoxBlock is for bounding boxes in an image
*   BBoxLblBlock is for labeled bounding boxes, potentially with vocab

So depending on type of domain these blocks can be used.

So coming to our example The MaskBlock is generated with the codes that give the correspondence between pixel value of the masks and the object they correspond to.

# Example 2

Now lets take multi label classification problem


```
df = pd.read_csv(path2/'train.csv') df.head()</span>
```


![Image for post](https://miro.medium.com/max/60/0*7tN9wkglp13rhIJT.png?q=20)

<noscript><img alt="Image for post" class="du io dv ip t" src="https://miro.medium.com/max/742/0*7tN9wkglp13rhIJT.png" width="371" height="206" srcSet="https://miro.medium.com/max/552/0*7tN9wkglp13rhIJT.png 276w, https://miro.medium.com/max/742/0*7tN9wkglp13rhIJT.png 371w" sizes="371px"/></noscript>


```
pascal = DataBlock(blocks=(ImageBlock, MultiCategoryBlock),
                   splitter=ColSplitter('is_valid'),
                   get_x=ColReader('fname', pref=str(path2/'train') + os.path.sep),
                   get_y=ColReader('labels', label_delim=' '),
                   item_tfms = [FlipItem(p=0.5),Resize(224,method='pad')],
                   batch_tfms=[*aug_transforms(do_flip=True, flip_vert=True, max_rotate=180.0, max_lighting=0.6,max_warp=0.1, p_affine=0.75, p_lighting=0.75,xtra_tfms=[RandomErasing(p=1.0,sh=0.1, min_aspect=0.2,max_count=2)]),Normalize])</span><span id="de26" class="de he hf ef hg b db if ig ih ii ij hi w hj">dls2 = pascal.dataloaders(df)</span><span id="1bf1" class="de he hf ef hg b db if ig ih ii ij hi w hj">dls2.show_batch()</span>
```


![Image for post](https://miro.medium.com/max/60/0*KzNMG_pdM4ynDQDO.png?q=20)

<noscript><img alt="Image for post" class="du io dv ip t" src="https://miro.medium.com/max/1024/0*KzNMG_pdM4ynDQDO.png" width="512" height="519" srcSet="https://miro.medium.com/max/552/0*KzNMG_pdM4ynDQDO.png 276w, https://miro.medium.com/max/1024/0*KzNMG_pdM4ynDQDO.png 512w" sizes="512px"/></noscript>

Basic principles remain same, depending on domain blocks are used.

Now if we see splitters in example 1 we used RandomSplitter because we did not had any rule how to split the data, but that is not the case in example 2, we have column called is_valid in df so depending on that we need to split, so used ColSplitter(‘is_valid’)

so I assume, you understood how splitter works???

**Think of example where you had column of folds and depending on that you need to split for k fold cross validation, then how would you split the dataset**???

This is shown with code in my [Kaggle kernel](https://www.kaggle.com/kirankamat/fastai-multilabel-classification-using-kfold-cv)

get_x and get_y are easy and in my above kernel it is also explained,

Now I’ll move to item_tfms and batch_tfms

Observe item_tfms and batch_tfms in example2

I should not have applied those many like flip_vert because in this case it makes no sense but it is applied to show you there are lot of transforms and we can use it.

even if you dont write fastai default applied few transforms and that is beauty of fastai


```
item_tfms = [FlipItem(p=0.5),Resize(224,method='pad')]</span>
```


what does this mean, as we have seen in blog [part1](https://kirankamath.netlify.app/blog/fastais-datablock-api/) that item transforms are applied on cpu, so speed is normal so we dont apply lot of transforms here, only the basic transforms are used. flip with probability of 0.5 is applied, then resizing is applied where images are converted to 224x224 and that is done with method of padding.


```
batch_tfms=[*aug_transforms(do_flip=True, flip_vert=True, max_rotate=180.0, max_lighting=0.6,max_warp=0.1, p_affine=0.75, p_lighting=0.75,xtra_tfms=[RandomErasing(p=1.0,sh=0.1, min_aspect=0.2,max_count=2)]),Normalize])</span>
```


batch transforms are applied on GPU so this is faster. I have used many here, just to show how it works.

In example2 show_batch you see lot of erased boxes that is because of RandomErasing, you can vary propability and this increase accuracy, there is callback cutmix which uses similar but complicated techniques.

Normalize is used without imagenet stats, now normalize is done based on mean and sd of that batch.

`aug_transforms` is utility function to easily create a list of flip, rotate, zoom, warp, lighting transforms.

Random flip with p=0.5 is added when do_flip=True. With p_affine we apply a random rotation of max_rotate degrees, a random zoom between min_zoom and max_zoom and a perspective warping of max_warp. With p_lighting we apply a change in brightness and contrast of max_lighting. Custom xtra_tfms can be added.

So this is it:)

I assume you have understood introductory knowledge about datablock.

It is actually easy but needs practise and getting used to it, you can create dataloaders using datablock api very quickly.

You can practice in google colab [here](https://github.com/kirankamatmgm/Fastai-Data-Block-API/blob/master/Datablock.ipynb)

Credit: fastai

Thank you for giving your time:)

<span class="jw ff bk jx jy jz"></span><span class="jw ff bk jx jy jz"></span><span class="jw ff bk jx jy"></span>

_Originally published at_ [_https://kirankamath.netlify.app_](https://kirankamath.netlify.app/blog/make-code-simple-with-datablock-api-part2/)_._