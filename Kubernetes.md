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

<img width="1727" height="967" alt="Screenshot 2025-12-30 at 11 06 33 AM" src="https://github.com/user-attachments/assets/8f75beed-e231-4edc-9e93-dd979437051e" />
