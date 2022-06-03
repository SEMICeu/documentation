# Artefact generation process

The creation of the data specification artefacts is roughly a two phase process. 
First, all information of the data specification is collected in an internal representation. 
Next, out of that internal representation, the artefacts of the data specification to be published are generated.
The internal representation is the same for each category of data specification. 



## aggregation phase 

The core activity of the first phase is the extraction of the semantic model expressed in the UML diagram into the internal representation.
Within the toolchain the [UML Conversion Tool](https://github.com/Informatievlaanderen/OSLO-EA-to-RDF) is used to convert a UML diagram.




## generation phase 

The artefact generation phase consists of parallell executions targetting one artefact.


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


