# Toolchain for publishing data specifications


## Motivation


To support the editors in creating and maintaining data specifications ([*](./glossary.md#data_spec), [**](./glossary.md#sem_web), [***](./glossary.md#reg_test), [****](./glossary.md#cd_ci), [*****](./glossary.md#shacl), [******](./glossary.md#xsd))in a coherent manner, tooling is required.
Data specifications have their own life cycle. 
The various Core Vocabularies are created by different (editorial) teams, with different Working Groups, at different times.
In the past, the manual editing has resulted in similar, yet distinct, and sometimes incoherent, expressions of these Core Vocabularies.
A situation that raised many questions by the consumers.

To have the data specifications progress in the same way, and following the same style, tooling support is required. 
Introducing tooling will force the editors to follow a predefined editorial flow, and thus reduce their editorial freedom to the limits of the tooling.
This limitation, however, brings crucial benefits for the SEMIC project; namely, it will:
  - provide a harmonised, coherent experience of the data specifications. This will increase the adoption by the consumers.
  - allow the embedding of the key SEMIC data modelling best practices in formal processes, instead of relying solely on the experience of the editors.
  - support scaling up the editorial capacity. Automation provides the ability to learn the editorial flow in a safe environment.


This chapter describes the tooling that is supporting the editorial flow for managing data specifications.
It focusses on the interplay between the different repositories, and how editors can use it to generate the data specification artefacts.
First, we present an overview of the overall design of the toolchain, and we describe how it is set up in the SEMIC space.
Then, we provide some useful information about the use of the toolchain, by answering a few frequently asked questions asked by the editors and developers.
The artefact generation itself is documented in a chapter on [artefact generation](./artefact_generation.md).



## Setup & Design


The toolchain used in the SEMICeu project is based on the [OSLO toolchain](https://github.com/Informatievlaanderen/OSLO-toolchain/tree/master/doc-generic).

The OSLO toolchain is part of a larger environment for supporting the generation, maintenance and publication of data specifications under the governance of the Flemish Government, Belgium.
Because OSLO has been participating in SEMIC from the start, the toolchain incorporates many advices and best practices SEMIC has produced or applies.
This is especially true for the support of the editorial flow. 
The main distinction between the use of the toolchain in the two environments is regarding their approach to publication. The current SEMIC practice is to use GitHub as publication platform, where each data specification is edited and published in its own repository. On the other hand, the OSLO toolchain has been designed with a single publication environment in mind.

In the [editorial flow](./editorial_flow.md) this distinction is indicated by the existence of the manual publication steps that the editor has to perform; steps that are not required in the OSLO context. It is future work to adapt the tooling to the SEMIC publication context.

The result produced by the OSLO toolchain can be seen at [data.vlaanderen.be](https://data.vlaanderen.be).
The source code of the tooling, as well as of the data specifications are all publicly available on [GitHub](https://github.com/search?q=org%3AInformatievlaanderen+topic%3Aoslo).


### Generic Design

The high level design of the OSLO toolchain is illustrated in the figure below.

![./images/toolchain-generic.jpg](./images/toolchain-generic.jpg)

The objective is to automate the publication of the data specifications on a publication environment.
A _publication environment_ is a website identified by a domain. 
The content of that website can be (and usually is) broader than the data specifications, but the toolchain is solely concerned with the publication of the data specifications.
The toolchain is designed to create a static website, i.e. a collection of webpages.
This design choice simplifies the operational work to serve the data specifications on the publication environment, but more importantly it also provides the editors with an exact view on what is being shared with the consumers on the publication environment.

The source code of the static website, i.e. the publication environment, is stored on GitHub in the _publication repository_.
The result of the generation process, i.e. the static website, is stored in the _generated repository_. 
A _publication_ repository is thus always paired with a _generated_ repository. 
The generated repository is kept in sync with the publication repository via a [Continuous Integration/Continuous Development](https://en.wikipedia.org/wiki/CI/CD) (CI/CD) execution flow. 
Within software engineering, CI/CD is the name for any automated process supporting the software building and deployment activities.
Each change (commit) to the publication repository will lead after a successful CI/CD execution to a change in the generated repository.

Using the branching functionality of Github repositories, system staging (i.e. publishing on development, testing and production publication environments) is also supported. 


To provide the editorial freedom and to let data specifications have their own life cycle, the source of each data specification is stored in their own repository. 
These repositories are called _thema repositories_. 
The publication repository contains a list of references to the thema repositories.
More precisely, they contain references to the state of the thema repositories at unique points in time, i.e. commits.
These references are called __publication points__.
Editors primarily interact with thema repositories, only when a new publication of the data specification is required, when they update the publication repository with a new publication point.
This setup creates flexibility and provides editorial scaling potential, without loosing a central control. 


For more information on the OSLO toolchain tools, the OSLO maintainers can be contacted. 
This can be done by posting a github issue, or contacting them via email at digitaal.vlaanderen@vlaanderen.be.

The deployment of the above design is supported by the existence of two template repositories.
 - a _template for a publication repository_ - available at: [https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template).
 - a _template for a thema repository_ - available at: [https://github.com/Informatievlaanderen/OSLOthema-template](https://github.com/Informatievlaanderen/OSLOthema-template)

The generated repository does not require a template.

After creating the publication repository from the template, the publication repository must be paired with the generated repository. 
Documentation on how to do this, as well as more configuration options, are found in the documentation that is part of the [template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template/tree/main/config).



### SEMIC setup

In contrast to the OSLO toolchain premise of a single publication environment, i.e. a single website, SEMIC has decided to apply a decentralised publication strategy. 
Each data specification repository in the SEMICeu space is not only the source of the specification, but also the publication platform for that data specification, by using  [GitHub Pages](https://pages.github.com/) service offering. 

The OSLO toolchain separates the different functionalities (master data source, content generation, publication) in separate repositories, making it then natural to combine the processing of multiple data specifications into a pair of publication and generated repository. 
Since there is no unique SEMIC publication environment identified with a unique domain, there are two alternatives to use the toolchain. (a) Integrate in each SEMIC data specification repository the toolchain functionalities. 
Or (b) deploy the toolchain in new SEMICeu repositories, pretending there is a single SEMIC publication environment. 
The second option has been chosen as it impacted the existing data specification repositories the least, and it deviates the least from the OSLO toolchain setup.
The deployment corresponds to a minimal setup, providing already the most important editorial support for creating harmonised artefacts for all data specifications.

In the SEMICeu GitHub space the toolchain has been deployed in these repositories:

- [https://github.com/SEMICeu/uri.semic.eu-publication](https://github.com/SEMICeu/uri.semic.eu-publication) - the _publication_ repository
- [https://github.com/SEMICeu/uri.semic.eu-generated](https://github.com/SEMICeu/uri.semic.eu-generated) - the _generated_ repository
- [https://github.com/SEMICeu/uri.semic.eu-thema](https://github.com/SEMICeu/uri.semic.eu-thema) - a _thema_ repository that currently contains _all_ the SEMIC data specifications. This choice can be revisited in the future.
All editing happens on the `master` branch as there are no staging publication environments.


Within the SEMICeu GitHub space, these repositories are **private** GitHub repositories. 
This influences the execution and configuration, as operating on private repositories requires different GitHub API requests than those that can be used with public GitHub repositories.
More information on this, and other aspects related to the configuration, can be found in the documentation of the [publication environment](https://github.com/SEMICeu/uri.semic.eu-publication/blob/master/config/README.md).

How these repositories are used in the management of data specifications is elaborated in the [editorial flow](./editorial_flow.md).

This setup does not provide the end-to-end experience of the original design, but it is feasible that the CI/CD flow can be adapted to achieve this.



#### Thema repository(ies)

The deployment of the toolchain resulted in a simplified setup with a _single_ thema repository. 
This choice has been made to facilitate the ongoing harmonisation of the Core Vocabularies and to ensure that future contractors will have everything at their disposal to perform changes.
One can consider the current SEMIC thema repository as the shared space to have the toolchain functioning.

However, this choice might need to be reconsidered in the future, if we want to support editors even better. 
The toolchain is designed to work with multiple thema repositories.
To organise the SEMIC data specifications in multiple thema repositories the following considerations can best taken into account:

  - It is best to group all data specifications that are defining PURIs in the same namespace in one thema repository. 
    Like this the risk for creating overlapping concepts is reduced, and the impact of a change on a URI is more visible.
  - It is best to decide a branching and tagging strategy within the thema repository. E.g. each data specification could be hosted on a separate branch.

Note that the some options might be blocked by past decisions. 
For instance, the PURI design influences strongly the grouping. 
I.e. the PURIs in the domain `http://data.europa.eu/m8g` form a global space and therefore all data specifications that create PURIs in this domain are best maintained together.
Modularity in the PURI design will thus also facilitate modularity in the data specification management.

Besides the "quick win" motivation, none of the above considerations have been discussed in depth. 
They are part of future work to bring further improvments to the editorial flow, and must be done in collaboration with the whole SEMIC team.



#### (Software) Components

This section lists the main software components involved in the toolchain which the editors and developers should be aware of. 

They are:

- UML editing tool: [Enterprise Architect from Sparx systems](https://www.sparxsystems.eu/enterprise-architect)
- Source Control System: [GitHub](https://github.com)
- Continuous Integration/Continuous Deployment: [CircleCI](https://circle.com)
- OSLO toolchain tools:
    - UML content extraction tool: [EA-to-RDF](https://github.com/Informatievlaanderen/OSLO-EA-to-RDF/tree/multilingual)
    - artefact generators: [OSLO Specification Generator](https://github.com/Informatievlaanderen/OSLO-SpecificationGenerator/tree/multigual-dev)
    - template for a publication repository: [OSLO-publicationenvironment-template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template)
    - template for a thema repository: [OSLOthema-template](https://github.com/Informatievlaanderen/OSLOthema-template)

Commercial fees are only required for Enterprise Architect.
The others have a free tier version (to which the objectives of this work complies) or are Open Source components.

Users should have an GitHub account. That GitHub account grants access also to CircleCI.


## Editors HowTo

### HowTo trigger the generation of the artefacts

Triggering the generation of the artefacts is done via changing the _publication_ repository. 
When a change is committed to the _publication_ repository, a CI/CD process is initiated which produces the artefacts.
The result of the generation process is stored in the _generated_ repository.

A commit to the _thema_ repository is _not_ triggering the generation process. 
An editor can thus improve incrementally the content in the _thema_ repository, without being forced to generate each time the artefacts.
Only when needed will the editor trigger the generation process.

The usual change to the publication repository for triggering the generation process consists of changing the publication point corresponding to the data specification that has been edited.
A publication point is a reference to a data specification in a _thema_ repository.
An example is shown below:
```
{
    "urlref": "/doc/core-vocabulary/core-person",
    "repository": "git@uri.semic.eu-thema:SEMICeu/uri.semic.eu-thema.git",
    "branchtag": "4629f50dbb5953284f83bda9321305bfeb2f7da7",
    "name": "core-person-ap",
    "filename": "config/core-person.json",
    "navigation": {}
  },
```
An elaborated description of the structure and semantics of the attributes is found in the [_publication_ repository](https://github.com/SEMICeu/uri.semic.eu-publication).
Intuitively, the above publication point can be read as the following processing instruction: "Write in the generated repository, at path `{urlref}`, the generated artefacts for the data specification `{name}`, according to config file `{filename}` located in `{repository}` as of the commit `{branchtag}`."
Thus, since changing the data specification content is changing the thema repository, a change in the publication point can correspond to changing the `{branchtag}` to point to the new content. 
Performing this change will trigger the generation of the artefacts.


Besides technical expectations, such as the repository should be a GitHub repository, the toolchain does not impose editorial management rules on a publication point's structure.
For instance, SEMIC could impose rules for the name-giving of the filenames, urlref path structure, and branchtags, but SEMIC could also impose a correspondence between the branchtag and the urlpath structure.
This is future work, and should be considered in the context of further integrating the toolchain in the publication process.



## Developers HowTo

### HowTo find the source code of the automation

The source code for the CircleCI automation is part of the repository [uri.semic.eu-publication](https://github.com/SEMICeu/uri.semic.eu-publication). 
The organisation and setup of the workflow of the CircleCI workflow is extensively documentated in the _template_ repository [OSLO-publicationenvironment-template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template).

The CircleCI workflow will execute in some steps software available as public Docker images. 
These images are build from the open source repositories 
  - [OSLO-EA-to-RDF](https://github.com/Informatievlaanderen/OSLO-EA-to-RDF)
  - [OSLO-Specificationgenerator](https://github.com/Informatievlaanderen/OSLO-SpecificationGenerator)



