# Modeling data specifications

This chapter decribes the key notions and information an editor needs to understand for _modeling data specifications_.
Within this document the term data specification is used to refer to its core: **the semantic model**, i.e. the classes and properties with their semantic description.
Besides this, and beyond the scope of this chapter, a data specification contains metadata about the document, a changelog, use case descriptions, context, conformance statements and more.



## Data specification categories

Designing a data specification encompasses the following activities:
- determining the appropriate data structures (Class, Property, ...)
- for each entity, specifing the necessary semantic information to relate it to the real world phenonomen it describes.

Data specifications can roughly be categorized in three categories according to their intend of reuse.

A *vocabulary* is a collection of terms. 
A term consists minimally of a label and definition, and it is identified by a URI. 
The information attached to a term in a vocabulary is expressed with the intend to be applicable within a broad context. 
Guidelines on writing good definitions can be found (here)[TODO].
 
An *application profile* is the usage of terms within a generic application context. 
The application context imposes additional constraints on the usage of the terms such as cardinality restrictions, ranges, code lists, etc.
This usage context may also introduce alternative labels, or more specific definitions for reused vocabulary terms. 
Editors of application profiles have the challenge to find the balance between introducing new terms and reusing existing terms. 

Application profiles can be further elaborated to the point where they describe the usage of the terms in an operational environment (e.g. software solution). 
These are called *implementation models*.


Aside from the differences in the content resulting from the reuse perspective, each category has different expectations on the representation and published artefacts. 
The listed expectations result from the premise to use the _Semantic Web_ as the __basis__ for the design of the data specification.

_Vocabularies_ expect: 

  - a document with a simple tabular view of the terms 
  - dereferenceable persistent identifiers ([PURIs](./puri.md))

_Application profiles_ expect:

  - a document 
    - explaining the application scope 
    - providing a visual overview of the data model
    - a textual, tabular representation expressing the data model entities
  - supportive assets for implementers, such as
    - SHACL templates
    - JSON-LD context files
    - XSD schemas
    - examples
  - and being integrated with the vocabularies they reuse

_Implementation models_ expect:

  - the same as Application profiles, but usually augmented with additional artefacts specific for a given system,
      e.g., a template DB or an API specification.


Observe that application profile design is always connected with the creation of a vocabulary associated with application context. 
It is very unlikely that an application profile is only reusing terms from existing vocabularies. 
Therefore creating and supporting application profiles means also creating and supporting vocabularies, in order to achieve the objectives. 


The SEMIC Core Vocabularies have the design intent of the _vocabularies_ category: namely broad reuse, mostly ignorant of the application context.
But over the years the SEMIC community has requested support towards the *application* of the Core Vocabularies. 
Therefore some aspects that are enumerated as *application profile* expectations above, are also provided for the Core Vocabularies. 
The provided artefacts can thus be seen as a (small) step in the process of incorporating the Core Vocabulary in a usage context. 
For instance, the SHACL shape for a Core Vocabulary is very permissive as it soley expresses that the range of a property might be of an expected broad type (e.g. Literal versus Resource). 

The Core Vocabularies are showing that the boundaries between a vocabulary and an application profile, as defined above, are not precisely determined.
Vocabularies, application profiles and implementation models are entities along a "reusability/application context" axis.
Vocabularies are collections of terms formulated in such a way that they are reusable to a maximum extend without becoming semantically too vague/abstract.
Application profiles are other collections of the same terms, but within a more specific, however still generic, application context. 
On the other extreme are the collection of terms used within a very specific context: implementation models.

At this moment, however, no formal expectation of the SEMIC data specifications has been written out. We are clarifying these concepts here in the assumption and hope that the editors' awareness of this categorisation will aid the creation the most appropriate semantic models.



# The UML model

As mentioned in the previous section, a SEMIC data specification is build and published according to the best practices of the Semantic Web.
Following this approach data specifications identifiy terms with URIs and associate the term with the real world using associated semantic information expressed as human readible expressions (labels, definitions, usage notes, ...) and formal logic statements (subclass, domain, range, cardinality restrictions, ...). 

However, because the Semantic Web representations (tables in HTML or machine readable formats, such as RDF) are not providing consumers a satisfactory way for understanding the data specification, often a graphical representation is provided.
Graphical representations are able to convey more condensly the key formal logic statements at one glance.
Instead of reinventing a new graphical language, SEMIC uses the Unified Modeling Language (UML) as graphical modelling language.
Instead of reinventing a new graphical language, SEMIC uses the Unified Modeling Language (UML) as graphical modelling language.

This introduces the challenge of maintaining the coherency between the Semantic Web representation, i.e. RDF, and the UML representation. 
The [toolchain](./toolchain.md) deployed by SEMIC implements the following master data management.

#### (transformation argument)
For coherency accross all specifications it is easier to transform a UML diagram to a semantic representation, than transforming an semantic representation into a UML notation. 
Turning RDF vocabularies into UML fully exploiting the graphical notation possibilies would require to create a new configuration language.
This language would not only include semantical instructions (for instance this URI is a UML class), but quickly also include styling and other represenation instructions. 
A large part of the editorial effort for a graphical representation is organising and styling the picture to make it as supportive as possible for the consumers. 
That is a complex task.
It is far more easier to exploit the power of a UML modeling tool, offering all the graphical styling possibilities an editor needs, and transform the resulting UML representation into a semantic model (such as RDF).

