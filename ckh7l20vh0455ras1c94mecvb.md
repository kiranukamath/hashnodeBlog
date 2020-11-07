## Matrix Calculus for DeepLearning (Part2)

<span class="s"></span>

# Matrix Calculus for DeepLearning (Part2)


May 29, 2020

![Image for post](https://miro.medium.com/max/60/0*XvvGnvw_VlQB_Lrf.jpg?q=20)

<noscript><img alt="Image for post" class="t u v hm aj" src="https://miro.medium.com/max/2560/0*XvvGnvw_VlQB_Lrf.jpg" width="1280" height="849" srcSet="https://miro.medium.com/max/552/0*XvvGnvw_VlQB_Lrf.jpg 276w, https://miro.medium.com/max/1104/0*XvvGnvw_VlQB_Lrf.jpg 552w, https://miro.medium.com/max/1280/0*XvvGnvw_VlQB_Lrf.jpg 640w, https://miro.medium.com/max/1400/0*XvvGnvw_VlQB_Lrf.jpg 700w" sizes="700px"/></noscript>

We can’t compute partial derivatives of very complicated functions using just the basic matrix calculus rules we’ve seen [Blog part 1](https://kirankamath.netlify.app/blog/matrix-calculus-for-deeplearning-part1/). For example, we can’t take the derivative of nested expressions like sum( **w** + **x**) directly without reducing it to its scalar equivalent. We need to be able to combine our basic vector rules using the vector chain rule.

In paper they have defined and named three different chain rules.

1.  single-variable chain rule
2.  single-variable total-derivative chain rule
3.  vector chain rule

The chain rule comes into play when we need the derivative of an expression composed of nested subexpressions. Chain rule helps in solving problem by breaking complicated expressions into subexpression whose derivatives are easy to compute.

# Single-variable chain rule

Chain rules are defined in terms of nested functions such as _y=f(g(x))_ for single variable chain rule.

Formula is

dy/dx = (dy/du) (du/dx)

There are 4 steps to solve using single variable chain rule

1.  Introduce intermediate variable
2.  compute derivatives of intermediate variables wrt(with respect to) their parameters.
3.  combine all derivatives by multiplying them together
4.  substitute intermediate variables back in derivative equation.

Lets see example of nested equation y = f (x) = _ln_(sin(x³ ) ² )

![Image for post](https://miro.medium.com/max/60/0*fwTfTOlu4Qp5RcZE.png?q=20)

<noscript><img alt="Image for post" class="t u v hm aj" src="https://miro.medium.com/max/1282/0*fwTfTOlu4Qp5RcZE.png" width="641" height="440" srcSet="https://miro.medium.com/max/552/0*fwTfTOlu4Qp5RcZE.png 276w, https://miro.medium.com/max/1104/0*fwTfTOlu4Qp5RcZE.png 552w, https://miro.medium.com/max/1280/0*fwTfTOlu4Qp5RcZE.png 640w, https://miro.medium.com/max/1282/0*fwTfTOlu4Qp5RcZE.png 641w" sizes="641px"/></noscript>

It is to compute the derivatives of the intermediate variables in isolation!

But single variable chain rule is applicable only when a single variable can influence output in only one way. As we see in example we can handle nested expression of single variable _x_ using this chain ruleonly when x can effect y through single data flow path.

# Single-variable total-derivative chain rule

If we apply single variable chain rule to **y = f (x) = x + x²** we get wrong answer, because derivative operator doesnot apply to multivariate functions. change in x in the equation , affects y both as operand og addition and as operand of square. so we clearly cant apply single variable chain rule. so…

we move to total derivatives.

which is to compute (dy/dx) , we need to sum up all possible contributions from changes in x to the change in y.

Formula for total derivative chain rule

![Image for post](https://miro.medium.com/max/60/0*80kLCjqmNvBTdQdt.png?q=20)

<noscript><img alt="Image for post" class="t u v hm aj" src="https://miro.medium.com/max/1298/0*80kLCjqmNvBTdQdt.png" width="649" height="66" srcSet="https://miro.medium.com/max/552/0*80kLCjqmNvBTdQdt.png 276w, https://miro.medium.com/max/1104/0*80kLCjqmNvBTdQdt.png 552w, https://miro.medium.com/max/1280/0*80kLCjqmNvBTdQdt.png 640w, https://miro.medium.com/max/1298/0*80kLCjqmNvBTdQdt.png 649w" sizes="649px"/></noscript>

Total derivative assumes all variables are potentially co-dependent where as partial derivative assumes all variables but _x_ are constants.

when you take the total derivative with respect to x, other variables might also be functions of _x_ so add in their contributions as well. The left side of the equation looks like a typical partial derivative but the right-hand side is actually the total derivative.

Lets see example,

![Image for post](https://miro.medium.com/max/60/0*shZeABxUNias1l5M.png?q=20)

<noscript><img alt="Image for post" class="t u v hm aj" src="https://miro.medium.com/max/1346/0*shZeABxUNias1l5M.png" width="673" height="234" srcSet="https://miro.medium.com/max/552/0*shZeABxUNias1l5M.png 276w, https://miro.medium.com/max/1104/0*shZeABxUNias1l5M.png 552w, https://miro.medium.com/max/1280/0*shZeABxUNias1l5M.png 640w, https://miro.medium.com/max/1346/0*shZeABxUNias1l5M.png 673w" sizes="673px"/></noscript>

total derivative formula always _sums_, that is sums up terms in the derivative. For example, given y = x × x² instead of y = x + x² , the total-derivative chain rule formula still adds partial derivative terms, for more detail see demonstration in paper.

Formula of total derivative can be simplified further.

![Image for post](https://miro.medium.com/max/60/0*sDqWUk96xgMSeazo.png?q=20)

<noscript><img alt="Image for post" class="t u v hm aj" src="https://miro.medium.com/max/1354/0*sDqWUk96xgMSeazo.png" width="677" height="111" srcSet="https://miro.medium.com/max/552/0*sDqWUk96xgMSeazo.png 276w, https://miro.medium.com/max/1104/0*sDqWUk96xgMSeazo.png 552w, https://miro.medium.com/max/1280/0*sDqWUk96xgMSeazo.png 640w, https://miro.medium.com/max/1354/0*sDqWUk96xgMSeazo.png 677w" sizes="677px"/></noscript>

This chain rule that takes into consideration the total derivative degenerates to the single-variable chain rule when all intermediate variables are functions of a single variable.

# Vector chain rule

derivative of a sample vector function with respect to a scalar, **y** = **f** (x).

![Image for post](https://miro.medium.com/max/60/0*1O9MEs3qhfvg_44T.jpg?q=20)

<noscript><img alt="Image for post" class="t u v hm aj" src="https://miro.medium.com/max/2800/0*1O9MEs3qhfvg_44T.jpg" width="1400" height="932" srcSet="https://miro.medium.com/max/552/0*1O9MEs3qhfvg_44T.jpg 276w, https://miro.medium.com/max/1104/0*1O9MEs3qhfvg_44T.jpg 552w, https://miro.medium.com/max/1280/0*1O9MEs3qhfvg_44T.jpg 640w, https://miro.medium.com/max/1400/0*1O9MEs3qhfvg_44T.jpg 700w" sizes="700px"/></noscript>

introduce two intermediate variables, g 1 and g 2 , one for each f i so that y looks more like **y** = **f** ( **g**(x))

![Image for post](https://miro.medium.com/max/60/0*W-RGdM4ajlxxxoDo.jpg?q=20)

<noscript><img alt="Image for post" class="t u v hm aj" src="https://miro.medium.com/max/2800/0*W-RGdM4ajlxxxoDo.jpg" width="1400" height="1179" srcSet="https://miro.medium.com/max/552/0*W-RGdM4ajlxxxoDo.jpg 276w, https://miro.medium.com/max/1104/0*W-RGdM4ajlxxxoDo.jpg 552w, https://miro.medium.com/max/1280/0*W-RGdM4ajlxxxoDo.jpg 640w, https://miro.medium.com/max/1400/0*W-RGdM4ajlxxxoDo.jpg 700w" sizes="700px"/></noscript>

If we split the terms, isolating the terms into a vector, we get a matrix by vector.

![Image for post](https://miro.medium.com/max/60/0*Af_9ZBseZjTGICSo.jpg?q=20)

<noscript><img alt="Image for post" class="t u v hm aj" src="https://miro.medium.com/max/2800/0*Af_9ZBseZjTGICSo.jpg" width="1400" height="872" srcSet="https://miro.medium.com/max/552/0*Af_9ZBseZjTGICSo.jpg 276w, https://miro.medium.com/max/1104/0*Af_9ZBseZjTGICSo.jpg 552w, https://miro.medium.com/max/1280/0*Af_9ZBseZjTGICSo.jpg 640w, https://miro.medium.com/max/1400/0*Af_9ZBseZjTGICSo.jpg 700w" sizes="700px"/></noscript>

This completes chain rule. In next blog that is part3 we will see how we can apply this gradient of neural activation and loss function and wrap up.

Thank you.

Useful Points:

It is difficult while writing a blog in markdown to convert to superscript and subscript so I have listed down, which you can use ( copy-paste) in your markdown

superscript ⁰ ¹ ² ³ ⁴ ⁵ ⁶ ⁷ ⁸ ⁹ ᵃ ᵇ ᶜ ᵈ ᵉ ᶠ ᵍ ʰ ᶦ ʲ ᵏ ˡ ᵐ ⁿ ᵒ ᵖ ʳ ˢ ᵗ ᵘ ᵛ ʷ ˣ ʸ ᶻ

subscript ₀ ₁ ₂ ₃ ₄ ₅ ₆ ₇ ₈ ₉ ₐ ᵦ 𝒸 𝒹 ₑ 𝒻 𝓰 ₕ ᵢ ⱼ ₖ ₗ ₘ ₙ ₒ ₚ ᵩ ᵣ ₛ ₜ ᵤ ᵥ 𝓌 ₓ ᵧ 𝓏

# **Blog 10**

<span class="jx ej fm jy jz ka"></span><span class="jx ej fm jy jz ka"></span><span class="jx ej fm jy jz"></span>

_Originally published at_ [_https://kirankamath.netlify.app_](https://kirankamath.netlify.app/blog/matrix-calculus-for-deeplearning-part2/)_._