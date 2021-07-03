# Hadoop EcoSystem


![image](https://user-images.githubusercontent.com/32897934/124363078-c11af680-dc56-11eb-904b-caee388d197b.png)


# YARN Architecture

![image](https://user-images.githubusercontent.com/32897934/124363099-ef003b00-dc56-11eb-9bac-6a95d490e24b.png)

# Hive Architecture

![image](https://user-images.githubusercontent.com/32897934/124363111-07705580-dc57-11eb-871b-5b03763cd48f.png)


# MapReduce execution steps

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

