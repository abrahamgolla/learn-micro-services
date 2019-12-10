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

### Linkerd Features
- Linkerd applies dynamic routing rules to determine which service the requester intended
    - routed to a service in production or in staging?
    - service in a local datacenter or one in the cloud?
    - To the most recent version of a service that’s being tested or to an older one that’s been vetted in production?
- Linkerd validates the service with the information it has and makes the service call
    - If this information diverges from what Linkerd has observed in practice, Linkerd makes a decision about which source of information to trust.
- Linkerd chooses the instance most likely to return a fast response based on a variety of factors, including its observed latency for recent requests
- Linkerd chooses the instance most likely to return a fast response based on a variety of factors, including its observed latency for recent requests
- If the instance is down, unresponsive, or fails to process the request, Linkerd retries the request on another instance (but only if it knows the request is idempotent).
- 
