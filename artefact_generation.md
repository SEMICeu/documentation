# Artefact generation process

This chapter describes condensly the artefact generation process for a data specification.
The target audience for this chapter are experienced editors and developers that want to understand and improve the artefact generation.
Nevertheless novel editors are invited to perform a quick reading as this will aid them to communicate better with the developers when the artefact generation fails.


The creation of the data specification artefacts is roughly a two phase process. 
First, all information of the data specification is collected in an internal representation. 
Next, out of that internal representation, the artefacts of the data specification to be published are generated.

The internal representation has the same structure for each data specification category. 
This simplifies the developer effort to create (new) data specification artefact generators, as experience from one generator can be transferred to another.
The internal representation contains besides the semantical content of a data specification (see the [datamodel](./datamodel.md) chapter) the stakeholders contributing to the data specification and the complete configuration information associated with the data specification:  the [data specification configuration](https://github.com/SEMICeu/uri.semic.eu-thema/blob/example/config/core-person.json), the [publication point configuration](https://github.com/SEMICeu/uri.semic.eu-publication/blob/example/config/dev/publication.json), the [publication environment configuration](https://github.com/SEMICeu/uri.semic.eu-publication/blob/example/config/config.json) and the toolchain execution information.
E.g. the internal representation for the example data specification discussed in the [editorial flow](./editorial_flow.md) chapter is [here](https://github.com/SEMICeu/uri.semic.eu-generated/blob/example/report/doc/core-vocabulary/core-person/all-core-person-ap.jsonld).
Storing the internal representation in the generated repository provides editors to explore this structure to detect the origin of errors or to express new features for artefact generators.

The artefact generation process is automated and implemented using CircleCI, within the publication repository [uri.semic.eu-publication](https://github.com/SEMICeu/uri.semic.eu-publication). 
The CircleCI web application offers a visual representation of the CircleCI workflow, and thus a visual representation of the artefact generation process.
Generic information about the organisation and setup of the workflow of the CircleCI workflow is documentated in [OSLO-publicationenvironment-template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template).


## aggregation phase 

The core activity of the first phase is the extraction of the semantic model expressed in the UML diagram into the internal representation.
In the [datamodel](./datamodel.md) chapter is explained that the UML diagram is a standard UML model extended with annotations.

Technically the [UML Conversion Tool](https://github.com/Informatievlaanderen/OSLO-EA-to-RDF) is used to convert a UML diagram.
This tool is responsible for assigning PURIs to the terms in the data specification and for the interpretation of the UML model as a semantic model.
To avoid diverging semantical interpretations across the artefacts, the generators in the generation phase should not make any semantic interpretation. 
This means determining what is a class or a property, the assignment of PURIs, etc. are the sole responsability for the UML Conversion Tool.

Besides the semantic interpretation, the aggregation phase is handling the multilingual aspects.
It will create [translation files](https://github.com/SEMICeu/uri.semic.eu-generated/blob/example/report/doc/core-vocabulary/core-person/translation/core-person-ap_de.json). 
Translation files contain all translatable content in a structure compatible with the semantic model.
During the aggration phase, the provided translations are merged into the internal representation to create a language aware internal representation.



## generation phase 

The artefact generation phase consists of parallell executions targetting one artefact.

The toolchain provides a number of artefact generators. 
Below for each artefact generator a short description is provided.

During editing a data specifications editors should not be concerned with the internal details of the artefact generators.
However experienced editors may start reflecting on whether the produced artefacts satisfy the consumers' expectations or needs.
At that moment editors become developers, namely evaluating and desiging the expected outcome of the artefacts.
The provided documentation targets the knowledge required for performing editorial activities. 
Design considerations for developers are beyond scope.

### HTML artefact generator

The HTML artefact generator makes a HTML file by rendering an template with the internal representation.
The template language used is [Nunjuncks](https://mozilla.github.io/nunjucks/).

The data specification configuration in the thema repository contains the reference to the template.
The template language supports modularity via importing other templates. 
The HTML artefact generator is designed, and configured, to exploit this mechanism so that the data specification's specific content, e.g. the summary,  is combined with a generic template for the publication environment.
The ability to work with reusable generic templates is an enabler for a coherent consumer experience on the web.
Creating reusable generic templates requires knowledge about the publication environment, such as the hostname and path where the HTML document will be published, and information where additional data specification's content, such as pictures.
Where the first is part of the publication repository configuration, is the latter part of the thema repository. 

The generation is language sensitive as the labels, definitions and usage notes of the terms in the data specification are language sensitive.
Therefore the language to use from the internal representation must be specified.

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

In the toolchain the first representation is active.

 

# Adding a new artefact generator to the artefact generation process

The repository [OSLO-Specificationgenerator](https://github.com/Informatievlaanderen/OSLO-SpecificationGenerator) collects the OSLO artefact generators.
These are all written in javascript. 
A test suite is available in the repository, illustrating the usage of each artefact generator w.r.t. different parameter choices.

Adding a new artefact generator in the artefact generation process is in short as follows:
   - implement the artefact generator
       - create the new artefact generator as a new javascript tool
       - add the test suite
       - build and publish a new docker image with the new artefact generator included
   - integrate the artefact generator
       - update the CircleCI workflow
       - extend or implement supportive scripts in the publication environment
       - test the result

The integration is best applied on a working setup.  
When the artefact generator has reached maturity add the additional generation possibility as part of a new version for
[OSLO-publicationenvironment-template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template) to share your work with the community.




