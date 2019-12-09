# Microservices

### Config Server
- To keep properties files are centralized location
- Can be version controlled
- Changes will be automatically pushed to all microservices without restarting
- Should not be a SPF (Single point of failure)

### Eureka Discovery Server
- Containers have dynamic IP addresses as they are spun on a fly, so it tracks all instances of a service
- if a service is removed it removes the service from registry
- A service contacts the discover server to get the details of the other service it want to contact
- Should not be a SPF (Single point of failure)

### Services
- Contains main business logic or a feature set

### Gateway service
- Used for Authentication or for security checks for each API calls made from the client
- It delegates the calls to the microservices

#### Micoservices example scenario
Here we are using a sample movie catalog example, where user will get ratings of the movies he watched.

So we have below microservices
- Movie Info Service - Contains the description of the movie
- Ratings Data Service - Contains the user ratings of a movie
- Movie Catalog Service - Mashes the data from the above two services and sends it to the client


https://start.spring.io/ is used to generate the projects

### 1. Config Server
- Choose  ***Config server*** dependency
- As an option add ***Actuator Dependency***, which returns the health check and different results of application state using a REST API


### Istio Service Mesh



#### What is Service Mesh and its features?
- Used for describing network of microservices and helps interaction between them
##### features
- Service Discovery
- Load balancing
- failure recovery
- metrics
- monitoring
- A/B testing (Split testing)
- Canary Rollouts
- rate limiting
- access control
- end to end authentication

#### Istio
- Istio provides behavioral insights and operational control over the service mesh as a whole
- Provides solutions to the challenges faced during transition of an app from monolith to distributed microservice architecture 
- makes it easy to create a network of deployed services with load balancing, service-to-service authentication, monitoring, and more
##### Control Plane
- Automatic load balancing for HTTP, gRPC, WebSocket, and TCP traffic.
- Fine-grained control of traffic behavior with rich routing rules, retries, failovers, and fault injection.
- A pluggable policy layer and configuration API supporting access controls, rate limits and quotas.
- Automatic metrics, logs, and traces for all traffic within a cluster, including cluster ingress and egress.
- Secure service-to-service communication in a cluster with strong identity-based authentication and authorization.

### Core Features
#### Traffic Management
- circuit breakers,timeouts ,retries
- A/B testing, canary rollouts, and staged rollouts with percentage-based traffic splits.

#### Security
- manages authentication, authorization, and encryption of service communication at scale.

#### Policies
- Rate limiting to dynamically limit the traffic to a service
- Denials, whitelists, and blacklists, to restrict access to services
- Header rewrites and redirects
- Custom policies

#### Observability
- Istio’s robust tracing, monitoring, and logging features give you deep insights into your service mesh deployment
- custom dashboards provide visibility into the performance of all your services
- Istio’s Mixer component is responsible for policy controls and telemetry collection

## Kubernetes
- Kubernetes coordinates a highly available cluster of computers that are connected to work as a single unit
- Kubernetes automates the distribution and scheduling of application containers across a cluster in a more efficient way
   - A Kubernetes cluster consists of two types of resources:
        - The **Master** coordinates the cluster
        - **Nodes** are the workers that run the application

![Cluster Diagram](https://d33wubrfki0l68.cloudfront.net/99d9808dcbf2880a996ed50d308a186b5900cec9/40b94/docs/tutorials/kubernetes-basics/public/images/module_01_cluster.svg)

- **Master** is responsible for managing the cluster, It helps in
   - Scheduling Applications
   - Maintaining Applications desired state
   - Scaling applications
   - Rolling out new updates
   - When you deploy applications on Kubernetes, you tell the master to start the application containers. The master schedules the containers to run on the cluster's nodes. 
- **node** is a VM or a physical machine that serves as a worker machine in K8s cluster
  - Each node has a kublet, which is an agent for managing the node and communicating with the master
  - A node should have tools for handling container operations, such as Docker or rkt
  - The nodes communicate with the master using the Kubernetes API
  
***A Kubernetes cluster that handles production traffic should have a minimum of three nodes***

### Kubernetes Cluster Components
- **Pods
- **Nodes

#### Pods
- A Pod is a kubernetes abstraction that represents a group of one or more application containers and some shared resources for those containers
   - Resources Include
      - Shared storage, as Volumes
      - Networking, as a unique cluster IP address
      - Information about how to run each container, such as the container image version or specific ports to use
- A Pod models an application-specific "logical host" and can contain different application containers which are relatively tightly coupled.
- Pods are the atomic unit on the Kubernetes platform
![Pods Diagram](https://d33wubrfki0l68.cloudfront.net/fe03f68d8ede9815184852ca2a4fd30325e5d15a/98064/docs/tutorials/kubernetes-basics/public/images/module_03_pods.svg)

#### Nodes
- A Pod always runs on a **node**. A ***Node*** is a worker machine in Kubernetes and may be either a virtual or a physical machine
- Nodes are managed by master
  - Kubernetes Node runs at least
    - Kubelet (a process responsible for communication between the Kubernetes Master and the Node)
    - A Container runtime (responsible for pulling, unpacking and running)
    
![Node Image](https://d33wubrfki0l68.cloudfront.net/5cb72d407cbe2755e581b6de757e0d81760d5b86/a9df9/docs/tutorials/kubernetes-basics/public/images/module_03_nodes.svg)

#### Services in Kubernertes
- A Service in Kubernetes is an abstraction which defines a logical set of Pods and a policy by which to access them
- Services enable a loose coupling between dependent Pods. Although each Pod has a unique IP address, those IPs are not exposed outside the cluster without a Service.
- Services allow your applications to receive traffic.
- Services can be exposed in different ways by specifying a ***type*** in the ServiceSpec:
   - ClusterIP (makes the Service only reachable from within the cluster)
   - NodePort (Exposes the Service on the same port of each selected Node in the cluster using NAT)
   - LoadBalancer (Creates an external load balancer in the current cloud)
   - ExternalName (Exposes the Service using an arbitrary name (specified by externalName in the spec) by returning a CNAME record with the name. No proxy is used)

![service_image](https://d33wubrfki0l68.cloudfront.net/cc38b0f3c0fd94e66495e3a4198f2096cdecd3d5/ace10/docs/tutorials/kubernetes-basics/public/images/module_04_services.svg)

- Services are the abstraction that allow pods to die and replicate in Kubernetes without impacting your application.
- Discovery and routing among dependent Pods (such as the frontend and backend components in an application) is handled by Kubernetes Services.
