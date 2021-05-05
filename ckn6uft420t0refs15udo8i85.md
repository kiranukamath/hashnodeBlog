## Establishing connection to Couchbase server from aws ec2 instance using Couchbase Java SDK

I was having problem in establishing connection to Couchbase server in ec2 from my laptop using public ip in Couchbase java sdk.
So for me, only way moving forward was creating maven project in ec2 instance and connect to Couchbase using connection String "localhost".

This blog is about how I created maven project in Ubuntu ec2 instance from terminal and established connection to Couchbase server to fetch data from bucket.

Maven is a Java tool, so you must have Java installed in order to proceed.  
First, download Maven and follow the  [installation instructions](https://maven.apache.org/install.html) .
I am using ubuntu in ec2 so, your steps may change if your using windows or mac.

```
mvn --version
```
Once confirmed on maven is installed, move to creating maven project.

Create a folder and start shell there, and execute the following Maven command.
```
mvn archetype:generate -DgroupId=com.couchbase.client -DartifactId=couchbaseanalytics -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```
Here ‘DartifactId‘ is your project name and ‘DarchetypeArtifactId‘ is the type of Maven project.

Once you press Enter after typing the above command, it will start creating the Maven project.
If you have just installed Maven, it may take a while on the first run. This is because Maven is downloading the most recent artifacts (plugin jars and other files) into your repository. You may also need to execute the command a couple of times before it succeeds. This is because the remote server may time out before your downloads are complete.

**ERROR**: In case of build failure, please check the Maven version number in the pom.xml file. It should match the version of Maven installed on your machine.

Once that the command is executed that it created a directory with the same name given as the artifactId. Change into that directory.

` cd couchbaseanalytics`

Under this directory you will notice the following standard project structure. If this is not, then you might have deviated somewhere.
```
couchbaseanalytics
|-- pom.xml
`-- src
    |-- main
    |   `-- java
    |       `-- com
    |           `-- couchbase
    |               `-- client
    |                   `-- App.java
    `-- test
        `-- java
            `-- com
                `-- couchbase
                    `-- client
                        `-- AppTest.java
```

The src/main/java directory should contain the project source code, and the pom.xml file is the project's Project Object Model, or POM.

The pom.xml file is the core of a project's configuration in Maven. It is a single configuration file that contains the majority of information required to build a project in just the way you want.

Open pom file and try to explore different fields.

Now run below command to build the project.
``` 
mvn package
```
Once you get BUILD SUCCESS , You may test the newly compiled and packaged JAR with the following command:
```
java -cp target/couchbaseanalytics-1.0-SNAPSHOT.jar com.couchbase.client.App
```
This command will print :

`Hello World!`

### Now adapting this project to connect to couchbase:

Now add below to pom.xml file inside `<dependencies>`:
```
<dependency>
        <groupId>com.couchbase.client</groupId>
        <artifactId>java-client</artifactId>
        <version>3.1.3</version>
</dependency>
```
once that is done, edit java App.java file:  
you can open using vi, I used following command instead of cd directory:

``` 
vi /home/ubuntu/kiran/couchbaseanalytics/src/main/java/com/couchbase/client/App.java 
```

Note: your path may be different so change it respectively.

Add below code inside main class

`Cluster cluster = Cluster.connect(connectionString, username, password);`

connectionString is "localhost"

The Cluster provides access to cluster-level operations like N1Ql queries, analytics or full-text search. 

following imports are necessary to build the snippets:
```
import com.couchbase.client.java.*;
import com.couchbase.client.java.kv.*;
import com.couchbase.client.java.json.*;
import com.couchbase.client.java.query.*;
```

To access the KV (Key/Value) API or to query views, you need to open a Bucket:
```
// get a bucket reference
Bucket bucket = cluster.bucket(bucketName);
```
perform a N1QL query at the cluster level:
```
QueryResult result = cluster.query("select * from `beer-sample` limit 10");
System.out.println(result.rowsAsObject());
```
Note: I had bucket `beer-sample` you can replace that with bucket name you have.

Now run:

` mvn clean install`

```
mvn compile exec:java -Dexec.mainClass="com.couchbase.client.App" -Dexec.arguments="Hello World,Bye"
```

you should see records from bucket in terminal.



### If you want to copy and paste to run the full code, here it is:

```
import com.couchbase.client.java.*;
import com.couchbase.client.java.kv.*;
import com.couchbase.client.java.json.*;
import com.couchbase.client.java.query.*;

public class App {
	public static void main(String[] args) {

    Cluster cluster = Cluster.connect(connectionString, username, password);
    Bucket bucket = cluster.bucket(bucketName);

    QueryResult result = cluster.query("select * from `beer-sample` limit 10");
    System.out.println(result.rowsAsObject());

}
```

Hurray!!! That's it. Now you have established connection with Couchbase server. You can edit code in App.java to adapt to your use case.