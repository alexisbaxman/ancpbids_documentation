# Writting a New Dataset

Once you've queried and worked with your BIDS dataset, you may want to save processed data or generate derivative datasets. Unlike PyBIDS, ´ancpBIDS´ supports **writing new datasets directly from its in-memory graph.**
When calling ancpbids.save_dataset(), the in-memory graph materializes as a new folder on disk. This is done "schema-aware": following the syntax and the semantic BIDS specification, such as naming Artifacts with correct key-value pairs. The new folder will contain the [dataset_description.json](https://alexisbaxman.github.io/ancpbids_documentation/extra/inmemory.html#the-model-of-a-bids-dataset), with the field ´BIDSVersion´ derived directly from the schema.


The implementation is schema-aware, so the target BIDS schema must be imported and used to create the in-memory instances. For example, a Datasaet must have the 

The result of calling ancpbids.save_dataset() is a new folder on the file system which represents the materializstion of the in-memory grap.

[figure-37]

For each subject, a separate folder is created, and for each Artifact a properly
constructed file name is set. One doesn't need to explicetely set every Artifact (such as sub entity in the example above), but the implementation it's automatic thanks to the information derivable from the original subject folder.

Internally, an instance of type schema.DatasetDescriptionFile will be created. As can be seen, the field BIDSVersion has been automatically derived from the schema’s version. Other fields have been set with default values.
[figure-38]







Write a new dataset from in-memory graph
‒ Write new derivatives to existing datasets


write is exclusive of ancpbids, not in pybids