#### (editorial argument)
When interacting with the Working Group the discussion is often driven by a graphical representation.
Therefore editors naturally first create the graphical representation of the proposed resolution.
When agreement is reached, the decision is turned into the data specification following the Semantic Web principles by the editor.

Both arguments resulted in the design decision to store the master data of the data specification in a UML model.
However, despite the fact that the UML diagram will act as the master data for the data specification, it is the **semantic model** that is generated from it that the consumers will consider as the data specification.

----

>
> And therefore existing RDF vocabulary visualisations offer not a mapping to the specific UML language but an ability to graphically browse the RDF vocabulary graph which the user of the visualisation can style and organise themselves. 
> These visualisation therefore are not intented to explore the semantics behind the 
>
> Creating an managing data specification acording to the Semantic Web principles is not a default course for students. 
> UML modeling is however part of most curicula.
> Therefore editors are more trained in modeling UML than modeling Semantic Web. 
>

----

## Extracting the semantic model from the UML model

In the toolchain the creation of the data specification is a roughly a two phase process. First, all information of the data specification is collected in an internal representation. Next, out of that internal representation, the artefacts of the data specification to be published are generated.
The internal representation is the same for each category of data specification. 

In this section we describe the core activity of the first phase: namely, the extraction of the semantic model expressed in the UML diagram into this internal representation.


Within the toolchain the [Enterprise Architect Conversion Tool](https://github.com/Informatievlaanderen/OSLO-EA-to-RDF) is used to convert a UML diagram into the internal representation.
At the moment the only supported input file format is an EAP file, the format used by the UML editor Enterprise Architect to save a project.
This is not a limitation for SEMIC as all data specifications are modeled in Enterprise Architect.

For a conversion tool to work, one must connect the UML model with the desired Semantic Web representation. 
The Enterprise Architect Conversion Tool bases itselves on interpreting the UML language (as expected) and additional annotations of the elements in the UML model.
These annotations are key because they control 
  - the URI assignments, and 
  - the human readible semantics.
This information is not part of the _standard_ UML language, and thus must be included in the UML model using a UML language extension mechanism to fullfil the master data design. 

>
> The annotations provide a flexible and extensible approach to support the conversion process beyond the semantic interpretation of the UML diagram.
> Beyond supporting the semantic interpretation of the UML diagram, annotations are also included to facilitate the control the conversion process. of the scope of the content of the semantic model.
>

Without going into detail, the figure below shows the abstract metamodel of the information that the Enterprise Architect Conversion Tool extracts from the UML model augmented with annotations.

![EA-annotation.jpg](./images/EA-annotation.jpg)

### UML annotations (tags)
Most attributes in the above figure correspond to an annotation. 
They are implemented as Enterprise Architect tags. 
EA tags can be applied to any UML model entity.

The tag names used in the SEMIC data specifications will follow the pattern:

```
   {spec-category}-{annotation}-{language}
```

The `{spec-category}` part represents the data specification category. The values for this can be either:
   - _ommitted_:  the annotation is associated with the _vocabulary_ in which the term is defined. It contains the base information about the term.
   - **ap**: the annotation is associated with an _application profile_ in which the term is used.

The `{language}` part corresponds to the 2-letter language code (conform to ISO 639-1) in which the content of the annotation is expressed.

**Examples:**
  - `label-nl`: the tag expresses the label of the term in Dutch, at the level of a vocabulary
  - `ap-usageNote-en`: the tag expresses the usage note in English for the application profile

The pattern is very useful because it allows to have two perspectives on the same term in the UML file.
One perspective is the base reference: the vocabulary, and the other perspective is the application usage context.
Having the ability to have them side by side makes it is much easier for editors to ensure that the reuse of a term is done properly.
Artefact generation tools can take benefit from this multi-perspective to implement a sensible fallback approach. 
For instance, when generating application profile content, first the tags with `{spec-category}` having value `ap` are consulted. 
If no value is found, then the vocabulary tag is consulted. 
Only when this is not present a `TODO/NOT FOUND` value is used.
Application profile editors are thus supported when reusing existing vocabularies.

Not all annotations require a prefix (`{documenttype}`) or suffix (`{language}`). 
For instance: `uri` has no prefix or suffix as a term should have only one globally unique persistent identifier. 

### Example annotated UML model
To use the [toolchain](./toolchain.md), editors are required to edit the EAP file of the data specification. 
The following screenshot shows the class _Person_ defined in the Core Person Vocabulary when edited in Enterprise Architect. 

![EA-example.png](./images/EA-example.png)

In the middle we can see the UML graphical representation. On the right hand side the tags for the selected class _Person_ are shown.
On the left side of the graphical representation the attributes and relationships of the class can be seen.


### Complete overview

The [OSLOthema-toolchainTestbed](https://github.com/Informatievlaanderen/OSLOthema-toolchainTestbed) _thema_ repository provides a collection of example UML models.
Editors can use the collection to understand the impact of a modeling choice in combination with the annotations for each supported data specification category. 
Developers can use it to do regression testing during development.


