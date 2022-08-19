# DCAT Profile

- Define minimum properties for `Dataset`, `Distribution`, and `DataService`.
- Add 1..N cardinality constraint to `hasPolicy`. Contained policies are defined using `OR` semantics, e.g. contract offer A or B.
- `accessURL` on `Distribution` needs to be specified as the connector address.
- Define how a DataService id can be a Web DID. In this case the accessUrl must match the service URL specified in the resolved DID document.
- Define custom dct:type (different than JSON-LD @type) for a connector on `DataService`.

# ODRL

- Need to define a deterministic `Policy` infoset so that hashes can be generated for verification and signing.
