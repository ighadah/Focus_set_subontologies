# Focus_set_subontologies
This repository contains the focus set subontology generator, and all the verification methods described in my doctoral thesis: "Focus Set Subontologies and Semantic Difference for Large ELH Ontologies"

* To compute focus set subontologies:

java -jar  Compute_Focus_set_subontologies.jar <ontology_path/O.owl> <signature_path/sig.owl> <output_path/subontology.owl>

* To verify that the transitive closure of the subontology is equal to the transitive closure of the source ontology restricted to the signature of the subontology:

java -jar Subontology_verification_TR.jar <subontology_path/subontology.owl> <sourceontology_path/source_ontology.owl>

* To check if the logical strength of the abstracted definitions is equal to (or weaker than) the original definitions in the source ontology:

1. Compute a copy of the source ontology which contains the abstracted definitions for chosen set of focus concepts. To do that, we use the subontology that were computed for the chosen focus set, then create a copy ontology of the source ontology where the original definitions for the chosen focus set are substituted by the abstracted definitios for the focus set in the subontology:

java -jar DefinitionsSubstitutions.java <path_to_subontology/subontology.owl> <path_to_sourceontology/source_ontology.owl> <output_path/ontology_after_substitution.owl> 

2. Using the output ontology (after definitions substitution), we check if the old definitions in the source ontology entail the abstracted definitions. The entailment check is done using the Hermit reasoner:

java -jar check_entailments_focus_set_defs.jar <path_to_ontology/O_with_new_definitions.owl> <path_to_ontology/O_with_old_definitions.owl> <path_to_subontology/subontology_of_new_definitions.owl>

As can be seen, we use the subontology in step 2, because from the subontology we want get those concepts that are labelled “focus concepts” to use them during the entailment check.

* To verify that the focus set definitions in a subontology is equivalent to the original definitions in the source ontology, we can check if there is a logical difference between both definitions using uniform interpolation:

java -jar ELH_UI_DIFF_PCK_7-3_NDR.jar <sourceontology_path/source_ontology.owl> <subontology_path/subontology.owl> <output_folder_path>

Calling ELH_UI_DIFF_PCK_7-3_NDR.jar in this way means that we check UIDiff(O,S), where O is the source ontology and S is the subontology, i.e., we see if there is a logical difference in S that is not entailed by the source ontology. 

Calling ELH_UI_DIFF_PCK_7-3_NDR.jar in the opposite way to check UIDiff(S,O) means that we see if the source ontology O has a logical difference that is not entailed by the subontology S.

The jar file: ELH_UI_DIFF_PCK_7-3_NDR.jar is based on the ELH forgetter developed by [gdhzLZ](https://github.com/gdhzLZ/ELH-forgetting).

All the data for the experiments described in Section 5.5 of my thesis is [here](https://tinyurl.com/evaluation-data). 

