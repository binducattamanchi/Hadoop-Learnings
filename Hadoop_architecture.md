# Hadoop EcoSystem


![image](https://user-images.githubusercontent.com/32897934/124363078-c11af680-dc56-11eb-904b-caee388d197b.png)


# YARN Architecture

![image](https://user-images.githubusercontent.com/32897934/124363099-ef003b00-dc56-11eb-9bac-6a95d490e24b.png)

# Hive Architecture

![image](https://user-images.githubusercontent.com/32897934/124363111-07705580-dc57-11eb-871b-5b03763cd48f.png)


# MapReduce execution steps

![image](https://user-images.githubusercontent.com/32897934/124363637-14427880-dc5a-11eb-8c05-d846988437c6.png)


* Input Splits:

An input to a MapReduce in Big Data job is divided into fixed-size pieces called input splits Input split is a chunk of the input that is consumed by a single map

* Record Reader:

Converts data into key value format.
InputFormat class calls the getSplits() function and computes splits for each file and then sends them to the JobTracker, which uses their storage locations to schedule map tasks to process them on the TaskTrackers. Map task then passes the split to the createRecordReader() method on InputFormat in task tracker to obtain a RecordReader for that split. The RecordReader load’s data from its source and converts into key-value pairs suitable for reading by the mapper.

* Mapping

This is the very first phase in the execution of map-reduce program. In this phase data in each split is passed to a mapping function to produce output values. In our example, a job of mapping phase is to count a number of occurrences of each word from input splits (more details about input-split is given below) and prepare a list in the form of <word, frequency>

* Partitioner

Partitioning of the keys of the intermediate map output is controlled by the Partitioner. By hash function, key (or a subset of the key) is used to derive the partition. According to the key-value each mapper output is partitioned and records having the same key value go into the same partition (within each mapper), and then each partition is sent to a reducer. Partition class determines which partition a given (key, value) pair will go. Partition phase takes place after map phase and before reduce phase.
Default is hash partitioning.

* Combiner

The combiner in MapReduce is also known as ‘Mini-reducer’. The primary job of Combiner is to process the output data from the Mapper, before passing it to Reducer. It runs after the mapper and before the Reducer and its use is optional.


* Shuffling

This phase consumes the output of Mapping phase. Its task is to consolidate the relevant records from Mapping phase output. In our example, the same words are clubed together along with their respective frequency.

* Reducing

In this phase, output values from the Shuffling phase are aggregated. This phase combines values from Shuffling phase and returns a single output value. In short, this phase summarizes the complete dataset.

* Seconday Sorting

If we want to sort reducer’s values, then the secondary sorting technique is used as it enables us to sort the values (in ascending or descending order) passed to each reducer.

# Yarn execution

![image](https://user-images.githubusercontent.com/32897934/124363370-7ac69700-dc58-11eb-92e0-627681fe6d91.png)

Application workflow in Hadoop YARN:

![image](https://user-images.githubusercontent.com/32897934/124363550-78187180-dc59-11eb-9513-55bdc35aa868.png)


1. Client submits an application
2. The Resource Manager allocates a container to start the Application Manager
3. The Application Manager registers itself with the Resource Manager
4. The Application Manager negotiates containers from the Resource Manager
5. The Application Manager notifies the Node Manager to launch containers
6. Application code is executed in the container
7. Client contacts Resource Manager/Application Manager to monitor application’s status
8. Once the processing is complete, the Application Manager un-registers with the Resource Manager

