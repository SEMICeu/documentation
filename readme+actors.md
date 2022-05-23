# Documentation
This repository contains the overview documentation describing the resources and tools developed and used by the Semantic Interoperability Community ([SEMIC](https://joinup.ec.europa.eu/collection/semantic-interoperability-community-semic)).

The [SEMICeu GitHub space](https://github.com/SEMICeu) is created to support the Semantic Interoperability Community with the creation of __data specifications__ (e-Government Core Vocabularies, Application Profiles, etc.). A list of these data specifications can be found [on the SEMIC website](https://joinup.ec.europa.eu/collection/semantic-interoperability-community-semic/our-resources). This documentation describes both how the different SEMIC resources are organized in GitHub repositories, as well as what are the supporting assets that need to be _set up_, _configured_, and _used_ to realise (i.e. edit and publish) such SEMIC data specifications.

This documentation covers the state of affairs as of May 2022.
The objective is that readers of this documentation are provided with sufficient achors to initiate mastering the methods and tooling used to create and manage data specifications.




## Table Of Contents
1. [Historical Background](#historical-background)
2. [User Roles](#user-roles)
3. [Activities](#activities)
4. [Organisation of the SEMIC GitHub Space](#organisation-of-the-semic-github-space)
5. [Usage](#usage)


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


## User Roles

There are three main types of __actors__ that will interact with the resources and assets produced and managed by SEMIC on the SEMICeu GitHub space: the data specification _consumers_, the data specification _editors_, and the supporting asset _developers_. 

The connection between these three group of actors is the following: The tools and methods are set up by the _developers_ to support the _editors_ in their work, to provide together a coherent experience to the _consumers_.

Since the _consumers_ are the "end users" of the data specifications, they will not need to interract directly with the SEMICeu GitHub space. 
Therefore, we will focus mainly on defining the roles of the _editors_ and _developers_, and will provide less details about _consumers_ and other user roles.

### Consumers 

The main group of consumers of the the data specifications are the EU Member State administrations that want to exchange data cross-border.
To support that activity an EU wide understanding of the semantics of the shared data is required.
SEMIC offers a platform to achieve a consensus on the semantics, and the result is being published as a data specification.

Although the EU Member State administrations are the main target audience, the work and participation is open to anybody. 
So, a consumer can also be an enterprise doing business in Japan, for example.


### Editors

The key users of the tooling and method are the _editors_ of data specifications. 
They are expected to have the following skills:   

 - can write “formal” statements in vocabularies & application profiles (linguistic skills)  
 - can organise information in a data model (structuring skills)  
 - can explain data model issues in a webinar (communication skills)  
 - can write & execute simple software code (software developer skills)  

The objective of the provided tooling and processes is that editors focus on their main task; namely, on improving and maintaining the data specification and interacting with the working group communities.    

A key non-functional requirement for the tooling is that it should not create bottlenecks that prevent the scaling up of the editorial effort. Therefore, local installation of software and data should be avoided. The maintenance of the data specification should never be blocked because one editor has sole access to data.

At any point in time it should be clear what is the technical content on which the data specification is build. Any knowledge transfer between editors can then be focussed on sharing the current expertise on the different opinions in the working group instead of figuring out how to pass technical artifacts. 

### Developers

_Developers_ are the supporting actors in this story.
Their role is mainly to be able to assist in resolving any technical issue with the setup. 
Thus, the performed activities are primarily of operational nature, and less oriented to new development.
When it comes to new development, this will be mostly in the area of automation. 
As mentioned in the [Historical Background](README.md#historical-background), the SEMIC tooling and organisation is grown step by step. 
To support the editors more automation is required.


The prerequisite knowlegde of a developer can be circumscribed as being a Swiss knife (or a full-stack) developer.
Developers (or the developers team) should have the following skills:

 - have generic programming skills
 - being able to process, read and manipulate software in different programming languages and development setups
 - being able to read documentation of various tools and search for missing documentation on the Web
 - understand and work with Continuous Integration and Continuous Development (CI/CD) tools
 - understand and work in the spirit of "infrastructure as code", and be able to operate and deploy software using Docker containers
 - be familiar with the Linux ecosystem, able to explore and execute tasks via command line
 - have affinity with the Semantic Web
  
The work environment that the editors are faced with is more uniform than those by the developers. 
It is advised to maintain the highest burden on the developers and not make design decisions that make the developers life easier, but complicate the work of the editors.
For instance, the usage of GitHub repositories to store the data specifications, should not be the reason to impose a software development approach on those GitHub repositories. 
The organisation and management of those repositories should match the needs of the editors and the publication objectives. 
For instance, whereas for software the scope of a branch in a repository is to ensure that work always happens on a coherent set of instructions, in case of a data specification the scope is to keep a transparent record of the history of the specification. 


### Other roles
Besides the main roles that the above described actors have to fulfill, there exist also other roles, involving specific activities that certain actors need to assume. These activities are described below.

#### Communication
Besides the activities related to the creation and management of the data specifications, there are also __communication activities__, like publishing the results on JoinUp.

These are not documented here (yet).

#### Access management

All user access control operations can be done by the __SEMIC admin__ on [Github](https://github.com/orgs/SEMICeu/people).





## Activities

### The editing of the artefacts

Data specifications evolve over time. 
This evolution is the result of addressing the __use cases__ provided by the SEMIC community for the data specifications.
During the editorial process the _editors_ are adapting the data specification: i.e. the artefacts that are part of the data specification.

The assessment how to best address the use case is beyond this documentation. 
Nevertheless, this documentation provides insights in how a resolution is integrated in the published artefacts of the data specification.

Thus, to adequately respond to the use case, _editors_ should understand how to operate the [toolchain](./toolchain.md) to efficiently create the artefacts for a data specification. 


### Publication of the artefacts

The general idea is to publish each data specification in a human readable form (e.g. HTML) together with other supportive representations (JSON-LD context files, SHACL shapes, RDF vocabularies, etc.). 
The expectations, representations, and content has evolved over time, but has never been written out in a specification (e.g. style guide). Instead, through community feedback and the experience of the SEMIC editors an implicit expectation has been realised. 

Today the process adopted by SEMIC has evolved into using GitHub; one repository per data specification. 
Over the past years, the organisation and structure of these repositories underwent a gradual harmonisation process.

Since these repositories were created before an automated artefact generation tooling was applied, the repositories are set up and organised with the assumption that the content of the repository is manually created. 
Each repository has an individual lifecycle.



## Organisation of the SEMIC GitHub Space

The SEMIC GitHub space contains several dozens of repositories, each falling in specific categories. There are data specification repositories, repositories supporting the generation and publication of the data specifications, and others. 


### Data specification repositories

The data specification repositories are tagged with the topic ***data-specification***.
The full list of SEMICeu repositories tagged with ***data-specification*** can be found [here](https://github.com/search?q=org%3ASEMICeu+topic%3Adata-specification).


#### Core Vocabulary repositories

A subset of the data specification repositories that are set up for the editing of Core Vocabularies is tagged with the topic ***core-vocabulary***.
[Here](https://github.com/search?q=org%3ASEMICeu+topic%3Acore-vocabulary) is the current list of Core Vocabulary repositories.

The Core Vocabulary repositories (e.g. [Core Person Vocabulary](https://github.com/SEMICeu/Core-Person-Vocabulary/)) are organised as follows:

- `Webinars` : any documentation, meeting minutes, recording relating to a webinar on the data specification
- `releases` : the data specification releases, organised per version. Each release is identified by its version number, and has a dedicated subfolder.  The content of a specific data specification release version folder (e.g. [version 2.00 of the Core Person Vocabulary](https://github.com/SEMICeu/Core-Person-Vocabulary/tree/master/releases/2.00)) is not fixed.
The structure of the latest release will be conform to the setup of the artefact generating [toolchain](/toolchain.md). 
It is assumed that there is an `index.html` file, as the data specification is then rendered using GitHub Pages, a free service for public open source GitHub repositories (e.g. for the Person Core Vocabulary it would be published at [https://semiceu.github.io/Core-Person-Vocabulary/releases/2.00/](https://semiceu.github.io/Core-Person-Vocabulary/releases/2.00/)).

More governance agreements are not made.

#### Application Profile repositories

The data specification repositories are tagged with the topic ***application-profile***.
[Here](https://github.com/search?q=org%3ASEMICeu+topic%3Aapplication-profile) is the current list of Application Profile repositories.

Some Application Profile repositories will follow the same organisational structure as the Core Vocabularies, but others follow a different structure.
This has historic reasons.

When a new release for these Application Profiles is being prepared, restructuring the content in accordance to the above described structure is highly recommended.


### Repositories for Supporting Generation and Publication of Data Specifications

The repositories that provide the support for generating and publishing data specifications are tagged with the topic ***tooling***.
The full list of these repositories can be found [here](https://github.com/search?q=org%3ASEMICeu+topic%3Atooling).

These repositories have no common organisational structure, however their `README.md` file should provide a good overview about their organisation and usage.
Also, the [Toolchain](./toolchain.md) page can offer additional information about what these tools are meant to do and when and how to use it. 


## Usage

[TODO: Add an intro sentence]

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
Understanding the technical setup requires the understanding of [how data specifications are modelled](./datamodel.md), and how [persistent identifiers](./puri.md) are used.

Whereas the tooling addresses the generation of the artefacts to be published, the publication activity is a manual step. 
The editor has to _manually_ copy the resulting artefacts to the appropriate location. 


