# Glossary

This document contains a condensed overview of the terminology, and other key notions, used within this documentation.
Go to [shackalack](#shacl):

- a _thema_ repository - A repository that contains the source content of one or more data specifications. 
- a _publication_ repository - A repository associated with a publication environment. It contains the source of the static website published by the publication environment.
- a _generated_ repository - The repository that contains the result of processing the publication repository using a CI/CD flow.
- a _publication point_ - A structure describing the data specification to be published as a commit in a thema repository.
- a _PURI content_ repository - The repository containing the machine readable representations for the SEMIC PURI service.
- (SEMIC) _toolchain_ - the name given to the complete setup of editorial tooling to create and publish (automatically) artefacts for data specifications.

- a data specification _artefact_ - A representation of the data specification, can be named after the format or target audience.
- <a name="tool_int_rep"></a> the _toolchain internal representation_ - All the content of a data specification in a format optimal for the artefact generators.
- <a name="art_gen"></a> an _artefact generator_ - A tool able to generate a data specification artefact from the data specification's internal representation.

- <a name="mast_data_mngm"></a> _master data management_ - the data management principle in which one identifies the origin of data (the master) and with that knowledge the use of the data is organised so that a change in the master will propogate throughout the whole usage chain. 


- <a name="json_ld"></a> JSON-LD - JSON for Linking Data, https://json-ld.org/ ; A JSON-based Serialization for Linked Data, https://www.w3.org/TR/json-ld/
- <a name="shacl"></a> SHACL  - Shapes Constraint Language, https://www.w3.org/TR/shacl/
- {#xsd} XSD - W3C XML Schema Definition Language, https://www.w3.org/TR/xmlschema11-1/
- <a name="cd_ci" > CD/CI - Continous Development/Continous Integration: an approach in software development to automate the connection between a code change and the software artefacts in a running service. https://en.wikipedia.org/wiki/CI/CD
- <a id="sem_web"> Semantic Web </a>- the web of data, interlinked data through semantical links, https://en.wikipedia.org/wiki/Semantic_Web
- <a name="reg_test" > regression testing </a> - a software testing approach oriented to the detection of loss of functionality when developing new features.
- <a id="data_spec"></a> data specification - a document describing the semantical agreements for data shared within an context.

<br><br><br><br><br><br><br><br><br><br><br><br><br><br>