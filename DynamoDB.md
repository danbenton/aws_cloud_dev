# Intro to DynamoDB
### What is DynamoDB: 
A fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. 
It is a fully managed database and supports both document and key-value data models.  Its flexible data model and reliable performance make it a great fit for mobile, web, gaming, ad-tech, IoT and many other applications.    
- Stored on SSD Storage 
- Spread across 3 geograhpically distinct data centers    
- Choice of 2 consistency models:     
  - Eventual Consistent Reads (Default)   
    - Consistenty across all copies of data is usually reached within a second.  Repeating a read after a short time should return the updated data (Best Read Performance).    
  - Strongly Consistent Reads     
    - Returns a result that reflects all writes that received a successful response prior to the read.    
#### DynamoDB Characteristics   
- Tables   
- Items (think of a row of data in a table)    
- Attributes (think of a column of data in a table)   
- Supports key-value and document data structures    
  - Key = The name of the data
  - Value = the data itself    
- Documents can be written in JSON, HTML or XML  
### DynamoDB - Primary Keys   
DynamoDB stores and retrieves data based on a Primary Key   
Two Types of Primary Keys:    
1) **Partition Key** - unique attributed (e.g. user ID)  
- Value of the partition key is input to an internal hash function which determines the partition or physical location on which the data is stored.    
- If you are using the partition key as your primary key, then no two items can have the same partition key    
2) **Composite Key** (Partition Key + Sort Key) in combination; e.g same user posting multiple times to a forum    
- Primary Key would be a composite key consisting of: 
  - Partition Key - user ID  
  - Sort Key - Timestamp of a post    
- Two items may have the same partition key but they must have a different sort key   
- All items with the same partition key are stored together, then sorted according tot he sort key value .  
- Allows you to store multiple items with the same partition key   
### DynamoDB Access Control    
- Authentication and Access Control is managed using AWS IAM   
- You can create an IAM user within your AWS account which has specific permissions to access and create DynamoDB tables   
- You can create an IAM role which enables you to obtain temporary access keys which can be used to access DynamoDB   
- You can also use a special **IAM Condition** to restrict user access to only their own records     
## Exam Tips   
- Fine grained access control using IAM Condition parameter:  
  _ **dynamodb:LeadingKeys** to allow users to access only the items where the parition key value matches their user ID   
# Indexes Deepdive  
In SQL databases, an index is a data structure which allows you to perform fast queries on specific columns in a table.  
You select the colums that you want included in the index and run your searches on the index - rather than on the entire dataset.    

In DynamoDB, two types of Indecies are suppord to help speed-up queries:    
1) **Local Secondary Index**    
- Can only be created when you are creating your table  
- You cannot add, remove, or modify it later   
- It has the same *Partition Key* as your original table; but different *Sort Key* 
- Gives you a different view of your data, organized accoreing to an alternative sort key   
- Any queries base don this sort key are much faster using the index than the main table    
  - e.g. 
    - Partition Key: user ID 
    - Sort Key: Account creation date    
2) **Global Secondary Index**  
- Create it when you create your table, or add it later   
- Different partition ***and*** sort key   
- Gives a different view of the data   
- Speeds up any queries relating to this alternative Partition and Sort Key   
- e.g. 
  - Partition Key: email address   
  - Sort Key: last log-in date   
# Scan vs. Query API Call   
### What is a Query?    
- A **Query** operation finds items in a table base don the Primary Key attribut3 and a distinct value to search for    
  - e.g. select an item where the user ID is equal to 212, will select all the attributes for that item (first name, surname, email, etc.)    
- Use optional sort key name and value to refine the results . 
  - e.g. if your sort key is a time stamp, you can refine the query to only select items with a timestamp of the last 7 days   
- By default, a Query returns all the attributes for the items but you can use the **ProjectionExpression** parameter if you want the query to only return the specific attributes you want   
  - e.g. if you only want to see the email address rather than all the attributes 
- Results are always sorted by the sort key   
- Numeric order, by default in ascending order (1, 2, 3, 4)   
- ASCII character code values   
- You can revers the order by setting the **ScanIndexForwardparameter** to false   
- By default, Queries are *Eventually Consistent*   
- You need to explicitly se the query to be *Strongly Consistent*   
### What is a Scan?  
- A **Scan** operation examines every item in the table   
- By default returns all data attributes   
- Use the **ProjectionExpression** parameter to refine the scan to only return the attributes you want    
### Query or Scan?   
- Query is more efficient than Scan   
- Scan dumps the entire table, then filters out the valus to provide the desired result - removing the unwanted data 
- This adds an extra step of removing the data you don't want   
- As the table grows, scan operations take longer   
- Scan operations on a large table can use up the provisioned throughput for a large table in a single operation   
### How to Improve Performance      
- Reduce the impace of a query/scan by setting a smaller page size which uses fewer read operations     
  - e.g. set the page size to return 40 items   
