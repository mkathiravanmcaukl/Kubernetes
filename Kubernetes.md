-> Kubernetes is an orchestration tool

### Self Healing

--> If any container crash it will scale up automatically. When the container loading is up it will automatically scaling up and when the container space looks free it will automatically scale down. This is called **Auto Scaling**

--> Kubernetes having two nodes one is master node and another one is slave node

---> Master node having controller manager, API server, ETCD and Scheduler. **API server** is important role in the master node. Every communication is done through API Server. **Controller manager** is maintain the state of the container. It maintain the desire state and actual state. **ETCD** maintain the databse so the API manager ask to the ETCD what is the desire state of the container. **Schedule**r is maintain where we have to create the container inside the worker node so it will check all the system CPU and memory according to that will create the container.  

--> Each and every worker node having **KUBELET**. **API Server** will inform to the Kubelet we have to create one container with this image name so kubelet will inform to **CONTAINER RUNTIME** it will create a container. 

--> **CONTAINER RUNTIME** will create an image pull, container run and remove all the processes handle by **CRI(Container Runtime Interface)**

--> **KUBELET** will monitor all the container process whether it is running or not and crash. If any container will crash then **KUBELET** will inform to the CRI to remove the container. **KUBELET** will inform to the **API server** we have removed one container. **API Manager** will inform to the **Controller Manager** to check the state 

<img width="1711" height="1033" alt="Screenshot 2025-12-30 at 10 50 20 AM" src="https://github.com/user-attachments/assets/be7d28a8-ab6b-4ba2-8995-902d64ea7550" />

### Kubernetes POD

 --> When we create a container it will store inside the POD. POD will provider network, database for the container. When we create a POD each POD having unique IP address. If any POD is communicate with another POD it should know the IP address of another POD. Pods are isolated from each other. We can have multiple container inside a POD

 --> Continer inside the a POD, shares the network and storage. Containers inside a POD can communicate without IP address. For example if POD having two container one is working good and another one is getting crash means Kubernets will remove the whole POD and create a new POD with the two containers. So in this scenario we can create each container will create with separeate POD so one container will crash then particular POD will be only remove from kubernets other POD will run smootly. When this type of scenario is happen means one application depends on another application(Tightly coupled applications). 


### How to create a POD

       kubectl apply -f pod.yml

 After creating a Pod want to check this status   

       kubectl get pods

 Want to check ip address of the pod

      kubectl get pods -o wide

 To check full detail of the pod 

     kubectl describe pods podName

 For delete a pod

    kubectl delete pod podName

  <img width="1720" height="930" alt="Screenshot 2025-12-30 at 12 58 20 PM" src="https://github.com/user-attachments/assets/58cd49d1-429b-43c7-b5dc-227940c12260" />
   

<img width="1727" height="967" alt="Screenshot 2025-12-30 at 11 06 33 AM" src="https://github.com/user-attachments/assets/8f75beed-e231-4edc-9e93-dd979437051e" />

### Replica Set

 --> It contains to how many numbeer of copy of the pod.

 --> Pod creating file called as PodManifest file(yml)

 --> Replica creating file called as ReplicaManifest file (yml)

 --> Matching labels and Pod labels should be same

 --> Controller Manager having different controller like ReplicaSet Controller, StatefulSet Controller, DeameonSet Controller, etc..

 --> ReplicaSet Controller maintain the replicaset what we created. It will check any replica is avaialble in the pod if anything availble it will ask and maintain the desire state of the replica.

 --> Self Healing process handle by Replica Controller.

<img width="3438" height="1932" alt="image" src="https://github.com/user-attachments/assets/8597498c-f062-4f03-a064-61b5714d5c10" />


--> To check replica set using below cmd

        kubectl get rs

  <img width="1346" height="850" alt="Screenshot 2025-12-30 at 1 27 52 PM" src="https://github.com/user-attachments/assets/58ec40b8-11b1-466a-9479-4a2e12dad4fe" />

  If we are deleting all the pod also it will be keep 3 parts because we already mention in the yml file above as the replica as 3.

  <img width="1342" height="847" alt="Screenshot 2025-12-30 at 1 29 30 PM" src="https://github.com/user-attachments/assets/a10e3388-6fc4-48b4-b206-d5b7b3a12173" />

  --> If we want to create a replicaset using command we have to use the below command

   <img width="1342" height="847" alt="Screenshot 2025-12-30 at 1 29 30 PM" src="https://github.com/user-attachments/assets/117e3c97-faa1-4028-b20a-c9dabc621b4d" />

 --> We can configure replica in two ways one is declarative way(yml file approach) second one is imperative way(command approach). Best way is the declarative way because if we mention or changed the replica set others also will know about the changes so will be easy to maintain.   

 ### What is the use of ReplicaSet?

   --> A replicaSet ensures a specified number of identical pod replicas are running at all times.

   <img width="1728" height="965" alt="Screenshot 2025-12-31 at 10 29 09 AM" src="https://github.com/user-attachments/assets/0a926838-1dea-44b4-a0f1-77c3c72c35f5" />

   <img width="1723" height="963" alt="Screenshot 2025-12-31 at 10 29 36 AM" src="https://github.com/user-attachments/assets/3bdf31af-f61c-4d86-8272-e1abb532b431" />


--> Whenever we create a POD will be create inside the worker node. Master node will monitor all the POD is working or not inside the worker node. 

<img width="1466" height="970" alt="Screenshot 2025-12-31 at 10 48 47 AM" src="https://github.com/user-attachments/assets/a9c8ee2d-3def-49ed-b41f-9871c0b9ff74" />

### What is Cluster?

   -> It is combination of worker and master node.

   <img width="1447" height="963" alt="Screenshot 2025-12-31 at 10 50 43 AM" src="https://github.com/user-attachments/assets/abd768da-2cca-4fcf-9f51-16275ce2a585" />

### Minikube

  --> Minikube is local kubernetes, focusing on making it easy to learn and develop for kubernetes

  --> If we want to start cluster on local maching need to use the following command

          minikube start

  <img width="850" height="566" alt="Screenshot 2025-12-31 at 11 32 53 AM" src="https://github.com/user-attachments/assets/e7c52240-6cbe-4ef1-8699-8d4ae4024b77" />

  <img width="1550" height="833" alt="Screenshot 2025-12-31 at 11 33 07 AM" src="https://github.com/user-attachments/assets/df77f315-0bf1-4a13-af78-42afdbbea1d1" />

        

 --> Minikube will create worker and master node on the same machine
