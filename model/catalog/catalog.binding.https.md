# Catalog HTTPS Binding

## Introduction

This specification defines a RESTful API over HTTPS for the [Catalog Protocol] specification. 

The OpenAPI definitions for this specification can be accessed [here](TBD). 

## Path Bindings

### Prerequisites

1. The `<base>` notation indicates the base URL for a catalog service endpoint. For example, if the base catalog URL is `api.example.com`, the URL `https://<base>/catalog` will 
map to `https//api.example.com/catalog`.

2. All request and response messages must use the `application/json` media type. 

### 1. CatalogErrorMessage

In the event of a request error, the catalog service must return an appropriate HTTP code and a [CatalogErrorMessage](./catalog.protocol.md#) in the response body.
                                 
| Field   | Type          |  Description                                               |
|---------|---------------|------------------------------------------------------------|
| code    | string        | An optional implementation-specific error code.            |
| reasons | Array[object] | An optional array of implementation-specific error objects. |


### 2. The `catalog` endpoint

#### 2.1 GET

The [CatalogRequestMessage](catalog.protocol.md#1-catalogrequestmessage) corresponds to `GET https://<base>/catalog`: 

```
GET https://provider.com/catalog

Authorization: ...
```
The `Authorization` header is optional if the catalog service does not require authorization. If present, the contents of the `Authorization` header are detailed in the 
[Authorization section](#authorization).

#### 2.1.1 OK (200) Response

If the request is successful, the catalog service must return a response body containing a [CatalogMessage](./message/catalog.message.json) which is a profiled DCAT Catalog type
described by the [Catalog Protocol Specification](catalog.protocol.md).

## Technical Considerations

### Authorization

A catalog service may require authorization. If the catalog service requires authorization, requests must include an HTTP `Authorization` header with a token. The contents of  
the token are undefined by may be an OAUTH2, Web DID, or other access token type.

### Versioning

- Versioning will be done via URLs. TBD.

### Pagination

A catalog service may choose to paginate the results of a `CatalogRequestMessage`. Pagination data is specified using [Web Linking](https://datatracker.ietf.org/doc/html/rfc5988)
and the HTTP `Link` header. The `Link` header will contain URLs for navigating to previous and subsequent results. The following request sequence demonstrates pagination:


```
Link: <https://provider.com/catalog?page=2&per_page=100>; rel="next"
{
   "@type": "dcat:Catalog"
   ...
}

```

Second page response:

```
Link: <https://provider.com/catalog?page=1&per_page=100>; rel="previous"
Link: <https://provider.com/catalog?page=3&per_page=100>; rel="next"

{
   "@type": "dcat:Catalog"
   ...
}
```

Last page response:

```
Link: <https://provider.com/catalog?page=2&per_page=100>; rel="previous"

{
   "@type": "dcat:Catalog"
   ...
}
```
