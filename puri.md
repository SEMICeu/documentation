# Persistent URIs (PURIs)

Persistent URIs are identifiers in the form of a URI that are maintained for eternity. 
They provide stability throughout space and time for data.

A key aspect for persistent URIs is dereferenceability.
Technically it means that content negotation is active for the PURI.
Without it, nobody can verify the original values and the risk exists that a local usage changes the semantics for the identifier unnoticed.
Dereferencing is thus a technical mean to ensure that semantics are stable and not shifting behind the back of users.


## PURIs at SEMIC

A PURI is of the form *http://data.europa.eu/{domain}/{reference}*. 

where 

 - domain: requested and assigned by Publications Office which is the maintainer of data.europa.eu
 - reference: maintained and assigned by editors of the data model


### Supported domains by SEMIC

TDB

|domain|description|example|Content|
|---|---|---|---|
|m8g| The Core Vocabularies domain | http://data.europa.eu/m8g/Criterion | [releases/m8g](https://github.com/SEMICeu/uri.semic.eu-puris/tree/main/releases/m8g) |

### System setup by SEMIC

All PURIs maintained by SEMIC should be handled by the server *uri.semic.eu*.
On this server a PURI resolvement service is installed that implements the content negotation.
The source code and deployment instructions are found in the repository [uri.semic.eu-proxy](https://github.com/SEMICeu/uri.semic.eu-proxy).


### Data specifications and PURIs

Data specifications must assign an URI to each term. 
This URI is either an existing URI or a new URI minted within [one of the persistent URI domains](#Supported-domains-by-SEMIC) from SEMIC.

Any change (creation, updating, ...) to a term associated with a SEMIC owned PURI requires editorial effort to ensure the expected dereferenceability.

1. Editors create/update a UML representation of the vocabulary annotated with the right information.
2. Using the toolchain an RDF file is created that contains the data of the vocabulary.
3. Editors extract from the RDF file the data for each PURI and add it to the  [uri.semic.eu-puris](https://github.com/SEMICeu/uri.semic.eu-puris) repository.

These steps are part of the editorial effort editors have to perform manually.

**Note**: this process is a candidate to be automated. 










