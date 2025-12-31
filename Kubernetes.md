--> Kubernetes is an orchestration tool

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

 --> The below command will show worker node and master node on the same machine 

 <img width="1673" height="729" alt="Screenshot 2025-12-31 at 11 37 59 AM" src="https://github.com/user-attachments/assets/8da2b579-7cc7-431e-b40b-6007222dd683" />


## Kubernetes Service:

--> Service will help to communicate between PODS. Without service also we can communicate between PODS but if any POD will crash then kubernetes will do the self healing means to create another POD so that time ip addres will be change so can not able to communicate so that is the reason service will help to communicate the POD. Service having unique ip address that will store in the POD


**There is a scenaio like we have one front end application so this front end application have to communicate back end application and database via service. So how to service knows which pod should it forward the request?**

  -> When we create a service we have use the yml file so in that yml file **selector** section we have to add the label that lable should match with the POD label.

<img width="1724" height="968" alt="Screenshot 2025-12-31 at 11 58 17 AM" src="https://github.com/user-attachments/assets/7ace6ce7-834e-4662-91a2-24542d19bb9c" />


### How does service knows the ip address of the pod?

--> When we create a service that time another component also will be create that is name is called **endpoint**. End point is one of the kubernetes components. 

### What is the use of endpoint?

  --> Endpoint will provide ip address of PODs. It will keep all the POD ip address.

  <img width="1721" height="966" alt="Screenshot 2025-12-31 at 12 03 56 PM" src="https://github.com/user-attachments/assets/3849081d-0735-4de1-a559-77dd606f61a9" />

 --> Service will provide us statble IP address and Endpoint provide us the IP address of the PODS

 <img width="1727" height="969" alt="Screenshot 2025-12-31 at 12 05 23 PM" src="https://github.com/user-attachments/assets/4581fbcb-82e0-4859-8daf-3011ed5a55ae" />


## What is kube-proxy?

--> Kube-proxy runs in all worker nodes. So all the worker node having one kube-proxy. This kube-proxy having one table that stores service IP address and end points.

<img width="1728" height="974" alt="Screenshot 2025-12-31 at 12 09 55 PM" src="https://github.com/user-attachments/assets/f370c18c-0881-4634-af42-dca44f9c45e4" />

<img width="1714" height="956" alt="Screenshot 2025-12-31 at 12 10 13 PM" src="https://github.com/user-attachments/assets/f15661a7-a3b5-4c42-8baf-73d0bca55f23" />

--> If anyone send request to service it will goes to kube-proxy and kube-proxy check with the table of particular ip request and will forward the ip request. 


### Scneario question: 

  --> **Every time pods is crash or delete new pod will create how end points store all the new pod creation ip address?**

   Ans: In the master node we have controller manager it will controll all the components. Controller manager having end point controller this end point controller will check any end point are availble or not, if it is availble it will check the end point selector label and this selector lable will check with all the PODS and matching this lable will update to the end point via controller manager so that end point will save the ip address. This process will keep running frequently so that end point will keep the new ip address of the POD.

<img width="1720" height="963" alt="Screenshot 2025-12-31 at 12 21 04 PM" src="https://github.com/user-attachments/assets/677fff6d-1c75-4fab-9e6c-c8695055b688" />

### Why do we need a service while pod has its own ip for communcation?

  --> POD is Ephemeral because it is not stable. So that we are using service so service having stable ip address and act as a load balancer. 

### How does a service know which pod to forward the traffic to?

--> While creating a service via yml file we have selector section and this label field will be there that label field will match with POD

         selector:
            app: backend

 ### What is the role of kube-proxy in kubernetes networking?

   --> Kube proxy runs on every node. It manages iptables on every nodes. When a request comes to a service IP, kube-proxy forward it to one of the backend POD IPs, doing load balancing.

 ### What is an Endpoint in Kubernetes, and how is it managed?

   --> An EndPoint is a kubernetes object that maps a service to its actual POD IPs. It is automatically updated by the EndPoint Controller 


