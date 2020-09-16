# Microservices: Design Patterns

## Microservices:
- Smaller scoped units of work
- Focus on data, business, or function domains
- Not monolithic service artifacts

## Service Types:
- Data service: Connects to data source.
- Business service: Higher level of abstraction built over data service.
- Translation service: is any abstraction on third party operation that we may need to encapsulate.
- Edge service: Responsible for servicing data to user or external services.

## Platform:
- Runtime for services
- Ancillary services
- Operational components
- Diagnostic components

## Cloud Native
- Architectural style
- Designed to facilitate operating in the cloud
- Focuses on portable and scalable applications
- Can be run in single datacenter

## Why Cloud Native & Microservices Go Together:
- Scalability
- Can run one without the other 
- Distinct concepts, often considered the same

## 1. Decomposition Patterns:

### Functional Use Patterns:
- Domain based
- Business process based
- Atomic transaction based

### Decomposition Strategies:
- Strangler pattern
- Sidecar pattern

### Domain Based Microservices:

#### Data Domains:
- Driven by the data domain model itself
- Undelying schema "unimportant"
- Focus on data patterns

#### Data Domain Design:
- Domain-driven design
- Start with the model, not the datastore
- Evaluate actions
- Build the service, contract first

### Business Process-Based Microservices:

#### Business Process Domains:
- Provide higher-level business functionality
- Allow us to encapsulate related domains
- No datasource access
- Distinct functional uses

#### Business Process Domain Design:
- Identify process
- Identify domains
- Define API
- Wire service

### Atomic Transaction-Based Microservices:
- Gurantee atomicity, consistency, isolation, durability (ACID) transactions across domains.
- Provide failure domains and rollbacks
- Force blocking until commit
- Don't use distributes transactions

#### Designing Atomic Services:
- Ensure we must have the atomic service
- Domains must be in shared database
- Clearly get the transaction defined, including rollback conditions
- Implement the service as normal, with fast fail and rollback

### Strangler Pattern:
- Break a monolith up by "strangling" the dependency on it.
- Can be top down.
- Can be bottom up.
- Essentially carving out functionality.

### Sidecar Pattern:
- Determine the process
- Build the sidecar
- Schedule it to deploy with the appropriate services
- Functionality appears without embedding it

## 2. Integration Patterns:

### Gateway/ API Gateway Pattern:
- Problem: Client ability to call any service can create chaos
- Gateway provides a facade/proxy
- Single layer that proxies, mutates or limits call
- Can become a single point of failure

#### Mutation Behaviors:
- Can simply proxy
- Can decorate
- Can aggregate
- Can limit access
- Movement Buffer

#### Strategy:
- Define Contracts
- Expose APIs for those contracts, client focused
- Adhere to strict version control and passive changes only
- Implement the gateway to call our services and our clients to call the gateway

### Process Aggregator Pattern:
- Problem: We have serveral business processes that must be called together and have a composite payload.
- Aggregator provides clients a single API to call 
- Can introduce its own process logic
- Can cause long blocking calls

#### Aggregator Design:
- Determines the business process
- Determines the processing rules
- Design a consolidated model
- Design an API for the actions on that model
- Wire the service and implement the integral processing


### Edge Pattern:
- Problem: Client use varies by platform and scaling a gateway presents wasted resources or clients need special business logic.
- Client-specific (Mobile, Web, etc.  ) "gateways".
- Focus on isolating calls for client systems.

#### Edge Design:
- Identify client
- Build contracts
- Implement contracts
- Maintain passivity as long as client is needed

### Gateway vs. Edge:
- Similar but different
- Edge targets clients
- Edge is more scalable
- Edge is more flexible for new clients
- Gateway has less moving points

## 3. Data Patterns:

### Single Service Database Pattern (Single Service, Single Database):
- Problem: Scalability needs between database and service are related.
- Each service implementation gets its own datastore
- Datastore distributes with the service
- Datastore scales proportionally to the service

### Shared Service Database Pattern:
- All data domains exist within a single database
- Data distribution should be handled by the database
- Break data domains into schemas or similar constructs
- User don't span schemas
- Data Domains connect to single schema

### Command Query Responsibility Segregation (CQRS) Pattern:

#### What is CQRS?
- Multi-model bounded contexts
- Multi-interface operations, write versus read
- Divergence from simple CRUD
- Dramatically increases complexity

#### When does CQRS make sense?
- Task-based UI operations
- Eventual consistency is a must
- Event-based models

### Asynchronous Eventing Pattern:
- Problem: Some processes cannot be done in real time
- Service API to trigger event
- Event can cascade asynchronously from API
- Event can trigger from messaging
- Very powerful in distributed systems

## 4. Operational Patterns:

### Log Aggregation Pattern:

#### Logging:
- Problem: We need to know what is going on?
- Logging is invaluable in operations.
- Logging must be consistent.
- Logging must be structured.
- Logging must share a taxonomy.

#### Log Aggregation:
- Problem: Logs are everywhere
- Aggregation of logs
- Parsing of logs
- Correlating of logs
- Indexing of logs

### Metrics Aggregation Patterns:
- Problem: Need to see what is going on with the system
- Taxonomy
- Standard libraries
- Metrics shipping
- Dashboards

#### Get All Metrices:
- Build high-level dashboards
- Build detailed dashboards
- Inject events, especially deployments
- Trace alarms on our graphs
- Ensure we have runbooks for all alarms

### Tracing Patterns:

#### Tracing:
- Problem: Call stacks span processes, so code traces are less valuable
- Tracing gives us a way to recreate the call stack 
- Should span from the edge to the database
- No call is lost

#### How to implement Tracing?
- Use standard-based approaches
- Inject the entry point to our system 
- Every log message should embed the trace ID through structure logging with common taxonomy.
- Leverage tracing tools and application performance management (APM) to visualize

### External Configuration Pattern:

#### Externalized Config:
- Use consistent tooling
- Use consistent naming
- Err on the side of externalization
- Protect secrets

#### How to use Externalized Config:
- Config is injected or retrieved
- Application utilizes externalized value in favor of embedded values; however, defaults can be useful
- Common libraries or tooling helps
- Read, config, and act.


### Service Discovery Pattern:
- Problem: What service do I call?
- Central location of all services
- Advertise what they offer 
- Find what we need
- Consume the URI from the discovery engine, not config

