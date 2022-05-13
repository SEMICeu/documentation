# SEMIC open issues

## generation and publication are not integrated

The generation of the artefacts and the publication of these are not integrated.
This makes that the editors have to perform manually
   - a synchronisation check before starting (does the change happens on the right version) 
   - a publication to push the resulting artifacts to all target environments:
	- the data specification repository
        - the puri repository

To avoid these errorprone activities both should be technically integrated.
This is feasible, but will require further alignment and restructuring of the data specification repositories in the SEMIC GitHub space.
Topics like version numbering, using shared PURI domain, etc. are affecting the automation.


# Example editorial flow


Example scenario: add property "baptismal name" to the class Person in Core Person Vocabulary and publish it as version 2.0.1-Example

The figure below shows the interactions with Github the editor has to perform to reach the objective of the example scenario.

![Example editorial flow](./semic-editor-flow.jpg)

1. find the latest UML master data. 
    1.1. In [Core Person Vocabulary](https://github.com/SEMICeu/Core-Person-Vocabulary/tree/master/releases/2.00/uml) the latest published file is found.
    1.2. Copy this version to the [uri.semic.eu-thema]() for editing
2. Edit the EAP file in [uri.semic.eu-thema]
    2.1. Open the EAP file in Enterprise Architect
    2.2. Add the property with the annotations 
    2.3. Commit the changed file  
3. Trigger the toolchain
    3.1. Create a new publication point in [uri.semic.eu-publication]
4. Check the generated artefacts
    4.1. When the toolchain is finished the urlref path in [uri.semic.eu-generated] contains the generated artefacts
5. Publish the generated artefacts 
    5.1. Create a new branch 2.0.1-Example in the Core Person Vocabulary repository
    5.2. Check the branch out and create a new directory in the releases called 2.0.1-Example
    5.3. Copy the content of the uri.semic.eu-generated to the created directory in 5.2
    5.4. activate a the new persistent identifier in uri.semic.eu-puris
6. Verify the published artefacts 
    
  
    
