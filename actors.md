# Actors

There are three main types of __actors__ that will interact with the resources and assets produced and managed by SEMIC on the SEMICeu GitHub space: the data specification _consumers_, the data specification _editors_, and the supporting asset _developers_. 

The connection between these three group of actors is the following: The tools and methods are set up by the _developers_ to support the _editors_ in their work to provide together a coherent experience to the _consumers_.

Since the consumers are the "end users" of the data specifications, they will not need to interract directly with the SEMICeu GitHub space. Therefore, this documentation will only focus on the _editors_ and _developers_, as they constitute its target audience.


## Consumers 

The main group of consumers of the the data specifications are the EU Member State administrations that want to exchange data cross-border.
For that activity an EU wide understanding of the semantics of the shared data is required.
SEMIC offers a platform to achieve a consensus on the semantics and the result is being published as a data specification.

Although the EU Member State administrations are the main target audience, the work and participation is open to anybody. 
So a consumer can also be an enterprise doing business in Japan.


## Editors

The key users of the tooling and method are _editors_ of data specifications. 
They are expected to have the following skills:   

 - can write “formal” statements in vocabularies & application profiles (linguistic skills)  
 - can organise information in a data model (structuring skills)  
 - can explain data model issues in a webinar (communication skills)  
 - can write & execute simple software code (software developer skills)  

The objective of the provided tooling and processes is that editors focus on their main task: namely improving and maintaining the data specification and interacting with the working group communities.    

A main non-functional requirement for the tooling is that it should be avoided that the tooling creates bottlenecks that prevent the scaling up of the editorial effort. Therefore, local installation of software and data should be avoided. The maintenance of the data specification should never be blocked because one editor has sole access to data. It should be at any point in time clear what is the technical content on which the data specification is build. Any knowledge transfer between editors can then be focussed on sharing the current expertise on the different opinions in the working group instead of figuring out how to pass technical artifacts. 

### communication
Besides the activities related to the creation and management of the data specifications, there are also communication activities like publishing the results on JoinUp. These are not documented here (yet).

## Developers

_Developers_ are the supporting actors in this story.
They role is mainly being able to assist in resolving any technical issue with the setup. 
Thus in the first place the performed activities are more operational than new development.
When it comes to new development, this will be mostly in the area of automation. 
As already mentioned in the [Historical Background](#historical-background), the SEMIC tooling and organisation is grown step by step. 
)
To support the editors more automation is required.


The prerequisite knowlegde of a developer can be circumscribed as being a Swiss knife (or a full-stack) developer.
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
For instance the usage of GitHub repositories to store the data specifications, should not be the reason to impose a software development approach on those GitHub repositories. 
The organisation and management of those repositories should match the needs of the editors and the publication objectives. 
For instance, whereas for software the scope of a branch in a repository is a coherent set of instructions, the scope of a data specification is the transparent history of the specification. 


### access management

All user access control operations can be done by the SEMIC admin on [Github](https://github.com/orgs/SEMICeu/people).








