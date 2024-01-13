# An Event Processing Service Architecure

A generic event processing service architecture for minimizing data loss even when a service goes down.

As expert in enterprise real-time logging and analytics platforms like LogRhythm, I have spent a lot of time with event processing platforms.  The general architecture usually follows the same core patterns/processes to reliably receive events while protecting against data loss:

1. There are agents that receive or actively collect events through push or pull mechanisms from various sources.
2. Agents then batch/aggregate these events, sometimes persisting them on the client side until they are ACK'd by an upstream ingestion service.
3. A stateless highly available ingestion service, that can scale based on incoming rates, receive batches of events over the network (i.e. HTTP/GRPC).  
4. The transaction to client doesn't complete until the events are written to a durable and performant storage layer, i.e. a distributed event streaming platform like Kafka.  The goal is to have the event data persisted, replicated, highly available and easily consumable.
5. Downstream services, apps, and datastores can independently scale and asyncronously consume, enrich, normalize, order, archive, analyze and store the data according to use case.

This type of architecture is very similar to what can be achieved with an data mesh and the type of platform I helped lead the construction of at LogRhythm.  

Please refer to the below diagram for a more in detail look at the described architecture:

![Event Processing Architecture Diagram](EventProcessingArchitecture.png)