- Larger number of smaller operations will allow other requests to succeed without throttling   
- Avoid using scan operations if you can; design tables ina way that you can use the Query, Get or BatchGetItem APIs   
- By default, a scan operation processes data sequentially in returning 1MB increments befor moving on to retrieve the next 1MB of ata.  It can only scan one partition at a time.      
- You can configure DynamoDB to use parallel scans instead by logically divigin a table or index into segments and scanning each segment in parallel   
- Best to avoid parallel scans if your table or index is already incurring heavy read / write activity from other applications    
## Exam Tips   
- A Query operation finds items in table using only the Primary Key attribute 
  - You provide the Primary Key name and a distinct value to search for  
- A Scan operation examines every item in the table; by default, returns all data attributes   
  - Use the **ProjectionExpression** parameter to refine the results; can also use filter   
- Query results are always sorted by the sort key if there is one; sorted in ascending order . 
- Set **ScanIndexForward** parameter to false to reverse the order - queries only   
- Query operation is generally more efficient than a Scan   
# DynamoDB Provisioned Throughput   
- DynamoDB Provisioned Throughput is measured in Capacity Units  
- When you create your table, you specifiy your requirements in terms of Read Capacity Units and Write Capacity Units   
- 1 x Write Capacity Unit = 1 x 1KB Write per second  
- 1 x Read Capacity Unit = 1 x Strongly Consistent Read of 4KB per second **or** 2 x Eventually Consistent Reads of 4KB per second (Default)    
### Strongly Consistent Reads Calculation     
- Your application needs to read 80 items (table rows) per second: each item is 3KB in size - you need Strongly Consisten Reads   
- First, calculate how many Read Capacity Units needed for each read:  Size of each item / 4KB   
  - 3KB / 4KB  
  - Rounded up to the nearest whole number, each read will need 1 x Read Capacity Unit per read operation    
  - Multiplied by the nubmer of reads per second = 80 Read Capacity Units required     
### Eventually Consistent Reads Calculation   
- Same calculation but with you get 2 x 4KB reads per second - or **double** the throughput of Strongly Consisten reads   
- Divide 80 by 2, so you only need 40 Read Capacity Units for Eventually Consistent reads   
### Write Capacity Units Calulation   
- You want to write 100 items per second; each item is 512 bytes in size   
- First, calculate how many Capacity Units for each write:  Size of each item / 1KB   
  - 512 bytes / 1KB = .5   
  - Rounded-up to the nearest whole number, each write will need 1 x Write Capacity Unit per write operation   
  - Multiplied by the number of writes per second = 100 Write Capacity Units required    
# DynamoDB On-Demand Capacity   
- Charges apply for: Reading, Writing and Storing data   
- With On-Demand, you don't need to specify your requirements    
- DynamoDB instantly scales up and down based on the actvity of your application   
- Great for unpredictable workloads   
- You want to pay for only what you use (pay per request)  
### Use Cases  
- Unknown workloads  
- Unpredictable application traffic   
- You want a Pay-per-use model   
- Spiky, short lived peaks 
*You can switched between On-Demand vs. Provisioned Capacity **once** per day*   
# DynamoDB Accelerator (DAX)  
### What is DAX?    
**DynamoDB Accelerator (DAX)** is a fully managed, clustered in-memory cache for DynamoDB.  
- Delivers up to a 10x read performance improvement  
- Microsecond performance for millions of requests per second   
- Ideal for Read-Heavy and bursty workloads
  - e.g. auction applications, gaming and retail sites during black Friday promotions    
### How Does it Work?   
- DAX is a write-through caching service - this means data is written to teh cache as well as the back end store at the same time   
- Allows you to point your DynamoDB API calls at the DAX cluster   
- If the item you are querying is in the cache (cache hit), DAX returns the result to the application    
- If the item is not available (cache miss) then DAX performs an Eventually Consistent GetItem operation against DynamoDB  
- Retrevial of data from DAX reduces the read load on DynamoDB tables   
- May be able to reduce Provisioned Read Capacity     
### What is it NOT Suitable For?   
- Caters for **Eventually Consistent** reads only - so not suitable for applications that require Strongly Consisten reads   
- Write intensive applications (DAX is read only)  
- Applications that do not perform many operations   
- Applications that do not requre microsecond response times   
- 


  
  







  


