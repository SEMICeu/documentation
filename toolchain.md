# Toolchain for publishing data specifications


## Motivation

To support the editors in creating and maintaining data models in a coherent approach tooling is required.

Data models have their own life cycle. 
For instance in the past the Core Vocabularies where created by different teams with different Work Groups at different times.
This had resulted in very similar but yet still distinct and sometime incoherent expressing between the Core Vocabularies.

To have them progress in the same way and same style tooling support is required. 
Certainly if one wants to provide the SEMIC community supportive additional artifacts around the Core Vocabularies, the impact on manual editing is high.


## Setup & Design

The toolchain is based on the [OSLO toolchain](https://github.com/Informatievlaanderen/OSLO-toolchain/blob/master/doc-generic/OSLO-toolchain-27april2022.pptx).

The OSLO toolchain is part of a larger environment for supporting the generation, maintenance and publication of data specifications under the governance of the Flemish Government, Belgium.


The OSLO toolchain has been deployed in 3 repositories at SEMIC:

- a thema repository : [https://github.com/SEMICeu/uri.semic.eu-thema](https://github.com/SEMICeu/uri.semic.eu-thema) A repository which contains the content of one or more data specifications.
- a publication repository: [https://github.com/SEMICeu/uri.semic.eu-publication](https://github.com/SEMICeu/uri.semic.eu-publication)  A repository associated with a publication environment.
- a generated repository: [https://github.com/SEMICeu/uri.semic.eu-generated](https://github.com/SEMICeu/uri.semic.eu-generated) The repository that contains the result of the processing. 

A publication repository is always paired with a generated repository. 
For the moment a single thema repository is active as it is covering the Core Vocabularies.
This choice can be revisited in the future.

To setup a new publication environment there is also a template for the publication environment [https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template).
This contains the latest scripts and tooling references.

At SEMIC these repositories are private GitHub repositories. 
This influences the execution and configuration as operating on private repositories is a differrent GitHub API request than those which can be used for public GitHub repositories.
More information on the configuration can be found in the [publication environment documentation](https://github.com/SEMICeu/uri.semic.eu-publication/blob/master/config/README.md).

The setup makes only partially use of the OSLO toolchain ecosystem. 
Where in OSLO the generated repository is a complete static webpage to be shared with the public, SEMIC uses github pages to publish each data specification independently. 
The connection between both repositories is _not_ automated, and requires manual intervention of the editors.
In SEMIC the OSLO toolchain is defacto used as a locally installed software, where the editor has to take care of adapting the result to make it publishable.

_Design note_: Future work should investigate this issue, as it is errorprone and reduces the efficiency of the toolchain for the editors.
The design should also investigate the issue of the publication of the common domain `http://data.europa.eu/m8g`. 


### Operational considerations
The usage of the OSLO toolchain disconnected from a publication environment but as online editorial tool impacts the current setup.
For instance, the support for multi-environment publication (development/testing/production) on the same domain is not used.
Also checks and quality aspects that are can be guaranteed when both are integrated, 
such as the [out-of-the box source tracing](#HowTo-know-which-repository-is-connected-a-data-specification),
become editorial attention points.


### (Software) Components

The main components are:

- UML editing tool: Enterprise Architect from Sparx systems 
- Source Control System: [GitHub](https://github.com)
- Continuous Integration/Continous Deployment: [CircleCI](https://circle.com)
- OSLO toolchain tools:
    - content extraction tool from UML document: [EA-to-RDF](https://github.com/Informatievlaanderen/OSLO-EA-to-RDF/tree/multilingual)
    - artifact generators: [specgenerator](https://github.com/Informatievlaanderen/OSLO-SpecificationGenerator/tree/multigual-dev)
    - template for publication environment
    - template for thema repository

Commercial fees are only required for Enterprise Architect.
The others have a free tier (to which the objectives of this work complies) or are Open Source components.

_Roadmap note_: the OSLO toolchain is organically grown over the past years. 
The team is currently building 4.0 including a rewrite of the EA-to-RDF with improved documentation of the processing rules of the annotations.
In case of developer related questions on the OSLO-toolchain tools the OSLO maintainers can be best contacted.


## Editors HowTo


### HowTo add a new data specification 

There are basically two approaches to initiate a new data specification, each them addressing a different objective.
The first is creating a full fresh start with a new thema repository. 
The advantages and reasons for this choice are that the changes to the github repository reflect the (editorial) changes to data specification. 
They are thus not mixed with the changes to other data specifications. 
If the new data specification is an extension or will be part of the common maintenance (e.g. common versioning and publication history) of an existing collection of data specifications, then these should be present in the same GitHub repository.

For instance, if each Core Vocabulary is considered a subpart of the common data model, the Common Core Vocabularies, and the release policy is that a change in the one element will increase the release version number for all individual Core Vocabularies, then a single thema repository is a good choice.
When each Core Vocabulary has a totally independent release and maintenance flow, with distinct version numbering ( e.g. CCCEV is 2.1.4 and Core Person is 3.2.4) then distinct thema repositories are adviced.
The release and maintenance processes evolve over time, therefore the organisation of the thema repositories can change over time.

#### An new thema repository

The OSLO-toolchain has prepared a thema repository template [https://github.com/Informatievlaanderen/OSLOthema-template](https://github.com/Informatievlaanderen/OSLOthema-template). 
Use this to create an initial thema repository in the SEMIC space.
Mark the new repository as private.

The repository is ready to be used but it is advised to create quickly the minimal context and configuration relating to the target data specification.
And to remove as much as possible the not necessary boilerplate configuration with sensible values for SEMIC.



#### As part of an existing thema repository

In this case the user has to step wise add the necessary configuration and data related to the data specification {NEW}.
Either by copying the boilerplate values found in https://github.com/Informatievlaanderen/OSLOthema-template, or by copying the values from another data specification in the thema repository.

The current minimal steps are:

1. add config file {NEW} for the data specification in {THEMAREPO}/config/{NEW}.json 
2. add the UML document  {THEMAREPO}/{NEW}.eap
3. add the stakeolder information {THEMAREPO}/stakholders.csv
4. add the html template information {THEMAREPO}/templates/{NEW}.j2
5. add the directory {NEW} for additional information in the html representation: {THEMAREPO}/site-skeleton/{NEW}
    TIP: if the directory is empty, add an empty file called .gitignore to the directory.

### HowTo add/update a term to/in a data specification

Adding or updating a term to/in a data specification is a UML modeling task. 
It does not involve manipulating any other data.

The editor thus updates the UML model in Enterprise Architect, and commits the changed file to the thema repository.
To trigger the artifact generator, the corresponding publication point has to be adapted in the publication environment.

The rules for manipulating the UML model can be found []().

### HowTo trigger the generation of the artifacts

Triggering the generation of the artifacts is done via changing the publication repository. 
When a change is committed to the publication repository, CI/CD process (CircleCI) is initiated which produces the artifacts.
The result of the generation process is stored in the generated repository.

A commit to the thema repository is _not_ triggering the generation process. 
An editor can thus improve incrementally the content in the thema repository, without being forced to generate each time the artifacts.
Ony when needed the editor will trigger the generation process.

The usual commit for triggering the generation process is changing the publication point corresponding to the data specification the editor.
Guidelines on how to create and maintain publication points are found in the publication repository.


### HowTo track errors

The editorial process is a continuous process of improvements.
Errors or mistakes can be either data specification related, either the result of a technical error in the processing.

The first are in general only detectable by the data specification readers. 
For instance, a definition set to be "TODO definition" by the editor is technically a valid string, but from a data specification incorrect.
Spotting these kind of errors/mistakes/issues are the responsability,  in the first place,  of the editor but in general of the whole working group.
The tooling will only facilitate the propagation of the correction throughout all artifacts.

A second category are when the artifacts yield unexpected content (being the presence or absence of data). 
This might be caused by a bug in the artifact generator, or the result of a mis-configuration (of the artifact generator).
Check if the same unexpected content is present for other data models, not under your responsability. 
If that is the case, then the issue is probably a "feature" of the artifact generator. 
Otherwise, it might be a wrong configuration which can be checked by comparing with a data model configuration for which the artifact is as expected.
Usually the issue can be efficiently analysed by a developer, as technical experience enable quick tracing of the problem.

The last category are errors that are due to a technical error in the processing. 
The source can be inside or outside the toolchain.
E.g. GitHub is not accessible in the organisation.
The variation of these errors require thus developer knowledge, to assess and react to the issue.

The toolchain foresees in error reporting and user feedback in 2 major channels:
 - via the generated repository
 - via the CircleCI interface

When the artifact generation is successful, i.e. technically successful, the generated repository contains the intermediate processing data including logs from the artifacts generators in the directory `report`. In SEMIC it is [here]().
A successful execution is thus equivalent with a commit to the generated repository where the content of the publication point is updated to reflect the change done by the editor.
To know if the issue is a content issue (category 1) or an artifact generator issue (category 2) the report directory contains the aggregated content, serialised as a json file, produced in the aggregation phase. 
If the content is present in the aggregated file, then the issue is most likely a category 2 issue. 

When there is no commit present, then the CircleCI processing might be terminated.
To check this open in the CircleCI UI the execution trace for this repository and corresponding branch.
A failed step is indicated clearly, and this forms the starting point of the investigation.
The logged messages are verbose, and normally provide sufficient context to find the source. 
However in some cases, it is more efficient to rerun the step with SSH active and investigate the processing with the data by connecting through SSH to the CircleCI step. 
This requires developer knowledge.
Note that the log messages are targetting developers, not editors. 
The business validation errors are always collected and committed to the generated repository. 
Most editors will therefore use CircleCI to follow the progress of the artifact generation or to understand how their commit to the publication environment triggered a processing error.

Since the toolchain is based on versioned services, a complete block of the execution of the toolchain can _always_ be resolved by reverting to the last correct operational situation in the (publication) repositories. 
This are normal GitHub operations, therefore even editors are capable to realise this.


### HowTo know which repository is connected a data specification 
When dealing with issues for a data specification, tracking the data specification to its source is a common issue.
For that the editor has to create a (mental) map crossing different repositories, which is helped by built-in features of the toolchain.

The toolchain will always add the 
   - commit hash code for the publication environment that triggered the generation of the artifact, and
   - commit hash code for the thema repository from which the artifact is generated
to the aggregated content.
Per default, this is part in the html representation as a html link to the thema repository pointing to the source of the data specification.

This allows to exactly know the (UML) content on which the data specification is based. 
Even more, git history provides an undeniable ledger of which changes that have resulted in this state.

In SEMIC, where the publication of the artifacts is done manually by copying the generated artifacts to the corresponding Core Vocabulary github repositories, adding this information (even hidden) is aiding the tracing.


## Developers HowTo

### HowTo find the source code of the automation

The source code for the CircleCI automation is part of the repository [uri.semic.eu-publication](https://github.com/SEMICeu/uri.semic.eu-publication). 
The organisation and setup of the workflow of the CircleCI workflow is extensively documentated in the template repository [OSLO-publicationenvironment-template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template).

The CircleCI workflow will executes in some steps software available as public Docker images. 
These images are build from the open source repositores 
  - [OSLO-EA-to-RDF](https://github.com/Informatievlaanderen/OSLO-EA-to-RDF)
  - [OSLO-Specificationgenerator](https://github.com/Informatievlaanderen/OSLO-SpecificationGenerator)


### Howto add a new artifact generator

An artifact generator is a tool that transforms the intermediate aggregated json structure to the desired artifact. 
It has as input a json file and any additional tool configuration parameters and produces the artifact as a file.
In the repository [OSLO-Specificationgenerator](https://github.com/Informatievlaanderen/OSLO-SpecificationGenerator) collects the OSLO artifact generators.
These are all written in javascript. 
A test suite is available in the repository, illustrating the usage of each artifact generator w.r.t. different parameter choices.

Adding a new artifact generator in that repository is thus the following process in short:
   - create a new tool as a new javascript tool
   - add the test suite
   - build and publish a new docker image
   - integrate the execution in the CircleCI workflow in a configured publication environment
   - test the result

When the artifact generator has reached maturity add the additional generation possibility as part of a new version for
[OSLO-publicationenvironment-template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template) to share your work with the community.


### Howto modify/improve an artifact generator

The process to update an artifact generator follows the same process as adding a new one.


