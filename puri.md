# Persistent URIs (PURIs)

Persistent URIs are identifiers in the form of a URI that are maintained for eternity. 
They provide stability for data through space and time.

A key aspect for persistent URIs is dereferenceability.
Technically it means that content negotation is active for the PURI.
	Without it, nobody can verify the original values, and the risk exists that a local usage changes the semantics for the identifier unnoticed.
	Dereferencing is thus a technical mean to ensure that semantics are stable and it is not shifting "behind the back" of the users.

PURIs form the foundation of data specifications. 
In order to unambigously fix the semantics of terms in a data specification, each term gets a URI assigned.
This URI is either an existing URI or a new URI minted within [one of the persistent URI domains](#supported-domains-by-semic) from SEMIC.
Reusing PURIs from external domains means that the data specification will rely on the semantics and the governance associated with the external URI to set the semantics of the term.
For those terms that are identified by a PURI within a SEMIC owned domain, it is the editors duty to perform the neccesary editorial effort to maintain the correctness of the shared content via dereferenceability.
In this chapter the setup and basic editorial maintenance activities for PURIs within SEMIC are described.


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

The SEMIC PURI service is designed to provide editors the means to manage the PURIs without (or with minimal) involvement of a developer or a system admin.
Because the editorial activities only involve GitHub interaction to create artefacts and publish them to the consumers, it is desirable for the PURI service to be also designed in this spirit.

Namely, the 	editor is granted acccess to a GitHub repository. 
By changing the content of this GitHub repository, the content of the PURI service should also change.



#### Deployed setup

Content negotation requires a more complex proxy configuration than serving a static website, as provided by GitHub Pages in the case of the data specifications.
Therefore, the solution has been deployed on a virtual machine operated by SEMIC. 

To the outside world, the SEMIC PURI service is accessible under the domain *uri.semic.eu*.
The description of the implemented content negotation rules, source code, and deployment instructions are found in the repository [uri.semic.eu-proxy](https://github.com/SEMICeu/uri.semic.eu-proxy). 

The content of the PURIs is stored in another repository [uri.semic.eu-puris](https://github.com/SEMICeu/uri.semic.eu-puris). 
The PURI content repository is organised to match directly the URI structure of a PURI.
The Turtle representation for the PURI of the form `http://data.europa.eu/{domain}/{reference}` is found in the file `/releases/{domain}/{reference}.ttl`, stored in the `main` branch of the PURI content repository.
The same holds for other representations.


#### Usage 

A developer is responsible for enabling (configuring) a domain in the SEMIC PURI service. 
When this is set up, the editors should only edit the content of the PURI in the content repository [uri.semic.eu-puris](https://github.com/SEMICeu/uri.semic.eu-puris). 
More precisely, the editors should extract the content for the PURI from the RDF artefact that was generated for the data specification.
Then they should create the RDF serialisations to be added to the content repository, according to the conventions explained before.

An example is shown in the [editorial flow](./editorial_flow.md#part-3-publish-the-result--video-) chapter.


**Future work 1**: Today the editors require assistance from a developer to complete the editorial process for PURIs.
This limitation is documented in the proxy documentation, and it is future work to improve the setup to match the design objectives.


**Future work 2**: These steps are part of the editorial effort that editors have to perform manually.
Therefore, this process is a candidate to be automated and integrated in the toolchain.









