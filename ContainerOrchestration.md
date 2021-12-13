**Container orchestrators** are tools which group systems together to form clusters where containers' deployment and management is automated at scale while meeting the requirements mentioned above.



##### **Common Container Orchestration Solutions**

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

- - - Group hosts together while creating a cluster
    - Schedule containers to run on hosts in the cluster based on resources availability
    - Enable containers in a cluster to communicate with each other regardless of the host they are deployed to in the cluster
    - Bind containers and storage resources
    - Group sets of similar containers and bind them to load-balancing constructs to simplify access to containerized applications by creating a level of abstraction between the containers and the user
    - Manage and optimize resource usage
    - Allow for implementation of policies to secure access to applications running inside containers.

