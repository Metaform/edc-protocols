# Contract Negotiation Protocol

## Introduction: Terms

This document outlines the key elements of the contract negotiation protocol. The following terms are used:

- A _**message type**_ defines the structure of a _message_.
- A _**message**_  is an instantiation of a _message type_.
- The _**contract negotiation protocol**_ is the set of allowable message type sequences and is defined as a state machine (CNP-SM).
- A _**contract negotiation (CN)**_ is an instantiation of the CNP-SM.
- A _**provider**_ is a participant agent that offers an asset.
- A _**consumer**_ is a participant agent that requests access to an offered asset.

## Contract Negotiation Protocol

A contract negotiation (CN) involves two parties, a _provider_ that offers one or more assets under a usage policy and _consumer_ that requests assets. A CN progresses through
a series of states, which are tracked by the provider and consumer using messages. A CN transitions to a state in response to a message from the counter-party.

The CN states are:

- **REQUESTED** - A contract for an asset has been requested by the consumer and the provider has sent an ACK response.
- **PROVIDER_OFFERED** - The provider has sent a contract offer to the consumer and the consumer has sent an ACK response.
- **CONSUMER_OFFERED** - The consumer has sent a contract offer to the provider and the provider has sent an ACK response.
- **CONSUMER_ACCEPTED** - The consumer has accepted that latest contract offer and the provider has sent an ACK response.
- **PROVIDER_AGREED** - The provider has accepted that latest contract offer, sent an agreement to the consumer, and the consumer has sent an ACK response.
- **CONSUMER_VERIFIED** - The consumer has sent an agreement verification to the provider and the provider has sent an ACK response.
- **PROVIDER_FINALIZED** - The provider has sent a finalization message to the consumer and the provider has sent an ACK response. Data is now available to the consumer.
- **DECLINED** - The provider or consumer has declined the contract negotiation. This is a terminal state.
- **ERROR** - The provider or consumer has placed the contract negotiation in an error state. This is a terminal state.
- **ABANDONED** - The provider or consumer has placed the contract negotiation in an abandoned state. This is a terminal state.

### Contract Negotiation State Machine

The CN state machine is represented in the following diagram. Note that transitions to the ERROR or ABANDONED states may occur from any other state and are not shown for simplicty:

![](./contract.negotiation.state.machine.png)

Transition marked with `C` indicate a message sent by the consumer, transitions marked with `P` indicate a provider message. Terminal states are final; the state machine may 
not transition to another state.

## Message Types

The CN state machine is transitioned upon receipt and acknowledgement of a message. This section details those messages as abstract message types. 

### Notes
- Concrete wire formats are defined by the protocol binding, e.g. HTTPS. 
- The `OK` and `ERROR` response message types are empty body responses that are mapped onto a protocol such as HTTPS.
- All ODRL policy types (Offer, Agreement) must contain a UID (GUID).
- The ODRL Agreement must have a target property containing the asset id.

### 1. ContractRequestMessage

**Sent by**: Consumer

**Resulting State**: REQUESTED

**Example**: [ContractRequestMessage](./message/contract.request.message.json)

**Response**: [ContractNegotiation](./message/contract.negotiation.message.json) containing the negotiation id or ERROR. 

**Schema**: (xx)[]

#### Description

The _ContractRequestMessage_ is sent by a consumer to initiate a contract negotiation.

#### Notes

- The dataset id is not technically required but included to avoid an error where the offer is associated with a different data set.
- `callbackAddress` is a URI indicating where messages to the consumer should be sent. If the address is not understood, the provider MUST return an UNRECOVERABLE error.

### 2. ContractOfferMessage

**Sent by**: Consumer or Provider

**Resulting State**: PROVIDER_OFFERED or CONSUMER_OFFERED

**Example**: [ContractOfferMessage](./message/contract.offer.message.json)

**Response**: OK or ERROR

**Schema**: (xx)[]

#### Description

