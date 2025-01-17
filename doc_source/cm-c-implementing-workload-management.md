# Implementing Workload Management<a name="cm-c-implementing-workload-management"></a>


|  | 
| --- |
|  Currently, **Automatic WLM** is not available in all Amazon Redshift Regions\. Automatic WLM and associated Amazon Redshift console changes will be deployed to additional AWS Regions in the upcoming releases\.  | 

You can use workload management \(WLM\) to define multiple query queues and to route queries to the appropriate queues at run time\.

In some cases, you might have multiple sessions or users running queries at the same time\. In these cases, some queries might consume cluster resources for long periods of time and affect the performance of other queries\. For example, suppose that one group of users submits occasional complex, long\-running queries that select and sort rows from several large tables\. Another group frequently submits short queries that select only a few rows from one or two tables and run in a few seconds\. In this situation, the short\-running queries might have to wait in a queue for a long\-running query to complete\. 

With Concurrency Scaling, you can support virtually unlimited concurrent users and concurrent queries, with consistently fast query performance\. For more information, see [Concurrency Scaling](concurrency-scaling.md)\.

You can configure Amazon Redshift WLM to run with either automatic WLM or manual WLM\.
+ Automatic WLM

  You can enable Amazon Redshift to manage how resources are divided to run concurrent queries with automatic WLM\. *Automatic WLM *manages the resources required to run queries\. Amazon Redshift determines how many concurrent queries and how much memory is allocated to each dispatched query\. You can enable automatic WLM using the Amazon Redshift console by choosing **Switch WLM mode** and then choosing **Auto WLM**\. With this choice, one queue is used to manage queries, and the **Memory** and **Concurrency on main** fields are both set to **auto**\. For more information, see [Automatic Workload Management \(WLM\)](automatic-wlm.md)\. 
+ Manual WLM

  Alternatively, you can manage system performance and your users' experience by modifying your WLM configuration to create separate queues for the long\-running queries and the short\-running queries\. At run time, you can route queries to these queues according to user groups or query groups\. You can enable this manual configuration using the Amazon Redshift console by switching to **Manual WLM**\. With this choice, you specify the queues used to manage queries, and the **Memory** and **Concurrency on main** field values\. 

  With a manual configuration, you can configure up to eight query queues and set the number of queries that can run in each of those queues concurrently\. You can set up rules to route queries to particular queues based on the user running the query or labels that you specify\. You can also configure the amount of memory allocated to each queue, so that large queries run in queues with more memory than other queues\. You can also configure a query monitoring rule \(QMR\) to limit long\-running queries\. 
**Note**  
We recommend configuring your manual WLM query queues with a total of 15 or fewer query slots\. For more information, see [Concurrency Level](cm-c-defining-query-queues.md#cm-c-defining-query-queues-concurrency-level)\.

When switching between **Auto WLM** and **Manual WLM**, your cluster is put into `pending reboot` state\. The change doesn't take effect until a cluster reboot\.

**Topics**
+ [Defining Query Queues](cm-c-defining-query-queues.md)
+ [Automatic Workload Management \(WLM\)](automatic-wlm.md)
+ [Concurrency Scaling](concurrency-scaling.md)
+ [WLM Query Queue Hopping](wlm-queue-hopping.md)
+ [Short Query Acceleration](wlm-short-query-acceleration.md)
+ [Modifying the WLM Configuration](cm-c-modifying-wlm-configuration.md)
+ [WLM Queue Assignment Rules](cm-c-wlm-queue-assignment-rules.md)
+ [Assigning Queries to Queues](cm-c-executing-queries.md)
+ [WLM Dynamic and Static Configuration Properties](cm-c-wlm-dynamic-properties.md)
+ [WLM Query Monitoring Rules](cm-c-wlm-query-monitoring-rules.md)
+ [WLM System Tables and Views](cm-c-wlm-system-tables-and-views.md)