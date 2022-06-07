# Editorial flow

An editorial flow is initiated when issues for a data specification are to be adressed.
This section provides a high level overview how the editor will interact with the SEMIC GitHub space to execute this task.

First the editorial flow is described generically, at design level. 
The generic flow is then made more concrete with an example.

# Generic editorial flow


![Generic editorial flow](./images/editorial-flow-generic.jpg)


The editorial flow consist of 6 steps:

1. Find the latest UML master data.

   The editor selects the data specification GitHub repository that contains the latest published artefacts to determine the source information.
   From that repository the UML file is copied to the uri.semic.eu-thema repository.


2. Edit the UML file in [uri.semic.eu-thema]

   The editor opens and edits the UML file in the appropriate UML editor. 
   Then the UML structure is adapted to resolve the issue. 
   The UML structure is changed according to the [toolchain UML data model requirements](./datamodel.md). 

   The changed UML file is committed in the uri.semic.eu-thema repository.

3. Trigger the toolchain

   The editor triggers the rendering of the data specification artefacts by adding a publication point in the [publication reposiory](https://github.com/SEMICeu/uri.semic.eu-publication).

4. Check the generated artefacts

   When the toolchain processing is finished the artefacts are available in the [generated repository](https://github.com/SEMICeu/uri.semic.eu-generated).

   If the artefacts address the issue as expected the editor continues with the publication (step 5), otherwise another iteration is required (back to step 2 ).

5. Publish the generated artefacts 


   To provide the consumers access to the updated artefacts, the editor must publish the generated artefacts to the right places by copying the content to other GitHub repositories.
   
   This consists of copying artefacts to the data specification repository from where the editorial flow was started. 
   This must be done in accordance with the guidelines on these data specification repositories, for instance by creating a new release directory.

   Another repository might be affected to: namely when the edit resulted in a RDF content change for a persistent URI.
   Then the RDF artefact data has to changed according to the steps documented in [uri.semic.eu-puris](https://github.com/SEMICeu/uri.semic.eu-puris).

6. Verify the published artefacts 

   To finalise the editorial flow a final verifaction of the published data specification is adviced.
   The editor will then take the role of the consumer to investigate if the new situation is as desired.


## NOTE: generation and publication require manual effort

The workflow above shows that the artefact generation tooling (the toolchain) does not releaves editors from substantial manual work.
This manual work happens at the start of the editorial flow and at the end.
In both cases the work introduces risks for unnoticed changes or incomplete publications.

To reduce these risks additional work has to be done to further integrate the artefact generation into the data specification repositories and vice versa.
This is feasible, but probably will require further alignment and restructuring of the data specification repositories in the SEMIC GitHub space.
Topics like version numbering, using shared PURI domain, etc. are affecting the automation.



# Example editorial flow

To illustrate the generic editorial flow consider the common change request to add a property to a class in a data specification. 

The text below is summerized transcript of a video recording demonstrating the addition of a new property 'baptimal name' to the class Person in the Core Person Vocabulary.
The video recordings are:
 
   - [part 1](./images/step1.mp4)
   - [part 2](./images/step2.mp4)
   - [part 3](./images/step3.mp4)

All demonstrated changes are performed on separate branch called `example`. 
Using this branch all activities can demonstrated on a working environment, except for the last step: the official publication of the transformation.

This elaborated scenario shows the minimal steps to use  


## part 1 - change the UML model ( [video](./images/step1.mp4) )

1. Find the latest UML master data.

    In the [Core Person Vocabulary](https://github.com/SEMICeu/Core-Person-Vocabulary/tree/master/releases/2.00/uml) repository the latest published UML file is located.
    Copy this version to the [uri.semic.eu-thema](https://github.com/SEMICeu/uri.semic.eu-thema) for editing.
    

2. Edit the UML file in [uri.semic.eu-thema](https://github.com/SEMICeu/uri.semic.eu-thema)

   The editor edits the copy and adds the property 'baptimalName' with the annotations: the label in English, definition and the assigned URI. 
   After finishing the editing, the editor commits the UML file to the thema repository.
   
## part 2 - build the artefacts using the toolchain ( [video](./images/step2.mp4) )

3. Trigger the toolchain 

   The editor selects the commit hash corresponding to the UML file update in the thema repository. 
   Using this commit hash the [publication points](https://github.com/SEMICeu/uri.semic.eu-publication/blob/example/config/dev/publication.json) in the publication repository are updated. 
   In the demonstration video the `branchtag` attribute of the publication points is updated with the new commit hash.
   This change will trigger the artefact generation process.
   The progress of the generation process can be followed in [CircleCI](http://circleci.com).


## part 3 - publish the result ( [video](./images/step3.mp4) )

4. Check the generated artefacts

   When the artefact generation processs is finished, the generated artefacts are available in the generated repository.
   In the demonstration video, the updated artefacts are found within the directory [`/doc`](https://github.com/SEMICeu/uri.semic.eu-generated/tree/example/doc). 

   To prepare the next step, the editor checks the generated artefacts whether the result is correct: e.g. if the property is present in all relevant artefacts.
   There are several ways to check this: the editor can download the artefacts and checks within the downloaded files for the new property, or alternatively the editor can use the GitHub built in diffing support.

5. Publish the generated artefacts 

   (Note) This and the subsequent step are only partially shown in the recording. 
   In order to demonstrate the steps would require to propagate the demonstration content to the consumers on an official channel.
   Therefore only the changes that do not lead to immediate and direct impact to the consumers are included in the video.

   (not in recording) To share the new artefacts with the public the editor follows the publication guidelines for Core Person repository. 
   For that the editor use the version (release number) of the data specification.
   First, a directory named after the version is created in the Core Person Vocabulary repository in the releases directory.
   Because the editor must ensure that no information of the previous release of the Core Person Vocabulary is lost in the new release, it is advised to initiated the content of that directory with the content of the previous release.
   Then the artefacts from the generated repository in the directory `/doc/core-vocabulary/core-person/` are copied into this directory.
   Committing this will make the content available to the public.


   (in recording) Since the `baptismal name` is a new property and thus got a new PURI assigned, the editor has to publish the content in the repository uri.semic.eu-puris.
   The editor extracts from the generated RDF artefact the triples that are relating to the new property, and store these in a file with the name 'baptimalName'. 
   A variant for the RDF serialization ntriples, turtle, and RDF/XML with the approporiate file extension is then created.
   The editor will commit these files in the directory `releases/m8g` in the repository uri.semic.eu-puris.

   

6. Verify the published artefacts 
    
   (not in recording) All the steps above result in the page  `https://semiceu.github.io/Core-Person-Vocabulary/releases/{version}/`. 
   This is public URL for the html representation of the Core Vocabulary. 
   On this page the data specification is described and all artefacts and contextual information can be found.
   By doing a final check of this URL, the editor ensures quality of work.
   
    
    
