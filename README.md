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

The assessment how to best address the use case is beyond this documentation. 
Nevertheless, this documentation provides insights in how a resolution is integrated in the published artefacts of the data specification.

Thus, to adequately respond to the use case, _editors_ should understand how to operate the [toolchain](#Usage) to efficiently create the artefacts for a data specification. 
The created artefacts are always a human readable form (e.g. HTML) together with other supportive representations (JSON-LD context files, SHACL shapes, RDF vocabularies, etc.) depending on the nature of the data specification. 

The editorial activity typically requires to iterate several times in order to reach the final resolution.
The [toolchain](#usage) reduces the workload on editors created by these iterations, makes the artefact creation less errorprone and at the same time increase the coherency between the different data specifications. 
It also can play an important role to train future editors to maintain the data specifications. 


### Publication of the artefacts

After creating the artefacts, the editor has to make them accessible for the consumers. 
For this the artefacts have to be stored in a publication environment.

Today the publication environment adopted by SEMIC has evolved into using GitHub; one repository per data specification. 
Over the past years, the organisation and structure of these repositories underwent a gradual harmonisation process.
More specifically, the consumer access is facilitated through [GitHub Pages](https://pages.github.com/), a service offered to render webpages stored in a repository.

Since these repositories were created before an automated artefact generation tooling was applied, the repositories are set up and organised with the assumption that the content of the repository is manually created. 

The original source code for the [toolchain](#usage) has not designed with this publication choice in mind, therefore editors are today required to manually collect the generated artefacts and store them in the appropriate data specification repository.
It is future work to reduce the manual activity. 



## Organisation of the SEMIC GitHub Space

The SEMIC GitHub space contains several dozens of repositories, each falling in specific categories. There are data specification repositories, repositories supporting the generation and publication of the data specifications, and others. 


### Data specification repositories

The data specification repositories are tagged with the topic ***data-specification***.
The full list of SEMICeu repositories tagged with ***data-specification*** can be found [here](https://github.com/search?q=org%3ASEMICeu+topic%3Adata-specification).

As each data specification follows its an individual lifecycle, their repositories also do. 
Nevertheless, as part of the editorial process multiple data specification repositories might be updated to address an issue.


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

The toolchain is an online service build with a collection of GitHub repositories in the SEMIC GitHub space. 
The repositories are interconnected with automated processing.
There is no local install required besides a UML editing tool.

The basic idea behind the toolchain service is to consider a data specification as software source code. 
Software development has a long history in tooling and approaches to manage code changes with different contributors.
Due to the rise of Open Source software development in the past decades, tools and approaches for building software are now freely and reliable available for anybody.
One of the best practices within software development is to build tools that release developers from repetitive work and other risks that are part of the software development process.
Here, the toolchain will release editors from building the artefacts themselves.
However as consequence, editors must familiarize themselves with the software development mindset. 

Using the toolchain for editing data specifications requires editors to have insight in 
  
   - the interplay between the GitHub repositories ( See the Chapter on the [Editorial Flow](./editorial_flow.md) ) 
   - what data specifications are, and what information these are build of ( See the Chapter on the [data specifications](./datamodel.md) )
   - what persistent identiers are, and how they are supported by SEMIC ( See the Chapter on [persistent identifiers](./puris.md) )
   - the operational environment deployed ( See the Chapter on the [toolchain](./toolchain.md) )

These chapters have as purpose to introduce editors, but also developers, to foundational aspects of the editorial flow and how it is supported by the toolchain.

The documentation is not a reflection on design decisions, only those that are required to improve the understanding are included.
But it merely a description of the current state of affairs, with references to find more information for when it is needed by the task.
This makes that the documenation may raise valuable (design) questions without answer here. For instance, UML data modeling guidelines are not part of this documentation despite this is valuable knowledge for an editor.
In the future these aspects find their place in the documentation.

The chapters are written under the assumption of a basic knowledge on the Semantic Web, UML modeling, GitHub and software development by the reader.
Despite the efforts to make the text understandable for readers with diverse backgrounds, readers might encounter parts using unfamiliar terminology or approaches.
If this is blocking for the reader, it may be helpful to perform the editorial flow to experience the expressed idea. 
Also watching the included screencasts might help.

All chapters shed a different perspective on creating and publishing data specifications. 
Each chapter can be read to a high extend independently. 
Nevertheless they might use terms or knowlegde explained in other chapters in more depth. 
Cross referencing is applied to enable readers to find these explanations more quickly.
This organisation is to keep the documents concise and overviewable for the reader.


Supporting the editorial flow with a toolchain fits within the objective for SEMIC to provide more coherent, transparent and efficient services around the data specifications. 
When applying the documented approach, editors can ensure a coherency between the different data specifications published in distinct repositories.
Without tooling support this constitutes a serious challenge. 
Although it seems simple to follow the rule that "when change _A_ is applied to repository _R1_, then apply the same change _A_ to repository _R2_", in reality this ends up being errorprone. 
In particular, when editors are collaborating, or are replaced over time, such knowledge gets lost.
Within this objective the toolchain and this documentation should be seen the activity of capturing the existing editorial practices and experiences in such a way that future editors can more easily maintain the data specifications. 


----
To fulfill its editorial task, an editor will interact with the SEMIC GitHub space following the [editorial flow](./editorial_flow.md).
The editorial flow is supported by software for producing the data specification artefacts, called *the toolchain*.

The expectations, representations, and content has evolved over time, but has never been written out in a formal specification (e.g. style guide). 
Instead, through community feedback and the experience of the SEMIC editors an implicit expectation has been realised. 
