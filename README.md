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

## Service Discovery:
- Problem: What service do I call?
- Central location of all services
- Advertise what they offer 
- Find what we need
- Consume the URI from the discovery engine, not config

## Logging:
- Problem: We need to know what is going on?
- Logging is invaluable in operations.
- Logging must be consistent.
- Logging must be structured.
- Logging must share a taxonomy.

## Edge Design:
- Identify client
- Build contracts
- Implement contracts
- Maintain passivity as long as client is needed

## Business Process Domain:
- Provide higher-level business functionality
- Allow us to encapsulate related domains
- No datasource access
- Distinct functional uses

## Process Aggregator:
- Problem: We have serveral business processes that must be called together and have a composite payload.
- Aggregator provides clients a single API to call 
- Can introduce its own process logic
- Can cause long blocking calls

## Single Service, Single Database:
- Problem: Scalability needs between database and service are related.
- Each service implementation gets its own datastore
- Datastore distributes with the service
- Datastore scales proportionally to the service

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

## 2. Gateway/ API Gateway Pattern:
- Problem: Client ability to call any service can create chaos
- Gateway provides a facade/proxy
- Single layer that proxies, mutates or limits call
- Can become a single point of failure





