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


### access management
All user access control operations can be done by the SEMIC admin on [Github](https://github.com/orgs/SEMICeu/people).




