# Map side join ( REplicated join)
`using distributed cache on smaller table`

Map-side Join is similar to a join but  all the task will be performed by the mapper alone.

The Map-side Join will be mostly suitable for small tables to optimize the task.

How will the map-side join optimize the task?
Assume that we have two tables of which one of them is a small table. When we submit a map reduce task, a Map Reduce local task will be created before the original join Map Reduce task which will read data of the small table from HDFS and store it into an in-memory hash table. After reading, it serializes the in-memory hash table into a hash table file.

In the next stage, when the original join Map Reduce task is running, it moves the data in the hash table file to the Hadoop distributed cache, which populates these files to each mapper’s local disk. So all the mappers can load this persistent hash table file back into the memory and do the join work as before. The execution flow of the optimized map join is shown in the figure below. After optimization, the small table needs to be read just once. Also if multiple mappers are running on the same machine, the distributed cache only needs to push one copy of the hash table file to this machine.

![image](https://user-images.githubusercontent.com/32897934/124363994-3f2dcc00-dc5c-11eb-9c9b-cffccaa5c62f.png)

Advantages of using map side join:
Map-side join helps in minimizing the cost that is incurred for sorting and merging in the shuffle and reduce stages.
Map-side join also helps in improving the performance of the task by decreasing the time to finish the task.
Disadvantages of Map-side join:
Map side join is adequate only when one of the tables on which you perform map-side join operation is small enough to fit into the memory.  Hence it is not suitable to perform map-side join on the tables which are huge data in both of them.

# Reduce side join

![image](https://user-images.githubusercontent.com/32897934/124363910-d2b2cd00-dc5b-11eb-88cb-b0843f2ca351.png)

the reduce side join takes place in the following manner:

 - Mapper reads the input data which are to be combined based on common column or join key.
 - The mapper processes the input and adds a tag to the input to distinguish the input belonging from different sources or data sets or databases.
 - The mapper outputs the intermediate key-value pair where the key is nothing but the join key.
 - After the sorting and shuffling phase, a key and the list of values is generated for the reducer. 
 - Now, the reducer joins the values present in the list with the key to give the final aggregated output.

# replicated semi-join

`reduce side join with map side filtering`

even of the filtered data of small table doesn’t fit in to the memory it may be possible to include just the dept_id s of filtered records in the replicated data set. then at map side this cache can be used to filter out records which would be sent over to reduce side thus reducing the amount of data moved between the mappers and reducers.

