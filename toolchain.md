# Toolchain for publishing data specifications


## Motivation

To support the editors in creating and maintaining data specifications in a coherent manner, tooling is required.

Data specifications have their own life cycle. 
The various Core Vocabularies are created by different (editorial) teams, with different Working Groups, at different times.
In the past, the manual editing has resulted in similar, yet distinct, and sometimes incoherent, expressions of these Core Vocabularies.
A situation that raised many questions by the consumers.

To have the data specifications progress in the same way, and following the same style, tooling support is required. 
Introducing tooling will force the editors to follow a predefined editorial flow, and thus reduce their editorial freedom to the limits of the tooling.
This limitation brings, however, crucial benefits for the SEMIC project:
  - a harmonised coherent experience of the data specifications. This will increase the adoption by the consumers.
  - the embedding of the key SEMIC data modeling in formal processes, instead of relying solely on the experience of the editors.
  - support scaling up the editorial capacity. Automation provides the ability to learn the editorial flow in a safe environment.


In this chapter, the tooling that is supporting the editorial flow for managing data specifications is described.
First the design and how it is setup in SEMIC space is described.
Then frequently asked questions by the editors and developers are answered.


	

## Setup & Design


The toolchain used in the SEMICeu project is based on the [OSLO toolchain](https://github.com/Informatievlaanderen/OSLO-toolchain/tree/master/doc-generic).

The OSLO toolchain is part of a larger environment for supporting the generation, maintenance and publication of data specifications under the governance of the Flemish Government, Belgium.
Because OSLO has been participating in SEMIC from the start, the toolchain incorporates many advices and best practices SEMIC has produced or applies.
This is especially true for the support of the editorial flow. 
The main distinction situates at the publication approach: the current SEMIC practice is to use github as publication platform where per data specification a repository is created, while the OSLO toolchain has been designed with a single publication environment in mind.

In the [editorial flow](./editor.md) this distinction is visible in the manual publication steps the editor has to perform; steps that are not required in the OSLO context. This is future work to adapt the tooling to the SEMIC publication context.

The result from the OSLO toolchain can be seen at [data.vlaanderen.be](https://data.vlaanderen.be).
Tooling source code and data specifications are all publicly available on [GitHub](https://github.com/search?q=org%3AInformatievlaanderen+topic%3Aoslo).


### Generic Design

The high level design OSLO toolchain is illustrated in the figure below.

![./images/high-level-design.jpg](./images/high-level-design.jpg)

The objective is to automate the publication of the data specifications on a publication environment.
A _publication environment_ is a website identified by a domain. 
The content of that website can be (and usually is) broader than the data specifications, but the toolchain is solely concerned with the publication of the data specifications.
The toolchain is designed to create a static website, i.e. a collection of webpages.
This design choice simplifies the operational work to serve the data specifications on the publication environment, but also more importantly it provides the editors with a exact view on what is being shared with the consumers on the publication environment.

The source code of the static website, i.e. the publication environment, is stored on GitHub in the _publication repository_.
The result of the generation process, i.e. the static website, is stored in the _generated repository_. 
A _publication_ repository is thus always paired with a _generated_ repository. 
The generated repository is kept in sync with the publication repository via a CI/CD execution flow. 
Each change (commit) to the publication repository will after a successful CI/CD execution lead to a change in the generated repository.

Using the branching functionality of Github repositories, system staging, i.e. publishing on development, testing and production publication environments, is supported. 


To provide the editorial freedom to let data specifications have their own life cycle, the source of a data specification is stored in their own repository. 
These repositories are called _thema repositories_. 
The publication repository contains a list of references to the thema repositories.
More precisely it are references to a unique point in time, i.e. a commit.
These references are called publication points.
Editors primarely interact with thema repositories, only when a new publication of the data specification is required they update the publication repository with a new publication point.
This setup creates flexibility and provides editorial scaling potential, without loosing a central control. 

***Roadmap note***:
The OSLO toolchain has been developed throughout the past lustrum driven by the local needs and the experiences from the editors.
It is under active maintenance by the Flemisch Government.
Roughly yearly a new main release is done.
At the moment (May 2022) the release 3.0 is the latest, and 4.0 is under development.
The new development involves, among others, a rewrite of the key component EA-to-RDF, i.e. the UML information extraction tool, and activities to facilitate use beyond the original setting. 
Documentation is added and tools are more streamlined.

For more information on the OSLO toolchain tools, the OSLO maintainers can be contacted. 
This can be via posting a github issue or via email on digitaal.vlaanderen@vlaanderen.be.


The deployment of the above design is supported with two template repositories.
 - _template for a publication repository_ [https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template).
 - _template for a thema repository_ [https://github.com/Informatievlaanderen/OSLOthema-template](https://github.com/Informatievlaanderen/OSLOthema-template)

The generated repository does not require a template.

After creating the publication repository from the template the publication repository must be paired with the generated repository. 
Documentation how to this and more configuration options are found in the documentation that is part from of the template.


#### Glossary
- a _thema_ repository - A repository that contains the source content of one or more data specifications. 
- a _publication_ repository - A repository associated with a publication environment. It contains the source of the static website published by the publication environment.
- a _generated_ repository - The repository that contains the result of processing the publication repository using a CI/CD flow.





### SEMIC setup


[img] 

In contrast to the OSLO toolchain premisse of a single publication environment, i.e. a single website, SEMIC has decided to apply a decentralised publication strategy. 
Each data specification repository in the SEMICeu space is not only the source of the specification, but also the publication platform for that data specification by using GitHub pages service offering. 

In the OSLO toolchain terminology it means that each SEMICeu data specification repository functions as the pair publication and generated repository and aswell as a thema repository.
Instead of applying the OSLO toolchain setup to each SEMICeu data specification, the toolchain has been deployed in the assumption there is one SEMIC publication environment despite this technically is not the case.
This deployment corresponds to a minimalistic setup providing already the most important editorial support for creating harmonised artefacts for all data specifications.

In the SEMICeu GitHub space the toolchain has been deployed in these repositories:

- [https://github.com/SEMICeu/uri.semic.eu-publication](https://github.com/SEMICeu/uri.semic.eu-publication) - the _publication_ repository
- [https://github.com/SEMICeu/uri.semic.eu-generated](https://github.com/SEMICeu/uri.semic.eu-generated) - the _generated_ repository
- [https://github.com/SEMICeu/uri.semic.eu-thema](https://github.com/SEMICeu/uri.semic.eu-thema) - a _thema_ repository that currently contains _all_ the SEMIC data specifications. This choice can be revisited in the future.
All editing happens on the _master_ branch as there are no staging publication environments.


Within the SEMICeu GitHub space, these repositories are **private** GitHub repositories. 
This influences the execution and configuration as operating on private repositories is a differrent GitHub API request than those which can be used for public GitHub repositories.
More information this and the configuration can be found in the [publication environment documentation](https://github.com/SEMICeu/uri.semic.eu-publication/blob/master/config/README.md).

How these repositories feature in the management of data specifications is elaborated in the [editorial flow](./editor.md).

This setup does not provide the end-to-end experience of the original design, but it is feasible that the CI/CD flow can be adapted to achieve this.


----
The URLs for the data specifications to be consulted by the consumers are therefore strongly connected with the repository namegiving and structure.
The design should also investigate the issue of the publication of the common domain `http://data.europa.eu/m8g`. 
----


### (Software) Components

This section lists the main software components involved in the toolchain of which the editors and developers should be aware. 

They are:

- UML editing tool: Enterprise Architect from Sparx systems 
- Source Control System: [GitHub](https://github.com)
- Continuous Integration/Continous Deployment: [CircleCI](https://circle.com)
- OSLO toolchain tools:
    - content extraction tool from UML document: [EA-to-RDF](https://github.com/Informatievlaanderen/OSLO-EA-to-RDF/tree/multilingual)
    - artefact generators: [specgenerator](https://github.com/Informatievlaanderen/OSLO-SpecificationGenerator/tree/multigual-dev)
    - template for a publication repository [OSLO-publicationenvironment-template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template).
    - template for a thema repository [OSLOthema-template](https://github.com/Informatievlaanderen/OSLOthema-template)

Commercial fees are only required for Enterprise Architect.
The others have a free tier (to which the objectives of this work complies) or are Open Source components.



## Editors HowTo


### HowTo add a new data specification 

There are basically two approaches to initiate a new data specification, each them addressing a different objective.
The first is creating a full fresh start with a new _thema_ repository. 
The advantages and reasons for this choice are that the changes to the GitHub repository reflect the (editorial) changes to data specification. 
They are thus not mixed with the changes to other data specifications. 
If the new data specification is an extension or will be part of the common maintenance (e.g. common versioning and publication history) of an existing collection of data specifications, then these should be present in the same GitHub repository.

For instance, if each Core Vocabulary is considered a subpart of the common data model, the Common Core Vocabularies, and the release policy is that a change in the one element will increase the release version number for all individual Core Vocabularies, then a single _thema_ repository is a good choice.
When each Core Vocabulary has a totally independent release and maintenance flow, with distinct version numbering ( e.g. CCCEV is 2.1.4 and Core Person is 3.2.4) then distinct _thema_ repositories are adviced.
The release and maintenance processes evolve over time, therefore the organisation of the _thema_ repositories can change over time.

#### An new _thema_ repository

The OSLO-toolchain has prepared a _thema repository template_ [https://github.com/Informatievlaanderen/OSLOthema-template](https://github.com/Informatievlaanderen/OSLOthema-template). 
Use this to create an initial _thema_ repository in the SEMIC space.
Mark the new repository as private.

The repository is ready to be used but it is advised to create quickly the minimal context and configuration relating to the target data specification.
And to remove as much as possible the not necessary boilerplate configuration with sensible values for SEMIC.



#### As part of an existing _thema_ repository

In this case the user has to step wise add the necessary configuration and data related to the data specification {DATASPEC}.
Either by copying the boilerplate values found in https://github.com/Informatievlaanderen/OSLOthema-template, or by copying the values from another data specification in the _thema_ repository.

The current minimal steps are:

1. add config file {DATASPEC} for the data specification in {THEMAREPO}/config/{DATASPEC}.json 
2. add the UML document  {THEMAREPO}/{DATASPEC}.eap
3. add the stakeolder information {THEMAREPO}/stakholders.csv
4. add the html template information {THEMAREPO}/templates/{DATASPEC}.j2
5. add the directory {DATASPEC} for additional information in the html representation: {THEMAREPO}/site-skeleton/{DATASPEC}

***TIP***: if the directory is empty, add an empty file called .gitignore to the directory, to ensure the directory is included in the repository.

### HowTo add/update a term to/in a data specification

Adding or updating a term to/in a data specification is a UML modeling task. 
It does not involve manipulating any other data.

The editor thus updates the UML model in Enterprise Architect, and commits the changed file to the _thema_ repository.
To trigger the artefact generator, the corresponding publication point has to be adapted in the publication environment.

The rules for manipulating the UML model can be found []().

### HowTo trigger the generation of the artefacts

Triggering the generation of the artefacts is done via changing the _publication_ repository. 
When a change is committed to the _publication_ repository, CI/CD process (CircleCI) is initiated which produces the artefacts.
The result of the generation process is stored in the _generated_ repository.

A commit to the _thema_ repository is _not_ triggering the generation process. 
An editor can thus improve incrementally the content in the _thema_ repository, without being forced to generate each time the artefacts.
Ony when needed the editor will trigger the generation process.

The usual commit for triggering the generation process is changing the publication point corresponding to the data specification the editor.
Guidelines on how to create and maintain publication points are found in the _publication_ repository.


### HowTo track errors

The editorial process is a continuous process of improvements.
Errors or mistakes can be either data specification related, either the result of a technical error in the processing.

The first are in general only detectable by the data specification readers. 
For instance, a definition set to be "TODO definition" by the editor is technically a valid string, but from a data specification incorrect.
Spotting these kind of errors/mistakes/issues are the responsability,  in the first place,  of the editor but in general of the whole working group.
The tooling will only facilitate the propagation of the correction throughout all artefacts.

A second category are when the artefacts yield unexpected content (being the presence or absence of data). 
This might be caused by a bug in the artefact generator, or the result of a mis-configuration (of the artefact generator).
Check if the same unexpected content is present for other data models, not under your responsability. 
If that is the case, then the issue is probably a "feature" of the artefact generator. 
Otherwise, it might be a wrong configuration which can be checked by comparing with a data model configuration for which the artefact is as expected.
Usually the issue can be efficiently analysed by a developer, as technical experience enable quick tracing of the problem.

The last category are errors that are due to a technical error in the processing. 
The source can be inside or outside the toolchain.
E.g. GitHub is not accessible in the organisation.
The variation of these errors require thus developer knowledge, to assess and react to the issue.

The toolchain foresees in error reporting and user feedback in 2 major channels:
 - via the _generated_ repository
 - via the CircleCI interface

When the artefact generation is successful, i.e. technically successful, the _generated_ repository contains the intermediate processing data including logs from the artefacts generators in the directory `report`. In SEMIC it is [here]().
A successful execution is thus equivalent with a commit to the _generated_ repository where the content of the publication point is updated to reflect the change done by the editor.
To know if the issue is a content issue (category 1) or an artefact generator issue (category 2) the report directory contains the aggregated content, serialised as a json file, produced in the aggregation phase. 
If the content is present in the aggregated file, then the issue is most likely a category 2 issue. 

When there is no commit present, then the CircleCI processing might be terminated.
To check this open in the CircleCI UI the execution trace for this repository and corresponding branch.
A failed step is indicated clearly, and this forms the starting point of the investigation.
The logged messages are verbose, and normally provide sufficient context to find the source. 
However in some cases, it is more efficient to rerun the step with SSH active and investigate the processing with the data by connecting through SSH to the CircleCI step. 
This requires developer knowledge.
Note that the log messages are targetting developers, not editors. 
The business validation errors are always collected and committed to the _generated_ repository. 
Most editors will therefore use CircleCI to follow the progress of the artefact generation or to understand how their commit to the publication environment triggered a processing error.

Since the toolchain is based on versioned services, a complete block of the execution of the toolchain can _always_ be resolved by reverting to the last correct operational situation in the (_publication_) repositories. 
This are normal GitHub operations, therefore even editors are capable to realise this.


### HowTo know which repository is connected a data specification 
When dealing with issues for a data specification, tracking the data specification to its source is a common issue.
For that the editor has to create a (mental) map crossing different repositories, which is helped by built-in features of the toolchain.

The toolchain will always add the 
   - commit hash code for the publication environment that triggered the generation of the artefact, and
   - commit hash code for the _thema_ repository from which the artefact is generated
to the aggregated content.
Per default, this is part in the html representation as a html link to the _thema_ repository pointing to the source of the data specification.

This allows to exactly know the (UML) content on which the data specification is based. 
Even more, git history provides an undeniable ledger of which changes that have resulted in this state.

In SEMIC, where the publication of the artefacts is done manually by copying the generated artefacts to the corresponding Core Vocabulary GitHub repositories, adding this information (even hidden) is aiding the tracing.


## Developers HowTo

### HowTo find the source code of the automation

The source code for the CircleCI automation is part of the repository [uri.semic.eu-publication](https://github.com/SEMICeu/uri.semic.eu-publication). 
The organisation and setup of the workflow of the CircleCI workflow is extensively documentated in the _template_ repository [OSLO-publicationenvironment-template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template).

The CircleCI workflow will executes in some steps software available as public Docker images. 
These images are build from the open source repositores 
  - [OSLO-EA-to-RDF](https://github.com/Informatievlaanderen/OSLO-EA-to-RDF)
  - [OSLO-Specificationgenerator](https://github.com/Informatievlaanderen/OSLO-SpecificationGenerator)


### Howto add a new artefact generator

An artefact generator is a tool that transforms the intermediate aggregated json structure to the desired artefact. 
It has as input a json file and any additional tool configuration parameters and produces the artefact as a file.
In the repository [OSLO-Specificationgenerator](https://github.com/Informatievlaanderen/OSLO-SpecificationGenerator) collects the OSLO artefact generators.
These are all written in javascript. 
A test suite is available in the repository, illustrating the usage of each artefact generator w.r.t. different parameter choices.

Adding a new artefact generator in that repository is thus the following process in short:
   - create a new tool as a new javascript tool
   - add the test suite
   - build and publish a new docker image
   - integrate the execution in the CircleCI workflow in a configured publication environment
   - test the result

When the artefact generator has reached maturity add the additional generation possibility as part of a new version for
[OSLO-publicationenvironment-template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template) to share your work with the community.


### Howto modify/improve an artefact generator

The process to update an artefact generator follows the same process as adding a new one.


