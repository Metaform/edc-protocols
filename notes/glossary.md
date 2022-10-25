# Glossary


## A


### Applicant
Organization formally applying for being certified by the
 [Certification Body](#certification-body).

### Authorization
The process of verifying whether a requesting party is allowed to 
access a resource or system.

## B


## C

### Catalog (formerly Broker Service Provider)
Intermediary managing a metadata repository that provides information
 about the [Data Source](#data-source)s available in the
 International Data Spaces; multiple catalog providers may be
 around at the same time, maintaining references to different,
 domain-specific subsets of [Data Endpoint](#data-endpoint)s.

### Certificate Authority
Trusted third-party entity issuing digital certificates
 (e.g., x509 certificates); may host services to validate certificates
 issued. (see [Identity Provider](../Components/IdentityProvider/README.md))

### Certification Body
Governance body certifying components and entities seeking admission to
 the International Data Spaces; aside from having the final word on
 granting or denying a certificate, it is responsible for maintaining
 the [Certification Scheme](#certification-scheme) (including its
 catalog of requirements), overseeing and approval of Evaluation
 Facilities, and ensuring compatibility of evaluation procedures carried
 out by Evaluation Facilities.

### Certification Scheme
Scheme defining the processes, roles, targets, and criteria involved in
 the certification of components and entities; maintained by the
 [Certification Body](#certification-body).
- [IDS Certification Scheme 2.0 (current version)](https://www.internationaldataspaces.org/wp-content/uploads/2020/01/IDSA-Strategy-paper-certification-scheme-V.2.pdf)


### Connector
Dedicated communication server for sending and receiving data in
 compliance with the general Connector specification; different types
 of Connectors can be distinguished (Base Connector vs.
 Trusted Connector, or Internal Connector vs. External Connector).
- [IDS-G specification "Connector"](../Components/Connector/README.md)

### Connector-Self-description
Description of a [Connector](#connector) participating in the IDS for
 being read by other IDS [Participant](#participant)s; created by
 the[Data Provider](#data-provider) or Data User as the first step of
 the [Connector](#connector) configuration process; contains information
 such as the name of the [Connector](#connector) provider or the name of
 the maintainer, as well as information about the content and type of
 the data offered or requested, about data communication interfaces,
 and about usage policies and contracts.

### Consumer (formerly Data Consumer)
Core [Participant](#participant) in the International Data Spaces
 requesting and using data provided by a [Data Provider](#data-provider).


## D


### Data Asset
Content exposed for exchange via [Data Endpoint](#data-endpoint)s
 according to a parametrized Data Service interface; Data Assets are
 expected to be focused, homogeneous, and consistent over time with
 regard to granularity, coverage, context, data structure, and
 conceptual classification.




### Data Owner
Core [Participant](#participant) having complete control over the data
 it makes available in the International Data Spaces; defines the terms
 and conditions of use of its data.

### Data Provider
Core [Participant](#participant) exposing [Data Source](#data-source)s
 via a [Connector](#connector); a Data Provider may be an enterprise or
 other organization, a data marketplace, an individual, or a
 “smart thing”.



## E

### Evaluation Facility
Governance body providing services related to the certification of
 components and entities (certification targets) seeking admission to
 the International Data Spaces; responsible for detailed technical
 evaluation of targets in consistence with the
 [Certification Scheme](#certification-scheme) and its catalog of
 requirements; reports evaluation results to the
 [Certification Body](#certification-body).

## G



## I

### Identity Provider
Intermediary offering services to create, maintain, manage and validate
 identity information of and for [Participant](#participant)s in the
 International Data Spaces.

### Identity Verification
The process of verifying the validity of a supplied identity proof.

### IDS
- See [International Data Spaces](#international-data-spaces).

### IDS Information Model
Set of vocabularies and related schema information for the semantic
 description of International Data Spaces entities (e.g.,
 [Data Endpoint](#data-endpoint)s or [Data App](#data-app)s), data
 provenance, or licensing information; the core IDS Vocabulary is
 domain-independent; it can be extended and/or reference third-party
 vocabularies to express domain-specific aspects.

See also:
- GitHub [repository](https://github.com/International-Data-Spaces-Association/InformationModel)
- IDS-G specification [Information Model](../Infomodel/README.md)
- Shortcut: `IDS-IM`


### Information Model
- [Information Model](https://github.com/International-Data-Spaces-Association/IDS-G-pre/tree/connector-interaction/Infomodel)
The data model of the IDS. It defines all classes, attributes and entities known to the actors in the IDS.

### International Data Spaces
Distributed network of [Data Endpoint](#data-endpoint)s (i.e.,
 instantiations of the International Data Spaces
 [Connector](#connector)), allowing secure exchange of data and
 guaranteeing [Data Sovereignty](#data-sovereignty).
- Shortcut: `IDS`


### IDS Reference Architecture Model
Data Exchange and Data Sharing are essential for Data-Driven
 Business-Ecosystems, as well as the need for
 [Data Sovereignty](#data-sovereignty). The International Data Spaces
 Reference Architecture Model (IDS-RAM) defines fundamental concepts
 for [Data Sovereignty](#data-sovereignty), Data Sharing and Data
 Exchange. Focusing on the generalization of concepts, functionality,
 and overall processes involved in the creation of a secure
 “network of trusted data”, the IDS-RAM resides at a higher
 abstraction level than common architecture models of concrete software
 solutions do. The document provides an overview supplemented by
 dedicated architecture specifications defining the individual
 components of the International Data Spaces

The model is made up of five layers: The Business Layer specifies and
 categorizes the different roles which the [Participant](#participant)s
 of the International Data Space can assume, and it specifies the main
 activities and interactions connected with each of these roles. The
 Functional Layer defines the functional requirements of the
 International Data Spaces, plus the concrete features to be derived
 from these. The Process Layer specifies the interactions taking place
 between the different components of the International Data Spaces;
 it provides a dynamic view of the Reference Architecture Model. The
 Information Layer defines a conceptual model which makes use of
 linked-data principles for describing both the static and the dynamic
 aspects of the International Data Spaces’s constituents. The System
 Layer is concerned with the decomposition of the logical software
 components, considering aspects such as integration, configuration,
 deployment, and extensibility of these components.

In addition, the Reference Architecture Model comprises three
 perspectives that need to be implemented across all five layers:
 Security, Certification, and Governance. The Security Perspective
 defines the common security measures for the International Data Spaces
 and the concepts for Data Usage Control. The Certification Perspective
 describes the IDS [Certification Scheme](#certification-scheme) as a
 foundation for every interaction in the IDS. The Governance Perspective
 describes the Responsibilities of the Roles in the IDS.

- [IDS-RAM 3.0 (current version, PDF)](https://www.internationaldataspaces.org/wp-content/uploads/2019/03/IDS-Reference-Architecture-Model-3.0.pdf)

- Shortcut: `IDS-RAM`

## J

### JSON Web Token
- [rfc7523](https://tools.ietf.org/html/rfc7523)
- Shortcut: `JWT`

### JWT
- Glossary: [JSON Web Token](#json-web-token)

## M


## P

### Participant
Stakeholder in the International Data Spaces, assuming one or more of
 the predefined roles; every Participant is given a unique identity by
 the [Identity Provider](#identity-provider).

### Participant Information Service

- [IDS-G specification "ParIS"](../Components/IdentityProvider/ParIS/README.md)
- Shortcut: `ParIS`

## S

## U

### Usage Contract
Set of rules and conditions regarding one or more transactions in the
 International Data Spaces.

### Usage Control

### Usage Policy
Set of rules specified by the [Data Owner](#data-owner) restricting
 usage of its data; covers aspects like time-to-live or forwarding
 conditions (e.g., anonymization or scope of usage); transmitted along
 with the respective data, and enforced while residing on the
 [Connector](#connector) of the [Data Consumer](#data-consumer).

## V
