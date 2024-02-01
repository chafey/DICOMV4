# Validation

Note - raw notes below, needs more work!

- A "validator" refers to a product that will vouch for a certain level of comformance for a dataset (e.g. a specific group of SOP instances)
- A "validator" could create a digital signature for a given dataset and store it with that dataset in an archive
- A "consuming application" can request the digital signature for a given dataset in an archive and check it against a list of known trusted validators
- Example - A vendor archive product could run the [dciodvfy](https://www.dclunie.com/dicom3tools/dciodvfy.html) tool against all data it receives. If the data passes, it could use its public key to sign the dataset and expose the signature via a REST API call. A client (like OHIF) could have already been configured to only load datasets that have been digitally signed by that vendor archive. When OHIF goes to load the dataset, it would obtain the digital signature from the archive and verify it against the retrieved dataset. If the signature checks out, it would display the data. If the signature does not pass, an error is displayed
- This mechanism could be used along with the new concepts of a "Transaction" or "Shape" as well
