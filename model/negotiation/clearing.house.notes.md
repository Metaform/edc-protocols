# Cryptography and Signing 
- [Jackson Canonicalization](https://cowtowncoder.medium.com/jackson-tips-sorting-json-using-jsonnode-ce4476e37aee)
- [JCS Signing](https://connect2id.com/blog/how-to-secure-json-objects-with-hmac)
- [JWS Signing](https://connect2id.com/products/nimbus-jose-jwt/examples/jws-with-rsa-signature)
- [JOSE JWS](https://cyberphone.github.io/doc/security/jose-jcs.html) 
- [JWS/CT](https://www.ietf.org/archive/id/draft-jordan-jws-ct-08.html) 

# Approach
## JWS Clear Text JSON Signature Option 
- Adopt JWS/CT, an extension to the JSON Web Signature (JWS) standard.
- Combines the detached mode of JWS with the JSON Canonicalization Scheme (JCS). Detached mode is when the payload section of the JWS is replaced 
by an empty string:  XXXX.PAYLOAD.YYYY becomes XXXX..YYYY. Detached mode is described in the JWS spec.
- Maintains Signed JSON data in JSON format.


# Clearing House Memorialization

The clearing house is a secure event store that is used to provide proof that an event occurred at a given time and has not been tampered with. 

## Principles
1. Parties memorialize events with a clearing house agent. Events contain data with a GUID. For example, a contract signing event may include the contract agreement.
2. The purpose of memorialization is to provide proof that an event occurred and that the data associated with the event has not been tampered with. 
3. Consumer and provider memorialization are independent processes.
4. The counter-party to an agreement event and its data are opaque to the clearing house. Only the party memorializing the event is known.
5. The role of the clearing house is **NOT** to prove two parties signed an agreement.
 

## Consumer Flow
1. Consumer receives the signed provider agreement (agreement with a detached JWS). (This is before the consumer has signed the agreement)
1. The consumer adds the provider detached JWS to the agreement provider signature property. 
1. The consumer hashes the agreement (including provider signature) using JCS. 
1. The consumer signs the agreement using a detached JWS. 
1. The consumer sends an `EventMessage` containing the hash and detached JWS to the clearing house (memorializes it).
1. The clearing house records the `EventMessage` and creates a `Receipt` (containing the hash, a UTC timestamp, and a detached JWS), and sends it back to the consumer.
1. The consumer receives the `Receipt` from the clearing house and adds it to the agreement receipt property array.
1. The consumer creates another JWS without the provider signature, adds it to the agreement consumer signature property, and sends a verification to the provider. 
   This can be done independently of the previous steps.

## Provider Flow
1. Provider receives the consumer verification (agreement with the consumer detached JWS). 
1. The provider adds the consumer detached JWS to the agreement consumer signature property. 
1. The provider hashes the agreement (including consumer signature) using JCS.  
1. The provider signs the agreement using a detached JWS. 
1. The provider sends an `EventMessage` containing the hash and detached JWS to the clearing house (memorializes it).
1. The clearing house records the `EventMessage` and creates a `Receipt` (containing the hash, a UTC timestamp, and a detached JWS), and sends it back to the provider.
1. The provider receives the `Receipt` from the clearing house and adds it to the agreement receipt property array.
1. The provider sends a FINALIZED message to the consumer.
                                
## Scenarios

#### Provider does not memorialize
The provider never registers with the clearing house. The consumer can prove it received a signed agreement from the provider and when it was
memorialized using the clearing house timestamp.

#### Consumer does not memorialize
The consumer never registers with the clearing house. The provider can prove it received a signed agreement from the consumer and when it was
memorialized using the clearing house timestamp.

#### Consumer does not verify
The provider does not advance the state to FINALIZED and the consumer will not have access to the data. The provider may need to send a message to the 
clearing house, which records with a timestamp. The timestamp is necessary to avoid race conditions.



