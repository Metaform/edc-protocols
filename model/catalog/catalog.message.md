

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
