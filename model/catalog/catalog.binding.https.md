# Catalog HTTPS Binding
               
This specification details how the [Catalog Protocol] maps to HTTPS messages.

## Key Points

- The API is RESTFul HTTPS.
- Versioning will be done via URLs.
- Pagination specified using [Web Linking](https://datatracker.ietf.org/doc/html/rfc5988).
- Authorization via OAUTH2, Web DIDs, or another mechanism.

## Message Bindings

### 1. CatalogRequestMessage

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

