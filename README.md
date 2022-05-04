# Documentation
A repository containing the overview documentation on the resources and tools related to the Core Vocabularies.

This documentation covers the state of affairs at May 2022.

## Table Of Contents
1. [Motivation](#motivation)
2. [Architecture](#architecture)
3. [Actors](#actors)
4. [Toolchain](./toolchain.md)
5. [Datamodel](./datamodel.md)
6. [Persistent URIs](./puri.md)


## Motivation

SEMIC is supporting the Semantic Interopability Community with the creation of data specifications (i.e. Core Vocabularies and Application Profiles).

This documentation describes the supporting assets that are being setup, configured, used to realise the data specifications.

## Architecture 

The creation of data specification is an activity that involves design decisions at two aspects:

- creation or generation of the artificats
- publication of the artifacts

Both activities are connected but require different tools and methods. 
In some organisations it even might be decided that both are performed by different teams. 

In SEMIC they are performed by the same team, however the connection between both has not been automated.
This has historic reasons. 
SEMIC has started with managing data specifications independently by independent editorial teams producing artificats manually.
Step by step, in the past 10 years, more harmonisation occurred.
The documented tooling and setup is a further step towards an integrated and automated flow between the creation and the publication of the artificats.
Nevertheless the argumentation why and how the design of the architecture has become this form is because its organically grown, making the best decision with the minimal impact to the existing processes and methodes.


We distinguish two main types of actors: editors and developers. These roles are elaborated in a separate section.
The tools and methods are setup to support the editors and to provide the "readers of the data specifications" a coherent experience.
But as already mentioned, due to historic reasons the editors (and the readers) are faced with historic organisation and presentations.



### publication of the artifacts

The general idea is to publish each data specification in a human readible form (html) and other supportive representations (JSON-LD context files, SHACL shapes, RDF vocabularies, ...). 
The expectations, representation, content has evolved through time, but never has been written out in a specification (style guide), but throughout community feedback and SEMIC editors experience an implicit expectation has been realised. 

Today SEMIC has evolved in using GitHub, one repository per data specification. 
During the past years, the organisation and structure of these slowly are harmonising.

Since these repositories where created before an automated artifact generation tooling was applied, the setup and organisation of the repositories are setup with the idea that the content of the repository is manually created. 
Each repository has an individual lifecycle.

For editors that are face to keep the coherency between different repositories this forms a challenge. 
Although it seems simple when applying change A to repository R1 then apply the same change to repository R2, this is errorprone. 
In particular when editors are collaborating or replaced over time. This knowledge gets lost.
Automated tooling that is able to propagate the same change over two data specification will ensure consistency.

A first step to support editors producing coherent cross-repository artifacts, is the deployment and use of a [toolchain](#./toolchain.md).
The editor has then to spend effort to _manually_ copy the resulting artifacts to the correct spot.

The technical setup of the data specification repositories is discussed [here](#GitHubOrganisation)


### generation of the artifacts

A first step towards coherency between data specifications is that the published artifacts are all in the same style.
To achieve this generators and automated tooling is necessary. 

The tooling provides support for the common editorial challenges:
   - how to initiate a new vocabulary
   - how to add/modify a term to a vocabulary
but also to the presentation challenges:
   - how to change the presentation of a vocabulary
   - how to adapt generated artificats
   - how to add new artifacts 

More explanation on the technical setup and operation on the toolchain is found [here](/toolchain.md).
Understanding the technical setup might require to understand what is a [data model](/datamodel.md) and how [persistent identifiers](/puri.md) work.


# GitHubOrganisation

For the Core Vocabularies, e.g. [Core Person](https://github.com/SEMICeu/Core-Person-Vocabulary/), the repository is organised as follows:

- Webinars : any documentation, meeting minutes, recording relating to a webinar on the data specification
- Releases : the data specifications organised per version.

Each release is identified with its version number. 
The content of the [data specification version directory](https://github.com/SEMICeu/Core-Person-Vocabulary/tree/master/releases/2.00) is not fixed.  
For the latest release it corresponds to the generated structure by the [toolchain](/toolchain.md) for generating the artifacts. 

It is assumed that there is an index.html file because the specification is then rendered using github pages, a free service for public open source GitHub repositories, at [https://semiceu.github.io/Core-Person-Vocabulary/releases/2.00/](https://semiceu.github.io/Core-Person-Vocabulary/releases/2.00/).



# Actors


The key users of the tooling and method are _editors_ of data specifications. 
They are expected to have the following skills:   

 - can write “formal” statements in vocabularies & application profiles (linguistic skills)  
 - can organise information in a data model (structuring skills)  
 - can explain data model issues in a webinar (communication skills)  
 - can write & execute simple software code (software developer skills)  

The objective of the provided tooling and processes is that editors focus on their main task: namely improving and maintaining the data specification and interacting with the working group communities.    


A main non-functional requirement for the tooling is that it should be avoided that the tooling creates bottlenecks that prevent the scaling up of the editorial effort. Therefore, local installation of software and data should be avoided. The maintenance of the data specification should never be blocked because one editor has sole access to data. It should be at any point in time clear what is the technical content on which the data specification is build. Any knowledge transfer between editors can then be focussed on sharing the current expertise on the different opinions in the working group instead of figuring out how to pass technical artifacts. 


_Developers_ are the supporting actors in this story.
They role is mainly being able to assist in resolving any technical issue with the setup. 
Thus more operational than new development.
When it comes to new development, this will be mostly in the area of automation. 
As already mentioned in the [architecture section](#architecture), the SEMIC tooling and organisation is grown step by step. 
To support the editors more automation is required.


The prerequisite knowlegde of a developer can be circumscribed as being a swith knife (or a full-stack) developer.
Developers (or the developers team) should have the following skills:

 - have generic programming skills
 - being able to process, read and manipulate software in different programming languages and development setups
 - being able to read documentation of various tools and search for missing documentation on the web
 - understand and work with Continuous Integration and Continuous Development (CI/CD) tools
 - understand and work in the spirit of "infrastructure as code", and there able to operate and deploy software using Docker containers
 - be familiar with the Linux ecosystem, able to explore and execute tasks via command line
 - have affinity with the Semantic Web
  
The work environment the editors are faced with is more uniform than those by the developers. 
It is advised to maintain the highest burden on the developers and not make design decisions that make the developers life easier but complicate the work of the editors.
For instance the usage of git repositories to store the data specifications, should not be the reason to impose a software development approach on those git repositories. 
The organisation and management of those git repositories should match the needs of the editors and the publication objectives. 
Where-as for software the scope of a branch is a coherent set of instructions, the scope of a data specification is the transparent history of the specification. 




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
-> By "artifact-generation" improval process
   -> toolchain.md 

What is open source?  
-> all components except Enterprise architect
```


