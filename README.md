# Documentation
This repository contains the overview documentation describing the resources and tools developed and used by the Semantic Interoperability Community ([SEMIC](https://joinup.ec.europa.eu/collection/semantic-interoperability-community-semic)).

The [SEMICeu GitHub space](https://github.com/SEMICeu) is created to support the Semantic Interoperability Community with the creation of __data specifications__ (e-Government Core Vocabularies, Application Profiles, etc.). A list of these data specifications can be found [on the SEMIC website](https://joinup.ec.europa.eu/collection/semantic-interoperability-community-semic/our-resources). This documentation describes both how the different SEMIC resources are organized in GitHub repositories, as well as what are the supporting assets that need to be _set up_, _configured_, and _used_ to realise (i.e. edit and publish) such SEMIC data specifications.

This documentation covers the state of affairs as of May 2022.
The objective is that readers of this documentation are provided with sufficient achors to initiate mastering the methods and tooling used to create and manage data specifications.




## Table Of Contents
1. [Historical Background](#historical-background)
2. [User Roles and Activities](#user-roles-and-activities)
3. [Organisation of the SEMIC GitHub Space](#organisation-of-the-semic-github-space)
4. [Usage](#usage)


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

There are three main types of __actors__ that will interact with the resources and assets produced and managed by SEMIC on the SEMICeu GitHub space: the data specification _consumers_, the data specification _editors_, and the supporting asset _developers_. 
The tools and methods are set up by the _developers_ to support the _editors_ in their work to provide together a coherent experience to the _consumers_.
Since the _consumers_ are the "end users" of the data specifications, they will not need to interract directly with the SEMICeu GitHub space. Therefore, this documentation will only focus on the _editors_ and _developers_, as they constitute its target audience.

For more information about the user roles please check out the [Actors](./actors.md) page.

### The editing of the artefacts

Data specifications evolve over time. 
This evolution is the result of addressing the __use cases__ provided by the SEMIC community for the data specifications.
During the editorial process the _editors_ are adapting the data specification: i.e. the artefacts that are part of the data specification.

The assessment of how to best address the different use cases is beyond the scope of this documentation. 
Nevertheless, this documentation provides insights into how a resolution for a given change is integrated in the published artefacts of the data specification.

To adequately respond to a use case, _editors_ should understand how to operate the **toolchain** (see [Usage section](#Usage) for details) to efficiently create the artefacts for a data specification. 
The created artefacts are always represented in a human readable form (e.g. HTML) together with other supportive representations (JSON-LD context files, SHACL shapes, RDF vocabularies, etc.) depending on the nature of the data specification. 

The editorial activity typically requires several iterations in order to reach the final resolution.
The *toolchain* reduces the workload on editors created by these iterations, makes the artefact creation less error-prone, and at the same time increase the coherency among the different data specifications. 
It also can play an important role in training future editors to maintain the data specifications. 


### Publication of the artefacts

After creating the artefacts, the editor has to make them accessible to the consumers. 
For this the artefacts have to be stored in a publication environment.

Currently, the publication environment that has been adopted by SEMIC is GitHub; one repository per data specification. 
Over the past years, the organisation and structure of these repositories underwent a gradual harmonisation process.
More specifically, the consumers' access to the content of these repositories is facilitated through [GitHub Pages](https://pages.github.com/), a service offered to render webpages stored in a repository.

Since these repositories were created before an automated artefact generation tooling was applied, the repositories are set up and organised with the assumption that the content of the repository is manually created. 

The original source code for the *toolchain* has not been designed with this publication design in mind, therefore editors are today required to manually collect the generated artefacts and store them in the appropriate data specification repository.
It is future work to reduce this manual activity. 



## Organisation of the SEMIC GitHub Space

The SEMIC GitHub space contains several dozens of repositories, each falling in specific categories. There are data specification repositories, repositories supporting the generation and publication of the data specifications, and others. 


### Data specification repositories

The data specification repositories are tagged with the topic ***data-specification*** in GitHub.
The full list of SEMICeu repositories tagged with ***data-specification*** can be found [here](https://github.com/search?q=org%3ASEMICeu+topic%3Adata-specification).

As each data specification follows its individual lifecycle, their respective repositories also do. 
Nevertheless, as part of the editorial process multiple data specification repositories might be updated to address a given issue.


#### Core Vocabulary repositories

A subset of the data specification repositories that are set up for the editing of Core Vocabularies is tagged with the topic ***core-vocabulary***.
[Here](https://github.com/search?q=org%3ASEMICeu+topic%3Acore-vocabulary) is the current list of Core Vocabulary repositories.

The Core Vocabulary repositories (e.g. [Core Person Vocabulary](https://github.com/SEMICeu/Core-Person-Vocabulary/)) are organised as follows:

- `Webinars` : any documentation, meeting minutes, recording relating to a webinar on the data specification
- `releases` : the data specification releases, organised per version. Each release is identified by its version number, and has a dedicated subfolder.  The content of a specific data specification release version folder (e.g. [version 2.00 of the Core Person Vocabulary](https://github.com/SEMICeu/Core-Person-Vocabulary/tree/master/releases/2.00)) is not fixed.
The structure of the latest release will conform to the setup of the artefact generating *toolchain*. 
It is assumed that there is an `index.html` file, as the data specification is then rendered using GitHub Pages, a free service for public open source GitHub repositories (e.g. version 2.0.0 of the Person Core Vocabulary would be published at [https://semiceu.github.io/Core-Person-Vocabulary/releases/2.00/](https://semiceu.github.io/Core-Person-Vocabulary/releases/2.00/)).

Further governance agreements regarding the structure of the Core Vocabulary repositories are not made.

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

The *toolchain* is an online service built from a collection of GitHub repositories in the SEMIC GitHub space. 
The repositories are interconnected with automated processing.
There is no local installation required, besides of a UML editing tool.

The basic idea behind the toolchain service is to consider a data specification as software source code. 
Software development has a long history in tooling and approaches to manage code changes with different contributors.
The rise of Open Source software development in the past decades made the tools and approaches for building software freely and reliable available for anybody.
One of the best practices within software development is to build tools that release developers from repetitive work and other risks that are part of the software development process.
Here, the toolchain will release editors from manually building the artefacts by exploiting software building tools.
As a consequence, editors must familiarize themselves with the software development mindset. 

Using the toolchain for editing data specifications requires editors to have insight in 
  
   - the interplay between the GitHub repositories (see the chapter on the [Editorial flow](./editorial_flow.md)) 
   - what data specifications are, and what information are they built of (see the chapter on the [Data specifications](./datamodel.md))
   - what persistent identifiers are, and how their use is supported by SEMIC (see the chapter on [Persistent identifiers](./puri.md))
   - the operational environment deployed (see the chapter on the [Toolchain](./toolchain.md))

The purpose of these chapters is  to introduce *editors*, but also *developers*, to foundational aspects of the *editorial flow* and how it is supported by the *toolchain*.

Note that the documentation is not a reflection on design decisions. Only those are included that are helpful to improve the understanding of how the tools and processes work. 
The documentation provides merely a description of the current state of affairs, with references to further information, when it might be necessary for a given task.
As a result, the documentation may raise valuable (design) questions without an answer provided here. For instance, UML data modeling guidelines are not part of this documentation, despite this being a valuable knowledge for an editor.
However, in the future, such aspects might be included also in this documentation.

The chapters are written with the assumption that the reader has at least a basic knowledge on the Semantic Web, UML modeling, GitHub and software development.
Despite the efforts to make the text understandable for readers with diverse backgrounds, readers might encounter parts using unfamiliar terminology or approaches.
If this is blocking for the reader, it may be helpful to perform the editorial flow, as a hands-on exercise, to experience the expressed ideas. 
Also, watching the included screencasts might be helpful.

The different chapters shed different perspectives on creating and publishing data specifications. 
Each chapter can be read, to a high extent, independently. 
Nevertheless, they might use terms or refer to knowlegde that are explained in other chapters in more depth. 
Cross referencing among chapters is used to enable readers to find these explanations more quickly.
This organisation is to keep the documents concise and easily processable for the reader.


