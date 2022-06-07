# Persistent URIs (PURIs)

Persistent URIs are identifiers in the form of a URI that are maintained for eternity. 
They provide stability throughout space and time for data.

A key aspect for persistent URIs is dereferenceability.
Technically it means that content negotation is active for the PURI.
Without it, nobody can verify the original values and the risk exists that a local usage changes the semantics for the identifier unnoticed.
Dereferencing is thus a technical mean to ensure that semantics are stable and not shifting behind the back of users.


## PURIs at SEMIC

A PURI is of the form *`http://data.europa.eu/{domain}/{reference}`*, where 

 - *{domain}* is requested and assigned by Publications Office, which is the maintainer of **data.europa.eu** domain
 - *{reference}* is maintained and assigned by editors of the data specification

The complete list of supported persistent domains by data.europa.eu are found [here](https://data.europa.eu/URI.html).

### Supported domains by SEMIC
SEMIC is responsible for a number of PURI domains. 
They are listed below with their activation level in the SEMIC PURI service.


The following domains are configured on SEMIC PURI service and are ready to be used by editors to publish PURIs 

|Domain|Description|Example|Content|
|---|---|---|---|
|m8g| The Core Vocabularies domain | http://data.europa.eu/m8g/Criterion | [releases/m8g](https://github.com/SEMICeu/uri.semic.eu-puris/tree/main/releases/m8g) |
|r5r| The DCAT-AP domain | http://data.europa.eu/r5r/availability | [releases/r5r](https://github.com/SEMICeu/uri.semic.eu-puris/tree/main/releases/r5r) |
|p4s| The EU Once Only Principle (Single Digital Gateway - OOTS) domain - unused | | [releases/p4s](https://github.com/SEMICeu/uri.semic.eu-puris/tree/main/releases/p4s) |

The following domains are handled by the [proxy](https://github.com/SEMICeu/uri.semic.eu-proxy) operated by SEMIC .

|Domain|Description| Notes |
| --- | --- | --- | 
|930| The GeoDCAT-AP domain | | 
|edm| The EU Public Domain project  | |

The following domains are directly handled by the [data.europa.eu proxy](http://data.europa.eu) operated by the Publications Office.

|Domain|Description| Notes |
| --- | --- | --- | 
|3b1| The adms controlled vocabularies | |
|s1n| The statDCAT-AP domain | | 

The following domains are domains that are closely related to SEMIC activities but maintained by other teams.

|Domain|Description| Notes |
| --- | --- | --- | 
|dap| The BregDCAT-AP domain | |
|w21| The Joinup data catalogue | |
|2sa| The Common Assessment Method for Standards and Specifications (CAMSS) domain | |


The following domains are decommissioned.

|Domain|Description| Notes |
| --- | --- | --- | 
| 3rx | The EU Budget Vocabulary | |


### System setup by SEMIC

#### Design objectives

The SEMIC PURI service is designed to provide editors the means to manage the PURIs without (or minimal) involvement of a developer or a system admin.
Because the editorial activities only involve GitHub interaction to create artefacts and publish them to the consumers, it is desirable for the PURI service to be also designed in this spirit.

Namely the editor is granted acccess to a GitHub repository. 
By changing the content of this GitHub repository also the content of the PURI service changes.



#### Deployed setup

Content negotation is a more complex proxy configuration than serving a static website as provided by GitHub pages used by the data specifications.
Therefore the solution has been deployed on a SEMIC operated virtual machine. 

To the outside world, the SEMIC PURI service is accessible under the domain *uri.semic.eu*.
The description of the implemented content negotation rules, source code and deployment instructions are found in the repository [uri.semic.eu-proxy](https://github.com/SEMICeu/uri.semic.eu-proxy). 

The content of the PURIs is stored in another repository [uri.semic.eu-puris](https://github.com/SEMICeu/uri.semic.eu-puris). 
The PURI content repository is organised to match straightforward the URI structure of a PURI.
The turtle representation for the PURI of the form `http://data.europa.eu/{domain}/{reference}` is found in the file `/releases/{domain}/{reference}.ttl` stored in the `main` branch of the PURI content repository.
The same holds for other representations.


#### Usage 

A developer is responsible for enabling (configuring) a domain in the SEMIC PURI service. 
When setup, editors should only edit the content of the PURI in the content repository [uri.semic.eu-puris](https://github.com/SEMICeu/uri.semic.eu-puris). 

**Future work**: Today the editors require assistance from a developer to complete the editorial process for PURIs.
This limitation is documented in the proxy documentation and it future work to improve the setup to match the design objectives.


### Data specifications and PURIs

Data specifications must assign an URI to each term. 
This URI is either an existing URI or a new URI minted within [one of the persistent URI domains](#supported-domains-by-semic) from SEMIC.

Any change (creation, updating, ...) to a term associated with a SEMIC owned PURI requires editorial effort to ensure the expected dereferenceability.

In short, the steps are: 

1. Editors create/update a UML representation of the vocabulary according to the [editorial flow](./editorial_flow.md).
2. Editors select the generated RDF file which contains the data of the vocabulary.
3. Editors extract from the RDF file the data for each PURI and add it to the  [uri.semic.eu-puris](https://github.com/SEMICeu/uri.semic.eu-puris) repository.  

Detailed steps are described in [uri.semic.eu-proxy](https://github.com/SEMICeu/uri.semic.eu-proxy).


**Note**: These steps are part of the editorial effort editors have to perform manually.
Therefore this process is a candidate to be automated and integrated in the toolchain.