The _ContractOfferMessage_ is sent by a consumer or provider to exchange a contract offer.

#### Notes

-   The contract offer must include a target containing the dataset id.  

### 3. ContractOfferAcceptMessage

**Sent by**: Consumer

**Resulting State**: CONSUMER_ACCEPT

**Example**: [ContractOfferAcceptMessage](./message/contract.offer.accept.message.json)

**Response**: OK or ERROR

**Schema**: (xx)[]

#### Description

The _ContractOfferAcceptMessage_ is sent by a consumer when it accepts a provider contract offer.

### 4. ContractOfferDeclineMessage

**Sent by**: Consumer or Provider

**Resulting State**: DECLINED

**Example**: [ContractOfferDeclineMessage](./message/contract.offer.decline.message.json)

**Response**: OK or ERROR

**Schema**: (xx)[]

#### Description

The _ContractOfferAcceptMessage_ is sent by a consumer or provider when it declines a contract offer or consumer ContractOfferAcceptMessage, thereby placing the state machine in
the DECLINED terminal state.

### 5. ContractAgreementMessage

**Sent by**: Consumer or Provider

**Resulting State**: PROVIDER_AGREED

**Example**: [ContractAgreementMessage](./message/contract.agreement.message.json)

**Response**: OK or ERROR

**Schema**: (xx)[]

#### Description

The _ContractAgreementMessage_ is sent by a provider when it agrees to a contract.

### 6. ContractAgreementVerificationMessage

**Sent by**: Consumer

**Resulting State**: CONSUMER_VERIFIED

**Example**: [ContractAgreementVerificationMessage](./message/contract.agreement.verification.message.json)

**Response**: OK or ERROR

**Schema**: (xx)[]

#### Description

The _ContractAgreementVerificationMessage_ is sent by a consumer to verify the acceptance of a contract agreement.

### 7. ContractAgreementFinalizeMessage

**Sent by**: Provider

**Resulting State**: PROVIDER_FINALIZED

**Example**: [ContractAgreementFinalizeMessage](./message/contract.agreement.finalize.message.json)

**Response**: OK or ERROR

**Schema**: (xx)[]

#### Description

The _ContractAgreementFinalizeMessage_ is sent by a provider to indicate a contract agreement has been finalized and the associated asset is accessible.

### 8. AbandonMessage

**Sent by**: Consumer or Provider

**Resulting State**: ABANDONED

**Example**: [AbandonMessage](./message/abandon.message.json)

**Response**: OK or ERROR

**Schema**: (xx)[]

#### Description

The _AbandonMessage_ is sent by a consumer or provider indicating it has abandoned the negotiation.

### 9. ErrorMessage

**Sent by**: Consumer or Provider

**Resulting State**: ERROR

**Example**: [ErrorMessage](./message/error.message.json)

**Response**: OK or ERROR

**Schema**: (xx)[]

#### Description

The _AbandonMessage_ is sent by a consumer or provider indicating an error has occurred.

## Checksum Calculations

Checksums are calculated by creating the [[JWS/CT]](#references) of ...

## References

- [[JCS] JSON Canonicalization Scheme](https://www.ietf.org/archive/id/draft-jordan-jws-ct-08.html)
- [[JWS/CT] JWS Clear Text JSON Signature Option](https://www.ietf.org/archive/id/draft-jordan-jws-ct-08.html)
- [[JWS] JSON Web Signature](https://www.rfc-editor.org/rfc/rfc7797.html)


## JWS Clear Text JSON Signature Option

- Adopt JWS/CT, an extension to the JSON Web Signature (JWS) standard.
- Combines the detached mode of JWS with the JSON Canonicalization Scheme (JCS). Detached mode is when the payload section of the JWS is replaced
  by an empty string:  XXXX.PAYLOAD.YYYY becomes XXXX..YYYY. Detached mode is described in the JWS spec.
- Maintains Signed JSON data in JSON format.











