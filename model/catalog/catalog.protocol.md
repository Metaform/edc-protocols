# Catalog Protocol

## Introduction: Terms

This document outlines the catalog protocol. The following terms are used:

- A _**message type**_ defines the structure of a _message_.
- A _**message**_  is an instantiation of a _message type_.
- A _**catalog**_ is a [DCAT catalog](https://www.w3.org/TR/vocab-dcat-3/) offered by a _provider_ 
- a _**catalog service**_ is a provider participant agent that advertises offered assets
- A _**consumer**_ is a participant agent that requests access to an offered asset.

The catalog protocol defines a how a catalog is exchanged between a catalog service and consumer.

## Message Types

### Notes
- Concrete wire formats are defined by the protocol binding, e.g. HTTPS. 

### 1. CatalogRequestMessage

**Sent by**: Consumer

**Example**: Abstract GET

**Response**: [CatalogMessage](./message/catalog.message.json) containing the [DCAT catalog](https://www.w3.org/TR/vocab-dcat-3/#Class:Catalog. 

**Schema**: (xx)[]

#### Description

The `CatalogRequestMessage` is an abstract empty body message sent by a consumer to a catalog service. The catalog service MUST respond with a `CatalogMessage,` which is a 
valid [DCAT Catalog](https://www.w3.org/TR/vocab-dcat-3/#Class:Catalog.

The catalog service MAY require an authorization token. Details for including that token can be found in the relevant catalog binding specification. Similarly, pagination may
be defined in the relevant catalog binding specification.
                            

### 2. CatalogRequirementsMessage
TBD.                               
   
## Technical Considerations

### Queries

The current specification does not require a _**catalog service**_ to support catalog queries. It is expected that query capabilities will be implemented by the consumer against the 
results of a `CatalogRequestMessage,` as the latter is an RDF vocabulary. It is expected client-side querying to be scaled by periodically crawling provider catalog services,
caching the results, and executing queries against the locally-stored catalogs.    

### Replication Protocol

The catalog protocol is designed to be used by federated services without the need for a replication protocol. Each consumer is responsible for issuing requests
to 1..N catalog services, and managing the results. It follows that a specific replication protocol is not needed, or more precisely, each consumer replicates data from 
catalog services by issuing `CatalogRequestMessages`.  

How the consumer discovers catalog services is defined by the discovery protocol adopted by a particular dataspace. 

### Security

It is expected (although not required) that catalog services implement access control. A catalog as well as individual catalog _datasets_ may be restricted to trusted parties.
The catalog service may therefore require consumers to include a security token along with `CatalogRequestMessage`s. The specifics of how this is done can be found in the relevant 
catalog binding specification. In addition, this specification does not detail the contents of the security token. It is expected different security mechanisms may be used such
as OAuth 2 or Web DIDs.

### Catalog Brokers

A dataspace may include _**catalog brokers**_. A catalog broker is a consumer that has trusted access to 1..N upstream catalog services and advertises their respective catalogs as a
single catalog service. The broker is expected to honor upstream access control requirements.

## DCAT and ODRL Profiles

The catalog is a DCAT catalog with the following restrictions:

1. Each DCAT `Dataset` must have at least one DCAT `Distribution`. 
2. The DCAT `Distribution` must have at least one `DataService` which specifies where the distribution is obtained. Specifically, a `DataService` specifies the endpoint for 
   initiating a [Contract Negotiation](../negotiation/contract.negotiation.protocol.md) and [Transfer Process](TBD).
3. Each DCAT `Dataset` must have an `hasPolicy` attribute that contains an ODRL `Offer`.
4. Each ODRL `Offer` must have a unique UUID (ODRL `uid`).
5. Each ODRL `Offer` must be unique to a dataset since the target of the offer is derived from its enclosing context.
6. Each ODRL `Offer` must NOT include an explicit `target` attribute. 
