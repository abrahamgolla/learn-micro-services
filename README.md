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





