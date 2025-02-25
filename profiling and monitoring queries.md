# Profiling and Monitoring Queries

Queries are profiled and monitored by issuing commands on the AnyLog command prompt or from a REST client.

Profiling is supported by several processes:  
a. a process providing statistical information on queries execution time.  
b. a process identifying slow queries.  
c. a process to identify the SQL used on each participating node.  

## Statistical information
In order to get statistical information, use the following command:  
On the AnyLog command prompt:  
```get queries time```  
From a REST client send a REST message and place in the headers the following keys and values:  
```type : info```  
```details : get queries time```

## Identifying slow queries

Slow queries can be redirected to the query log with the following AnyLog command:  

```set query log profile [n] seconds```   

The  ***set query log*** records all queries in the query log whereas adding ***profile [n] seconds***
places in the query log only queries with execution time greater or equal to [n] seconds.

To view the slow query log use the following command on the AnyLog command prompt:  
```get query log```  
From a REST client send a REST message and place in the headers the following keys and values:  
```type : info```  
```details : get query log```

### Command options for profiling and monitoring queries

Queries are executed in a context of jobs. A job is a process that sends a message to a peer in the network and is listed in a structure
that maintains information on the status of the message and the command execution status.

The command ***query*** considers the queries commands that are send to peers in the network.
Each job (including a query) is assigned with an ID which can be used by a user to indicate the job in interest.

The command ***query*** provides information on the last executed queries and there are 2 types of information captured on every executed query:  
1. Status - details the status of each query
2. Explain - Provides the SQL statement used on the nodes that participate in the query process.
 

```query status all``` - The status information on the last executed querys<br/>
```query status``` - The status information on the most recent executed query<br/>
```query status n``` - The status information on a particular query whereas n is the id of the job<br/>

```query explain all``` - The explain plan of the last executed querys<br/>
```query explain``` - The explain plan on the most recent executed query<br/>
```query explain n``` - The explain plan on a particular query<br/>

## Retrieving the status of queries being processed on an Operator node

Each operator can process many concurrent queries.  
The command ***get query execution*** provides the info on the currently processed queries.  
Usage:
<pre>
get query execution where node = [node id] and job = [job id]
</pre> 

[node id] is the IP of the query node.  
[job id] is the id of the query assigned by the query node (the command ***query status*** on the query node provides the job id).  

Example:
<pre>
 get query execution where node = 10.0.0.78 and job = 12
</pre> 



