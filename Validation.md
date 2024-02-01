# Validation

Note - raw notes below, needs more work!

- A "validator" refers to a product that will vouch for a certain level of comformance for a dataset (e.g. a specific group of SOP instances)
- A "validator" could vouch for a dataset by creating a digital signature for the dataset and storing it with that dataset in an archive
- A "consuming application" can request the digital signature for a given dataset in an archive, verify its public key against a list of acceptable validators and verify the dataset matches what was signed using the digital signature
- The concept of a known entity "validator" that digitall signs data "datasets" could be applied to the transaction and shape concepts as well

## Example Use Case

1. Modality sends a study with 100 SOP Instances to an Archive via DICOM CSTORE
2. Archive validates those SOP instances using [dciodvfy](https://www.dclunie.com/dicom3tools/dciodvfy.html).
3. All 100 sop instances pass validation so the archive creates a digital signature for the 100 SOP Instances using its public key and stores the digital signature in its database
4. A client (e.g. OHIF) is already configured to allow viewing of datasets that have been signed by the archives public key
5. The client queries (e.g. with CFIND/QIDO-RS) the archive for datasets and passes the list of public keys that it supports (e.g. the archives public key)
6. The archive filters the response to only return datasets that have been signed using the public keys the client provided
7. The client retrieves the a dataset along with its digital signature. It validates the data has not been tampered by checking the digital signature client side
8. The digital signature passes the check and the client displays the dataset. If the digital signature didn't check out, the viewer could warn the user or refuse to display the dataset
