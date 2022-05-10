# Data model 

## Data model types

Designing a data model encompasses the following activities:
- determining the appropriate data structures (Class, Property, ...)
- for each entity the necessary semantical information to relate it to the real world phenonomen it describes.

Data models can be roughly categorized in three groups, according to their intend of reuse.

A *vocabulary* is a collection of terms.  
A term is consists minimally of a label and definition and is identified with a URI. 
The information attached to a term in a vocabulary is expressed with the intend to be applicable within a broad context. 
Guidelines on writing good definitions can be found (here)[].
 
An *application profile* is the usage of terms with an generic application context. 
The application context imposes additional constraints on the usage of the terms such as cardinalities, ranges, codelists, ...
This usage context may also introduce alternative labels or more specific definitions for reused vocabulary terms. 
Editors of application profiles have the challenge to find the balance between introducing new terms and reusing existing terms. 

Application profiles can be further elaborated to the point they describe the usage of the terms in an operational environment (software solution). 
These are called *implementation models*.


Aside the differences in the content resulting from the reuse perspective, each category has different expectations on the representation and published artifacts. 
The listed expectatations are also resulting from the base premise to use the Semantic Web as basis for the design of the data models.

Vocabularies expect 

  - a document with a simple tabular view of the terms 
  - persistent identifiers (PURIs) 

Application profiles expect

  - a document 
    - explaining the application scope 
    - providing a visual overview of the data model
    - a textual, tabular representation expressing the data model entities
  - supportive assets for implementers such as
    - shacl templates
    - json-ld context files
    - xsd schemas
    - examples
  - and being integrated with the vocabularies it reuses

Implementation models expect

  - the same as application profiles, but usually augmented with additional specific artifacts for that system. 
      E.g. a template DB, an API specification, ...


Observe that application profile design is always connected with the creation of a vocabulary associated with application context. 
It is very unlikely that an application profile is only reusing terms from existing vocabularies. 
Therefore creating and supporting application profiles means also creating and supporting vocabularies, in order to achieve the objectives. 


## Core Vocabularies
The Core Vocabularies of SEMIC have the design intend of the vocabularies category: namely broad reuse mostly ignorant about the application context.
But over the years the SEMIC community has requested support towards the *application* of the Core Vocabularies. 
Therefore aspects of what are considered above *application profile* expectations are provided into the Core Vocabularies. 
The provided artifacts can thus be seen as (a small) step in the process of incorporating the core vocabulary in a usage context. 
For instance, the shacl shape template is very permissive for Core Vocabularies as it soley expresses that the range of a property might be of an expected broad type (e.g. Literal versus Resource). 

The Core Vocabularies are showing that the boundaries between a vocabulary and an application profile, as defined above, are not precisely determined.
Vocabularies, application profiles and implementation models are entities on an axe of reusability/application context.
Vocabularies are collections of terms formulated in such a way that they are reusable to a maximum extend without becoming semantically too vague/abstract.
Application profiles are other collections of the same terms but then within a more specific, but still generic  application context. 
And on the other far extreme are terms used within a very specific context: implementation models.


# UML model (annotations)

In SEMIC, the normative documents are Semantic Web models. 
Semantic Web models identifiy terms with URIs and associate the term with the real world using associated semantic information expressed as human readible expressions (labels, definitions, usage notes, ...) and formal logic statements (subclass, domain, range, cardinalities, ...). 

However often a graphical representation is expected.
Graphical representations are able to convey more condensly the key formal logic statements at one glance.
Instead of reinventing a new graphical language, it has been decided to (re)use UML as graphical modelling language.

For coherency accross all specifications it is easier to transform a UML diagram to a semantic representation, than transforming an semantic representation in a UML notation. 
But despite the UML diagram is the master data, the normative document is not the UML diagram but the semantic model that it is representing.

The [Enterprise Architect Conversion Tool](https://github.com/Informatievlaanderen/OSLO-EA-to-RDF) is a tool which converts a UML diagram, expressed as an EAP files, into a neutral representation suited for generating artefects for data specifications.
The syntax of that representation is json(-ld).

The connection between the UML graphical language and Semantic Web is based on interpreting the UML language and additional annotations provided by the editors.
These annotations are key because they control 
  - the URI assignment
  - the human readible semantics
This information is not part of the _standard_ UML. 

Beyond the supporting the interpretation of the UML diagram, the Enterprise Architect Convertion tool supports annotations to facilitate the control of the scope of the content of the semantic model.

An graphical overview of the content of extracted information is shown below.

![EA-annotation.jpg](./EA-annotation.jpg)

Each attribute corresponds with an annotation.


### EA data model tags
In Enterprise Architect these annotations are expressed as tags.
The tags have the following representation

```
   {documenttype}-{annotation}-{language}
```

The {documenttype} can be 
   - **empty**:  corresponds with the vocabulary interpretation. The base information about the term.
   - **ap**: application profile (ap) 

The {language} corresponds to the 2-letter code for a language in which the content of the annotation is expressed.

Examples:
  - `label-nl`: the tag expresses the label of the term in Dutch at the level of a vocabulary. 
  - `ap-usageNote-en`: the tag expresses the usage note in English for the application profile

The pattern is very useful as it allows to have two perspectives on the same term in the UML file.
One perspective is the base reference: the vocabulary, and the other perspective is the application usage context.
Having the ability to have them side by side make it is much easier for editors to ensure the reuse of a term is done properly.

Not all annotations support a prefix {documenttype} or suffix {language}. 
For instance: `uri` has no prefix or suffix as a term should have only one globally unique persistent identifier. 


### Example
To use the [toolchain](./toolchain.md), editors are required to edit the EAP file of the data specification. 
The following screenshot shows the class _Person_ in Enterprise Architect. 

![EA-example.png](./EA-example.png)

In the middle the UML graphical representation is shown. On the right hand side the tags for the selected class _Person_.
Right from the graphical represenation the attributes and relationships of the class are shown.


