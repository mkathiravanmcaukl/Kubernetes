-> Kubernetes is an orchestration tool

### Self Healing

--> If any container crash it will scale up automatically. When the container loading is up it will automatically scaling up and when the container space looks free it will automatically scale down. This is called **Auto Scaling**

--> Kubernetes having two nodes one is master node and another one is slave node

---> Master node having controller manager, API server, ETCD and Scheduler. API server is important role in the master node. Every communication is done through API Server.