## Type of Services:

  **1. Cluster IP**: It will be useful we need to communicate within the cluster. This service only accessible within the cluster only not outside the cluster. 

  <img width="1465" height="957" alt="Screenshot 2025-12-31 at 12 45 27 PM" src="https://github.com/user-attachments/assets/61be757f-2836-489b-959e-3411d6e46720" />

    --> We will set cluter IP address so that we can access the service inside the cluster only. 

    <img width="975" height="707" alt="Screenshot 2025-12-31 at 12 51 51 PM" src="https://github.com/user-attachments/assets/5e217319-3f53-4636-b6c3-91f3a88222e6" />

    --> In the above attached screenshot we have ports section it has two ports . The first one is the service port the second one is target port(means POD port). For example front end POD application access to the backend POD application we need to call the backend POD application service so we need to do two things when we calling i) IP address or Service name ii) Service port.

    <img width="1482" height="936" alt="Screenshot 2025-12-31 at 12 56 43 PM" src="https://github.com/user-attachments/assets/b605f606-a7be-4223-8d5c-22c7085ef905" />

    --> This cluster ip is the default type of service. When we create a service in the yml file if we not mention any type then it will consider as cluster ip address.


 **2. Node Port**: When we create a node port we have to mention 3 ports one is service port, target port and node port.

 <img width="1482" height="936" alt="Screenshot 2025-12-31 at 12 56 43 PM" src="https://github.com/user-attachments/assets/35cb4a1b-7da5-4a16-ad30-3cc84a9982e5" />

 --> It opens a port on all nodes in the cluster. If some want to access from outside to service they have to use the node-ip: node port. Most important thing is this node port only use for testing only not for production.Because we are opening a port in every node so this is not a safe approach.

 --> Node port number should be given the range between 30000 - 32767

**3. Headless Service** : When the service want to send the request using load balancer for particuluar POD we have to set the cluster as none.

<img width="1432" height="970" alt="Screenshot 2025-12-31 at 2 20 45 PM" src="https://github.com/user-attachments/assets/c35966ac-061b-4caa-ab0a-c370bb94ce28" />

**4. External Name**: When we want to access anything outside from the cluster we have to use this service. For example if i want to access the weather api that is not inside the cluster it is in outside cluster but want to access means we have to use the External name.

<img width="1691" height="832" alt="Screenshot 2025-12-31 at 2 24 42 PM" src="https://github.com/user-attachments/assets/ad5ff573-e35d-4f30-9c45-527d884d422d" />

<img width="1337" height="914" alt="Screenshot 2025-12-31 at 2 24 52 PM" src="https://github.com/user-attachments/assets/981832e5-bdf8-4d7b-8484-1fa5dd909716" />


## Kubernetes Deployment

--> When we to upgrade application 1.0 to 2.o then delete the old pod and create the new pod using replica set facing downtime problem(means while creating new POD takes sometimes so that time user can not able to access the application it returns 404) even if we create a new POD and we are able to access the application but some flows are breaking means again we want to rollback to previous version 1.0 we have to set in the replicaset. So for this issue only we are solving using **deployment**.

--> So hereafter we have create POD using deployment so it will create replica set and pod and it will solve the rolling updates.

<img width="1728" height="943" alt="Screenshot 2025-12-31 at 2 38 35 PM" src="https://github.com/user-attachments/assets/6b39cc81-a4db-4172-b446-444a9c7e7c7f" />

### How does deployment fix both downtime problem?

 --> Using Rolling Update Strategy. In this scenario when the new update is coming it will create new POD and will delete the old POD. So this process will continue until the batch update so **zero downtime**

 --> A Deployment maintains a history of changes that occur at the Pod level.

 --> Create a deployment using replica set as below

  <img width="1482" height="793" alt="Screenshot 2025-12-31 at 2 54 04 PM" src="https://github.com/user-attachments/assets/1c1100f9-a012-436f-aeee-183f2eef750c" />


 <img width="1489" height="796" alt="Screenshot 2025-12-31 at 3 01 20 PM" src="https://github.com/user-attachments/assets/39fd69e9-a0d6-4d18-9ae5-494932ad2f68" />

 <img width="1537" height="793" alt="Screenshot 2025-12-31 at 3 02 05 PM" src="https://github.com/user-attachments/assets/049cbf82-c0eb-46cf-8751-dd7c8f800c1c" />

 The above screen shot container is creating once the container is created we have to check as below

 <img width="799" height="332" alt="Screenshot 2025-12-31 at 3 04 11 PM" src="https://github.com/user-attachments/assets/21b1cb68-202e-438e-a999-48c53f9d82df" />



 --> In the attached screenshot in the **template section lables** whatever we mention that same thing we have to mention in the **selector matching labels**.

      kubectl get services

--> The above command will list of all the services but suppose we want to use particular service means we need url so we have to use the following command

      minikube service calculator-app-service --url

<img width="1001" height="313" alt="Screenshot 2025-12-31 at 3 09 41 PM" src="https://github.com/user-attachments/assets/7b662bfb-a3e0-448a-aff5-5a1a2706ee08" />
      
