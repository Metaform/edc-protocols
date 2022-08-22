# HTTP Messages

## Key Points

- The API is RESTFul HTTPS.
- Each dataspace participant will host a catalog agent (or will delegate to a third-party).
- Versioning will be done via URLs
- Pagination specified using [Web Linking](https://datatracker.ietf.org/doc/html/rfc5988).
- Authorization via OAUTH2, Web DIDs, or another mechanism.
- There is no need to specify a query language. Since all message types are DCAT serialized as JSON, any query language that can consume the serialization will work. 
- Replication can be handled via issuing GET requests, altough in most cases replication is not needed. 

## Message Examples

### 1. GET Catalog with pagination

Request: 

```
GET https://provider.com/catalog

Authorization: ...
```

First page response:

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
