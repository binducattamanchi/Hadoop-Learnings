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

* Mapping

This is the very first phase in the execution of map-reduce program. In this phase data in each split is passed to a mapping function to produce output values. In our example, a job of mapping phase is to count a number of occurrences of each word from input splits (more details about input-split is given below) and prepare a list in the form of <word, frequency>

* Shuffling

This phase consumes the output of Mapping phase. Its task is to consolidate the relevant records from Mapping phase output. In our example, the same words are clubed together along with their respective frequency.

* Reducing

In this phase, output values from the Shuffling phase are aggregated. This phase combines values from Shuffling phase and returns a single output value. In short, this phase summarizes the complete dataset.

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

