# Documentation
This repository contains the overview documentation describing the resources and tools developed and used by the Semantic Interoperability Community ([SEMIC](https://joinup.ec.europa.eu/collection/semantic-interoperability-community-semic)).

The [SEMICeu GitHub space](https://github.com/SEMICeu) is created to support the Semantic Interoperability Community with the creation of __data specifications__ (e-Government Core Vocabularies, Application Profiles, etc.). A list of these data specifications can be found [on the SEMIC website](https://joinup.ec.europa.eu/collection/semantic-interoperability-community-semic/our-resources). This documentation describes both how the different SEMIC resources are organized in GitHub repositories, as well as what are the supporting assets that need to be _set up_, _configured_, and _used_ to realise (i.e. edit and publish) such SEMIC data specifications.

This documentation covers the state of affairs as of May 2022.
The objective is that readers of this documentation are provided with sufficient achors to initiate mastering the methods and tooling used to create and manage data specifications.




## Table Of Contents
1. [Historical Background](#historical-background)
2. [User Roles and Activities](#user-roles-and-activities)
3. [Organisation of the SEMIC GitHub Space](#organisation-of-the-semic-github-space)
4. [Toolchain](./toolchain.md)
5. [Datamodel](./datamodel.md)
6. [Persistent URIs](./puri.md)


## Historical Background

The creation of data specification is an activity that involves design decisions regarding two aspects:

- Creation or generation of the artefacts
- Publication of the artefacts

These activities are connected, but require different tools and methods.
In some organisations it might be decided that these activities are performed by different teams. In SEMIC they are performed by the same team, however the connection between the two activities has <u>not</u> been (fully) automated, yet.
This has historic reasons. 
SEMIC has started with managing data specifications independently, by independent editorial teams producing artefacts manually.
Step by step, in the past 10 years, more harmonisation occurred.
The tooling documented hereby is a further step towards an integrated and automated flow between the creation and the publication of the artefacts.
Nevertheless, the current design of the architecture is a reflection of the organic growth of the system, during which a number of best possible decisions have been taken in order to minimize the impacts on the existing processes and methods.


## User Roles and Activities

There are three main types of __actors__ that will interact with the resources and assets produced and managed by SEMIC on the SEMICeu GitHub space: the data specification _consumers_, the data specification _editors_, and the supporting asset _developers_. These roles are elaborated on the [Actors](./actors.md) page.
The connection between these three group of actors is the following: The tools and methods are set up by the _developers_ to support the _editors_ in their work to provide together a coherent experience to the _consumers_.

Since the consumers are the "end users" of the data specifications, they will not need to interract directly with the SEMICeu GitHub space. Therefore, this documentation will only focus on the _editors_ and _developers_, as they constitute its target audience.

### The editing of the artefacts

Data specifications are subject to evolution. 
This evolution is the result of addressing the use cases provided by the SEMIC community to data specifications.
In that editorial process editors are adapting the data specification: i.e. the artefacts that are part of the data specification.

The assessment how to best address the use case is beyond this documentation. 
Nevertheless, this documentation provides insights in how a resolution is integrated in the published artefacts of the data specification.

Thus to adequately respond to the use case, editors should understand how to operate the [toolchain](./toolchain.md) to efficiently create the artefacts for a data specification. 


### Publication of the artefacts

The general idea is to publish each data specification in a human readable form (e.g. HTML) together with other supportive representations (JSON-LD context files, SHACL shapes, RDF vocabularies, etc.). 
The expectations, representations, and content has evolved over time, but has never been written out in a specification (e.g. style guide). Instead, through community feedback and the experience of the SEMIC editors an implicit expectation has been realised. 

Today the process adopted by SEMIC has evolved to using GitHub, one repository per data specification. 
Over the past years, the organisation and structure of these repositories underwent a gradual harmonisation process.

Since these repositories were created before an automated artefact generation tooling was applied, the repositories are set up and organised with the assumption that the content of the repository is manually created. 
Each repository has an individual lifecycle.

For the editors, who are expected to keep the coherency between different repositories, this constitutes a serious challenge. 
Although it seems simple to follow the rule that "when change _A_ is applied to repository _R1_, then apply the same change _A_ to repository _R2_", in reality this ends up being errorprone. 
In particular, when editors are collaborating, or are replaced over time, such knowledge gets lost.
An automated tooling that is able to propagate the same change over two data specification will ensure consistency.

A first step to support editors producing coherent cross-repository artefacts, is the deployment and use of a common __data specification generation tool__.
 
The tooling provides support for the common editorial challenges:
   - how to initiate a new vocabulary
   - how to add/modify a term to a vocabulary
   
but also for the presentation challenges:
   - how to change the presentation of a vocabulary
   - how to adapt generated artefacts
   - how to add new artefacts 

The [Toolchain](./toolchain.md) page provides the explanation on the technical setup and operation of the tooling.
Understanding the technical setup requires the understanding of what a [data model](./datamodel.md) is, and how [persistent identifiers](/puri.md) are used.

Whereas the tooling addresses the generation of the artefacts to be published, the publication activity is a manual step. 
The editor has to _manually_ copy the resulting artefacts to the appropriate location. 



## Organisation of the SEMIC GitHub Space

The SEMIC GitHub space contains several dozens of repositories, each falling in specific categories. There are data specification repositories, repositories supporting the generation and publication of the data specifications, and others. 


### Data specification repositories

The data specification repositories are tagged with the topic ***data-specification***.
The full list of SEMICeu repositories tagged with ***data-specification*** can be found [here](https://github.com/search?q=org%3ASEMICeu+topic%3Adata-specification).


#### Core Vocabulary repositories

A subset of the data specification repositories that are set up for the editing of Core Vocabularies is tagged with the topic ***core-vocabulary***.
[Here](https://github.com/search?q=org%3ASEMICeu+topic%3Acore-vocabulary) is the current list of Core Vocabulary repositories.

The Core Vocabulary repositories (e.g. [Core Person Vocabulary](https://github.com/SEMICeu/Core-Person-Vocabulary/)) are organised as follows:

- Webinars : any documentation, meeting minutes, recording relating to a webinar on the data specification
- Releases : the data specification releases, organised per version. Each release is identified by its version number, and has a dedicated subfolder.  The content of a specific data specification release version folder (e.g. [version 2.00 of the Core Person Vocabulary](https://github.com/SEMICeu/Core-Person-Vocabulary/tree/master/releases/2.00)) is not fixed.
The structure of the latest release will be conform to the setup of the artefact generating [toolchain](/toolchain.md). 
It is assumed that there is an `index.html` file, as the data specification is then rendered using GitHub Pages, a free service for public open source GitHub repositories (e.g. for the Person Core Vocabulary it would be published at [https://semiceu.github.io/Core-Person-Vocabulary/releases/2.00/](https://semiceu.github.io/Core-Person-Vocabulary/releases/2.00/)).

More governance agreements are not made.

#### Application Profile repositories

The data specification repositories are tagged with the topic ***application-profile***.
[Here](https://github.com/search?q=org%3ASEMICeu+topic%3Aapplication-profile) is the current list of application profile repositories.

Some application profile repositories will follow the same organisational structure as the Core Vocabularies, but others follow a different structure.
This has historic reasons.

When a new release for these Application Profiles is being prepared, restructuring the content in accordance to the above described structure is highly recommended.


### Repositories for Supporting Generation and Publication of Data Specifications

The repositories that provide the support for generating and publishing data specifications are tagged with the topic ***tooling***.
The full list of these repositories can be found [here](https://github.com/search?q=org%3ASEMICeu+topic%3Atooling).

These repositories have no common organisational structure, however their `README.md` file should provide a good overview about their organisation and usage.
Also, the [Toolchain](./toolchain.md) page can offer additional information about what these tools are meant to do and when and how to use it. 







```
Use Cases or “How-Tos”would be helpful, e.g.
detailed examples such as the flow from UML to final xsd, including the intermediate steps like what has to be done with references etc.
change an existing element in a vocabulary
  -> toolchain.md
add a new element to an existing vocabulary
  -> toolchain.md
delete an element in a vocabulary
  -> datamodel.md
design decision: Are there alternatives for Enterprise Architect (to model UML) and circleci (as built tool)? 
  -> toolchain.md
is it planned to offer a public PURI request service?
  -> puri.md
the PURI part of the ToolChain is mainly focused on technical issues: http/https, URL rewriting, Docker, etc.
semantic aspects are not discussed at all.
  -> puri.md (note that semantical discussion on puris somehow part of the background knownledge)

·       What is the role of each java script file? Is there a dedicated java script file for every different serialization?
  -> yes
·       Where the different rules for the creation of the xsd serialization are defined and how they can be modified?
  -> in the javascript tool there is an implementation from the rules expressed in confluence.

·       What is the minimum set of tools and files taken for the ones provided by OSLO so that SEMIC can perform its job?
  -> that is up to SEMIC to decide

·       How can I create a copy of the OSLO github and run the toolchain from an virtual image locally and how I can run it through github environment?
  -> github forking/cloning.

Clear definition of the different roles and prerequisite knowledge/skills.
-> Readme.md
Do the tools that are used at the moment meet the needs of the end-user (editor role and/or others)? An even one more basic level: What does the end-user need? What are his/her skills and knowledge.
-> Readme.md

What is already in use by the final user (editor and member of the WG) that can be re-used as tools to promote acceptance? Basic ideas on the perspective of the end user as a stakeholders, for example git, in terms of training.
-> no formal training exists. Same situation as before in the last 10 years.

How can the quality of the tools be ensured?
-> By collaboration as it is open source.

How can errors be created or fixed (e.g. the various issues in the Person XSD schema)?
-> By "artefact-generation" improval process
   -> toolchain.md 

What is open source?  
-> all components except Enterprise architect
```


