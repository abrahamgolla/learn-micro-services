## Linkerd Service Mesh

#### Why Service Mesh?
  - Safe Service to Service communication
  - Faster Communication
  - Reliable communication
 
**Service mesh is typically implemented as an array of lightweight network proxies that are deployed alongside application code, without the application needing to be aware(But there are variations to this idea, as we’ll see.)

***In the cloud native model, a single application might consist of hundreds of services; each service might have thousands of instances; and each of those instances might be in a constantly-changing state as they are dynamically scheduled by an orchestrator like Kubernetes***

**service mesh abstracts the mechanics of reliably delivering requests between services**

### Features of Service Mesh
**circuit-breaking, latency-aware load balancing, eventually consistent (“advisory”) service discovery, retries, and deadlines**

### History:
Linkerd - 2016, at Kubecon conference

**Who it is for?**
Platform Owners - SRE's, Architects, platform owners in a orgnization
- Developers will be secondary owners
**What are the uses of Linkerd?**
- Oberservability, Reliability, and security (mtls)
**why do we need?**
- Critical for cloud native archs

### Linkerd 1 vs Linkerd2
1 -> Powerfulr, highly configurable, multi-platform (K8s, ECS, Mesos..)
1 -> Ultralight, zero config, K8s first

### Control Plane- Go lang
### Data plane - rust

### Timeline of events when request made through Linkerd
1. It applies dynamic routing rules to determine which service the requestor intended (Prod or to staging, to local or in cloud or to the correct version) 
	Note: these rules are dynamically configurable
2. Having found the correct dest, it retrives coresponding services from a pool.
	Note: If the info diverges from what Linkerd has observed, it makes a decision about which source to trust
3. Then it chooses the dest which returns fast response
4. It sends the request and records the latency and response type of the result
5. If the instance is down or unresponsive, or fails to process the request, it tries make request to the other instabce from the pool (only if the service is idempotent)
6. If an instance is consistently returning errors, it evicts it from the load ba;nacing pool, to be tried later after sometime
7. If the deadline has elapsed, it proactively fails the requests rather than adding load with further retries.
8. Linkerd captures every aspect of the above behavior in the form of metrics and distributed tracing, which are emitted to a centralized metrics system


![Service Mesh](https://buoyant.io/wp-content/uploads/2017/04/linkerd-service-mesh-diagram-1024x587.png)


## Architecture

![Architecture Diagram](https://linkerd.io/images/architecture/control-plane.png)

The **control plane** is a *set of services* that run in a dedicated namespace. These services accomplish various things—*aggregating telemetry data, providing a user-facing API, providing control data to the data plane proxies, etc.* Together, they drive the behavior of the data plane.

The **data plane** consists of transparent proxies that are run next to each service instance. These proxies automatically handle all traffic to and from the service. Because they’re transparent, these proxies act as highly instrumented out-of-process network stacks, sending telemetry to, and receiving control signals from, the control plane.

#### Control Plane

The control plane is made up of:

- Controller
   - Consists of public-api container that provides an API for the CLI and Dashboard to interface with
- Destination
   - Each Proxy in the data plane uses this component to lookup where to send requests
   - Used to fetch service profile information used for per-route metrics, retries and timeouts
- Identity
   - Provides Certificate Authority
   - fectched by proxy on start and must be issued before the proxy becomes ready
   - helps to implemet mTLS
- Proxy Injector
   - The injector is an [admission controller](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/), which receives a webhook request every time a pod is created. This injector inspects resources for a Linkerd-specific annotation (linkerd.io/inject: enabled)
- Service Profile Validator
- Tap
- Web
- Heartbeat
- Grafana
- Prometheus








