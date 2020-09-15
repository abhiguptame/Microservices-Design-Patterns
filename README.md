# Microservices: Design Patterns

## Microservices:
- Smaller scoped units of work
- Focus on data, business, or function domains
- Not monolithic service artifacts

## Service Types:
- Data service
- Business service
- Translation service
- Edge service

## Platform:
- Runtime for services
- Ancillary services
- Operational components
- Diagnostic components

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

## Sidecar Design:
- Determine the process
- Build the sidecar
- Schedule it to deploy with the appropriate services
- Functionality appears without embedding it

## Strangler Pattern:
- Break a monolith up by "strangling" the dependency on it.
- Can be top down.
- Can be bottom up.
- Essentially carving out functionality.

## Edge Design:
- Identify client
- Build contracts
- Implement contracts
- Maintain passivity as long as client is needed

## Cloud Native
- Architectural style
- Designed to facilitate operating in the cloud
- Focuses on portable and scalable applications
- Can be run in single datacenter

## Atomic Transaction Microservices:
- Gurantee atomicity, consistency, isolation, durability (ACID) transactions across domains.
- Provide failure domains and rollbacks
- Force blocking until commit
- Don't use distributes transactions





