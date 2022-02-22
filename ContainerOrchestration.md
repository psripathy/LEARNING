**Container orchestrators** are tools which group systems together to form clusters where containers' deployment and management is automated at scale while meeting the requirements mentioned above.



#### **Common Container Orchestration Solutions**

- **Amazon Elastic Container Service**
  Amazon Elastic Container Service](https://aws.amazon.com/ecs/) (ECS) is a hosted service provided by [Amazon Web Services](https://aws.amazon.com/) (AWS) to run Docker containers at scale on its infrastructure.

- **Azure Container Instances**
  [Azure Container Instance](https://azure.microsoft.com/en-us/services/container-instances/) (ACI) is a basic container orchestration service provided by [Microsoft Azure](https://azure.microsoft.com/en-us/).

- **Azure Service Fabric**
  [Azure Service Fabric](https://azure.microsoft.com/en-us/services/service-fabric/) is an open source container orchestrator provided by [Microsoft Azure](https://azure.microsoft.com/en-us/).

- **Kubernetes**
  [Kubernetes](https://kubernetes.io/) is an open source orchestration tool, originally started by Google, today part of the [Cloud Native Computing Foundation](https://www.cncf.io/) (CNCF) project.

- **Marathon**
  [Marathon](https://mesosphere.github.io/marathon/) is a framework to run containers at scale on [Apache Mesos](https://mesos.apache.org/).

- **Nomad**
  [Nomad](https://www.nomadproject.io/) is the container and workload orchestrator provided by [HashiCorp](https://www.hashicorp.com/).

- **Docker Swarm**
  [Docker Swarm](https://docs.docker.com/engine/swarm/) is a container orchestrator provided by [Docker, Inc](https://www.docker.com/). It is part of [Docker Engine](https://docs.docker.com/engine/).


Most container orchestrators can:

    - Group hosts together while creating a cluster
    - Schedule containers to run on hosts in the cluster based on resources availability
    - Enable containers in a cluster to communicate with each other regardless of the host they are deployed to in the cluster
    - Bind containers and storage resources
    - Group sets of similar containers and bind them to load-balancing constructs to simplify access to containerized applications by creating a level of abstraction between the containers and the user
    - Manage and optimize resource usage
    - Allow for implementation of policies to secure access to applications running inside containers.


### Kubernetes
[Learn Kubernetes Basics | Kubernetes](https://kubernetes.io/docs/tutorials/kubernetes-basics/)
[Kubernetes Architecture | Chapter 4. Kubernetes Architecture | Introduction to Kubernetes | edX](https://learning.edx.org/course/course-v1:LinuxFoundationX+LFS158x+3T2020/block-v1:LinuxFoundationX+LFS158x+3T2020+type@sequential+block@f0d11db04aff45479f54a3075d2286c1/block-v1:LinuxFoundationX+LFS158x+3T2020+type@vertical+block@333baddf87994bbaa5e92a0583409fe3)

#### Kubernetes Architecture

At a very high level, Kubernetes has the following main components:

-   One or more  **master nodes**, which is part of the  **control plane**
-   One or more  **worker nodes**.
![Components of Kubernetes Architecture](https://courses.edx.org/assets/courseware/v1/51120ad23b216a6946e3c4ebef2106bf/asset-v1:LinuxFoundationX+LFS158x+3T2020+type@asset+block/arch-1.19-components-of-kubernetes.svg)


-   The **master node** provides a running environment for the **control plane** responsible for managing the state of a Kubernetes cluster, and it is the brain behind all operations inside the cluster. The Kubernetes control plane automatically handles scheduling the pods across the Nodes in the cluster. In order to communicate with the Kubernetes cluster, users send requests to the control plane via a Command Line Interface (CLI) tool, a Web User-Interface (Web UI) Dashboard, or Application Programming Interface (API).

> A master node runs the following control plane components:
>> -   **API Server** - The **`kube-apiserver`** intercepts RESTful calls from users, operators and external agents, then validates and processes them.  It is the only master plane component to talk to the etcd datastore to read/write Kubernetes cluster state
>> -   **Scheduler** - The **`kube-scheduler`** assigns workload objects such as pods to nodes. Scheduling decisions are made based on cluster state and new objects requirements by obtaining information from etcd data store using API server
>> -   **Controller Managers**
	> **`kube-controller-manager`** - responsible to act when nodes become unavailable, ensure pods count are as expected, to create endpoints, service accounts and API access tokens
	> **`cloud-controller-manager`** - responsible to interact with underlying infrastructure of cloud provider, when nodes become unavailable, manage storage volumes, load balancing and routing.
>> -   **Data Store** - **`etcd`** is a strongly consistent, distributed key-value store used to persist cluster state related data. Only API server can talk to etcd. etcd can be configured on the same master node (stacked topology) or on its dedicated host (external topology). etcd's client management CLI, **`etcdctl`** provides backup, snapshot and restore capabilities. 

> In addition, the master and the worker nodes run:
>> -   **Container Runtime** - Kubernetes requires container runtime (like Docker or containerd) on the node where pods and it's containers are scheduled
>> -   **Node Agent** - The **`kubelet`** is an agent running on each node and communicates with control plane components and receives pod definitions from API server and interacts with the container runtime to run the pods associated with the containers associated with the pod. It also monitors health and resources of the pods running the containers  
>> -   **Proxy** -  The **`kube-proxy`** is a network agent that runs on each node responsible for dynamic update and maintenance of all networking rules on the node.
>> - **Add-Ons** - Are cluster features not available in Kubernetes but implemented through external pods & services
	> **`DNS`** - cluster DNS is a DNS server required to assign DNS records to Kubernetes resources & objects
	> **`Dashboard`** - web UI for cluster management.
	> **`Monitoring`** - collects container level metrics and saves them to central data store
	> **`Logging`** - collects cluster level container logs and saves them to central log store.
	
- To persist the Kubernetes cluster's state, all cluster configuration data is saved to [etcd](https://etcd.io/). **`etcd`** is a distributed key-value store which only holds cluster state related data, no client workload data. etcd may be configured on the master node ([stacked](https://kubernetes.io/docs/setup/independent/ha-topology/#stacked-etcd-topology) topology), or on its dedicated host ([external](https://kubernetes.io/docs/setup/independent/ha-topology/#external-etcd-topology) topology) to help reduce the chances of data store loss by decoupling it from the other control plane agents.
    
-   **Node(s)** or worker node is a VM or physical computer that serves a worker machine in a Kubernetes cluster. Each node has Kubelet, which is an agent for managing the node and communicating with the Kubernetes control plane. The node should also have tools for handling container operations, such as containerd or Docker.
    ![](https://d33wubrfki0l68.cloudfront.net/5cb72d407cbe2755e581b6de757e0d81760d5b86/a9df9/docs/tutorials/kubernetes-basics/public/images/module_03_nodes.svg)
- In a multi worker Kubernetes cluster, the network traffic between client users and containerized app deployed in pods are handled directly by worker nodes and not routed through master node. The nodes communicate with the control plane using the  [Kubernetes API](https://kubernetes.io/docs/concepts/overview/kubernetes-api/), which the control plane exposes

#### API Directory Tree of Kubernetes
![API Server Space](https://courses.edx.org/assets/courseware/v1/7ebcb514203a3af89dc1599625779c1f/asset-v1:LinuxFoundationX+LFS158x+3T2020+type@asset+block/api-server-space_.jpg)

#### Kubernetes Installation Tools/Resources

- **kubeadm** - Bootstrap single node or multi-node production ready High Availability(HA) Kubernetes cluster on-prem or in the cloud
- **kubespray** - Based on Ansible. Can install multi node HA Kubernetes cluster on AWS, Azure or bare metal
- **kops** - Create, upgrade and maintain HA cluster from command line. Can also provision machines. Currently supports AWS.
- **kube-aws** - Create, upgrade & destroy Kubernetes cluster on AWS from the command line

For manual installation approach, the _[Kubernetes The Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way)_ GitHub project by [Kelsey Hightower](https://twitter.com/kelseyhightower) is extremely helpful.

#### Kubernetes Object Model

Kubernetes Object Model refers to different persistent entities in the Kubernetes cluster. These entities describe
- What containerized apps we are running
- The nodes where the containerized apps are deployed
- Application resource consumption
- Policies attached to applications, like restart/upgrade policies, fault tolerance etc.

 Examples of Kubernetes objects are: **`Pods, Replica-sets, Deployments, Namespaces, Service`** etc.

With each object, we declare our intent, or the desired state of the object, in the `spec` section. The Kubernetes system manages the `status` section for objects, where it records the actual state of the object. At any given point in time, the Kubernetes Control Plane tries to match the object's actual state to the object's desired state.

A **Pod** is the smallest and simplest Kubernetes Object. It is a unit of Deployment in Kubernetes, which represents a single instance of the application. It is a logical collection of one or more application containers (such as Docker), and some shared resources for those containers. Those resources include:
> - Shared storage, as Volumes
> - Networking, as a unique cluster IP address
> - Information about how to run each container, such as the container image version or specific ports to use

A Pod always runs on a Node. Pods that are running inside Kubernetes are running on a private, isolated network and are controlled by the cluster control plane running on the master node. Each Pod in a Kubernetes cluster has a unique IP address, even Pods on the same Node. By default they are visible from other pods and services within the same Kubernetes cluster, but not outside that network. 

 **Labels** are key-value pairs attached to Kubernetes objects. Labels are used to organize and select subset of objects.
![](https://courses.edx.org/assets/courseware/v1/6669997d43534cbd2f251a57ebe0587c/asset-v1:LinuxFoundationX+LFS158x+3T2020+type@asset+block/Labels.png)
2 types of Label Selectors: 
- Equality based selectors - allows filtering based on label key and value. ex. `env==dev or env=dev` 
- Set based selectors - allows filtering based on set of values. You can use `in, not in` for label values & `exist, does not exist` for Label Keys ex. `env in (dev, qa)`

**ReplicaSet** is the replication controller that ensures the availability of the replicas and ensures the current state always matches desired state

A **Deployment** object provides declarative updates to Pods and Replicasets.

**Namespaces** - If multiple teams and users use the same kubernetes cluster we can partition the cluster into virtual sub-clusters using Namespaces. The names of the resources/objects created inside a Namespace are unique, but not across Namespaces in the cluster. Kubernetes creates four Namespaces out of the box: `kube-system, kube-public, kube-node-lease, and default`

A **Service** in Kubernetes is an abstraction which defines a logical set of Pods and a policy by which to access them.   
A Service routes traffic across a set of Pods. A Service is defined using YAML [(preferred)](https://kubernetes.io/docs/concepts/configuration/overview/#general-configuration-tips) or JSON, like all Kubernetes objects.

Although each Pod has a unique IP address, those IPs are not exposed outside the cluster without a Service. Services allow your applications to receive traffic. Services can be exposed in different ways by specifying a  `type`  in the ServiceSpec:

-   **ClusterIP**  (default) - Exposes the Service on an internal IP in the cluster. This type makes the Service only reachable from within the cluster.
-   **NodePort**  - Exposes the Service on the same port of each selected Node in the cluster using NAT. Makes a Service accessible from outside the cluster using  `<NodeIP>:<NodePort>`. Superset of ClusterIP.
-   **LoadBalancer**  - Creates an external load balancer in the current cloud (if supported) and assigns a fixed, external IP to the Service. Superset of NodePort.
-   **ExternalName**  - Maps the Service to the contents of the  `externalName`  field (e.g.  `foo.bar.example.com`), by returning a  `CNAME`  record with its value. No proxying of any kind is set up. This type requires v1.7 or higher of  `kube-dns`, or CoreDNS version 0.0.8 or higher.

Additionally, note that there are some use cases with Services that involve not defining `selector` in the spec. A Service created without `selector` will also not create the corresponding Endpoints object. This allows users to manually map a Service to specific endpoints. Another possibility why there may be no selector is you are strictly using `type: ExternalName`.

Services match a set of Pods using  [labels and selectors](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels), a grouping primitive that allows logical operation on objects in Kubernetes. Labels are key/value pairs attached to objects and can be used in any number of ways:

-   Designate objects for development, test, and production
-   Embed version tags
-   Classify an object using tags

![](https://d33wubrfki0l68.cloudfront.net/7a13fe12acc9ea0728460c482c67e0eb31ff5303/2c8a7/docs/tutorials/kubernetes-basics/public/images/module_04_labels.svg)

     - kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080
     - kubectl describe deployment
     - kubectl get pods -l app=kubernetes-bootcamp (-l is param for label) 
     - kubectl get services -l app=kubernetes-bootcamp

#### Kubernetes Commands

**`kubectl`** is the Kubernetes CLI to manage  cluster resources and applications. When we use  `kubectl`, we're interacting through an API endpoint to communicate with our application.

- `kubectl config view` - View connection details to connect to master node. The connection setup can be found under ~/.kube/config
- `kubectl cluster-info`
- `kubectl get nodes` - Command takes the format kubectl *action* *resource* 
- `kubectl create deployment` (ex. `kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1`)
- `kubectl get deployments`
- `kubectl proxy` - command can create a proxy that will forward communications into the cluster-wide, private network. The proxy can be terminated by pressing control-C and won't show any output while its running.
- A Service is required to access the deployments/pods without proxy.
- `kubectl get pods` - The API server will automatically create an endpoint for each pod, based on the pod name, that is also accessible through the proxy.
- `kubectl get`  - list resources
- `kubectl describe`  - show detailed information about a resource
- `kubectl logs`  - print the logs from a container in a pod
- `kubectl exec`  - execute a command on a container in a pod

We can execute commands directly on the container once the Pod is up and running. For this, we use the `exec` command and use the name of the Pod as a parameter. Let’s list the environment variables:
> `kubectl exec $POD_NAME -- env`
> `kubectl exec -ti $POD_NAME -- bash` - Opens a console on the container.

#### Scaling

Scaling is accomplished by changing the number of replicas in a Deployment. Scaling out a Deployment will ensure new Pods are created and scheduled to Nodes with available resources. Scaling will increase the number of Pods to the new desired state.

Running multiple instances of an application will require a way to distribute the traffic to all of them. Services have an integrated load-balancer that will distribute network traffic to all Pods of an exposed Deployment. Services will monitor continuously the running Pods using endpoints, to ensure the traffic is sent only to available Pods.

    - kubectl scale deployments/kubernetes-bootcamp --replicas=4
    - kubectl get pods -o wide (gets the pods)
    - kubectl get rs (Gets replica set)

#### Rolling Update

Rolling updates allow Deployments update to take place with zero downtime by incrementally updating Pods instances with new ones. Rolling updates allow the following actions:

-   Promote an application from one environment to another (via container image updates)
-   Rollback to previous versions
-   Continuous Integration and Continuous Delivery of applications with zero downtime

![](https://d33wubrfki0l68.cloudfront.net/30f75140a581110443397192d70a4cdb37df7bfc/fa906/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates1.svg)![](https://d33wubrfki0l68.cloudfront.net/678bcc3281bfcc588e87c73ffdc73c7a8380aca9/703a2/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates2.svg)![](https://d33wubrfki0l68.cloudfront.net/9b57c000ea41aca21842da9e1d596cf22f1b9561/91786/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates3.svg)![](https://d33wubrfki0l68.cloudfront.net/6d8bc1ebb4dc67051242bc828d3ae849dbeedb93/fbfa8/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates4.svg)

Rolling update is triggered when we update specific properties of a Pod Template for a Deployment. While updating the container image, container port, volumes and mounts would trigger a new revision, other operations like scaling & labeling the deployment do not trigger a new rolling update, thus do not change revision number. 

In time, we need to push updates to the application managed by the Deployment object. Let's change the Pods' Template and update the container image from **nginx:1.7.9** to **nginx:1.9.1**. The **Deployment** triggers a new **ReplicaSet B** for the new container image versioned **1.9.1** and this association represents a new recorded state of the **Deployment**, **Revision 2**. The seamless transition between the two ReplicaSets, from **ReplicaSet A** with 3 Pods versioned **1.7.9** to the new **ReplicaSet B** with 3 new Pods versioned **1.9.1**, or from **Revision 1** to **Revision 2**, is a Deployment **rolling update**.
![Deployment - update](https://courses.edx.org/assets/courseware/v1/979a990d505485a3ad502836ca5f1078/asset-v1:LinuxFoundationX+LFS158x+3T2020+type@asset+block/ReplikaSet_B.png)
Once ReplicaSet B and its 3 Pods versioned 1.9.1 are ready, the Deployment starts actively managing them. However, the Deployment keeps its prior configuration states saved as Revisions which play a key factor in the rollback capability of the Deployment - returning to a prior known configuration state. In our example, if the performance of the new nginx:1.9.1 is not satisfactory, the Deployment can be rolled back to a prior Revision, in this case from Revision 2 back to Revision 1 running nginx:1.7.9 once again.

The command below notifies the Deployment to use a different image for your app and initiates a rolling update.
    - `kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2`
    - `kubectl rollout status deployments/kubernetes-bootcamp`
To roll back the deployment to your last working version, use
    - `kubectl rollout undo deployments/kubernetes-bootcamp`

The rolling updates and rollbacks are not just limited to deployments but can also be applied to other controllers like DaemonSets & StatefulSets
