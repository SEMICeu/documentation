# Artefact generation process

The creation of the data specification artefacts is roughly a two phase process. 
First, all information of the data specification is collected in an internal representation. 
Next, out of that internal representation, the artefacts of the data specification to be published are generated.

The internal representation has the same structure for each data specification category. 
This simplifies the developer effort to create a new data specification artefact generator as experience from one generator can be transferred to another.
But also it offers the ability for (experienced) editors to explore this structure to detect the origin of errors or to express more precisely new features for artefact generators.


## aggregation phase 

The core activity of the first phase is the extraction of the semantic model expressed in the UML diagram into the internal representation.
Within the toolchain the [UML Conversion Tool](https://github.com/Informatievlaanderen/OSLO-EA-to-RDF) is used to convert a UML diagram.


## generation phase 

The artefact generation phase consists of parallell executions targetting one artefact.

### HTML artefact generator

The HTML artefact generator makes a HTML file by rendering an template with the internal representation.
The template language used is Nunjuncks.

The data specification configuration in the thema repository contains the reference to the template.

The HTML artefact generator must be made aware of the publication environment.
Without that knowledge it is impossible to generate a HTML with the correct links.
Therefore the hostname and the path where the html document is being published must be provided.

The generation is language sensitive as the labels, definitions and usage notes of the terms in the data specification are language sensitive.
Therefore the language to use from the internal representation must be specified.

The HTML artefact generator has been configured to copy the content of the site-skeleton

Besides these key options, there are more options facilitating the implementation, but these are for the developers to explore. 


### RDF artefact generator

The RDF artefact generator makes a JSON-LD file out of the internal representation.

Using of-the-shelf JSON-LD to RDF serialisation convertion tools the JSON-LD file is expressed as turtle, ntriples or RDF/XML.

The generation is not language sensitive as RDF allows multilanguage content.

### JSON-LD context artefact generator

The JSON-LD context artefact generator creates a JSON-LD context out of the internal representation.

The generation is language sensitive as the attribute names to be mapped can be based on the labels of the terms in the data specification.
Therefore the language to use from the internal representation must be specified.

The generation is also sensitive to disambiguation challenges. 
Therefore an option has been added to force domain based disambiguation.

### SHACL artefact generator

The SHACL artefact generator creates a SHACL out of the internal representation.

The same collection of constraints can be expressed in various SHACL representations.
In the most compact representation the constraints are grouped per SHACL node.

This is one representation the SHACL artefact generator can produce. 
It was the first representation.
The error messages in this representation are those from the SHACL processing engine.

An alternative representation is to create per constraint an SHACL expression.
In this case specific error messages can be associated per constraint.
This representation allows to add more easily specific usage notes constraints such as, _there should only one value per language_ for which SHACL has a dedicated expression.

The generation is language sensitive as the validation messages are based on the labels of the terms in the data specification.
Therefore the language to use from the internal representation must be specified.
In a multilingual context, the second representation is required as it is the only way to create a error context aware message in multiple languages.




## Howto add a new artefact generator

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




