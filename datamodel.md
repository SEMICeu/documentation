# Data model development

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

    - integrated with the vocabularies it reuses

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


