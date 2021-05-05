## Exploring Couchbase Analytics Service

Recently I have been exploring Couchbase Analytics service and finding out how it could be more useful and increase efficiency compared to Couchbase query service.

Couchbase Analytics service comes with enterprise addition.

Couchbase Analytics is a parallel data management capability for Couchbase Server which is designed to efficiently run large ad hoc join, set, aggregation, and grouping operations over many records.

**Why analytics?**

Every business does these three things in a cycle or a spiral [The Goal]. 
1. Run the business process to deliver products or services to the customers. 
2. Analyze the business to determine what to change and what to change to. 
3. Make the change happen. 


The Query Service is used by the applications needed to run the the business; it is designed for large number of concurrent queries, each doing small amount of work.  In the RDBMS world, this workload is called the OLTP workload. 

Applications or tools used for analysis have different workload characteristics.  These typically use the Analytics Service; it is designed for a smaller number of concurrent queries analyzing a larger number of documents. In the RDBMS world, this workload is called the OLAP workload(Online analytical processing) 

 Advantages Couchbase Analytics approach/ WHY Couchbase Analytics? 

**Common data model**: we don’t have to force our data into a flat, predefined, relational model to analyze it  
**Workload isolation**: Operational query latency and throughput are protected from slow-downs due to your analytical query workload  
**High data freshness**: Analytics runs on data that’s extremely current, without ETL or delays. 
**Continuous data sync**  
**Easy to manage SQL++ interface**  
Reduce infrastructure complexity, application development complexity, and cost with a single system for operations and analytics. 

Analytics Service should be run alone, on its own cluster node, with no other Couchbase Service running on that node Due to the large scale and duration of operations it is likely to perform. 

The minimum memory(RAM) quota required is 1024 MB for analytics service. 

Analytics queries never touch Couchbase data servers, but instead running on real-time shadow copies of our data in parallel. Because of this, there is no worry about slowing down the Couchbase Server nodes with complex queries.

### Dataverse
The top-level organizing concept in the Analytics data world is the dataverse.  

A **dataverse**, is a namespace that gives you a place to create and manage datasets and other artifacts for a given Analytics application.  

In that respect, a dataverse is similar to a database or a schema(schema is the skeleton structure that represents the logical view of the entire database. It defines how the data is organized and how the relations among them are associated) in a relational DBMS. 

Datasets are containers that hold collections of JSON objects. They are similar to tables in an RDBMS or keyspaces in N1QL. A dataset is linked to a Couchbase bucket so that the dataset can ingest data from Couchbase Server.

Fresh Analytics instance starts out with two dataverses, one called Metadata (the system catalog) and one called Default (available for holding data). 

The first task is to tell Analytics about the Couchbase Server data that you want to shadow and the datasets where you want it to live. 


```
CREATE DATASET datasetName ON `bucketName`; 
```
If the bucket has data that are of different types or categories, we can create a separate dataset for those using `WHERE`  and it will be created.

```
CONNECT LINK Local; 
```

Local = local server(Data service in the same cluster) 

Now perform basic query from analytics service to check if everything is working fine.

```
SELECT meta(k) AS meta, k AS data 
FROM datasetName k 
LIMIT 1; 
```

As in SQL, the query’s FROM clause binds the variable `k` incrementally to the data instances residing in the dataset named `datasetName`.  The SELECT clause returns all of the meta-information plus the data value for each binding that satisfies the predicate.

Once this is set up you can access this service from Couchbase java SDK too.

 Follow [Establishing connection to Couchbase server using Couchbase Java SDK](https://kirankamath.hashnode.dev/establishing-connection-to-couchbase-server-from-aws-ec2-instance) to set up Java SDK.

After following that blog edit App.java code with following code to use Couchbase analytics.
```
import com.couchbase.client.java.*;
import com.couchbase.client.java.kv.*;
import com.couchbase.client.java.json.*;
import com.couchbase.client.java.query.*;
import com.couchbase.client.core.error.CouchbaseException;
import com.couchbase.client.java.analytics.*;


public class App {
	public static void main(String[] args) {
		try {
			Cluster cluster = Cluster.connect("localhost", "username", "password");
			  final AnalyticsResult result = cluster
			    .analyticsQuery("SELECT * FROM datasetName LIMIT 2;");

			  
			  for (JsonObject row : result.rowsAsObject()) {
	                System.out.println("Found row: " + row);
	                System.out.println();
	              
			  }

			} catch (CouchbaseException ex) {
			  ex.printStackTrace();
			}
	}
}

```











Credits:  [Couchbase Documentation](https://docs.couchbase.com/home/index.html) 