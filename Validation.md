# Validation

Note - raw notes below, needs more work!

- A "validator" refers to a product that will vouch for a certain level of comformance for a dataset (e.g. a specific group of SOP instances)
- A "validator" could vouch for a dataset by creating a digital signature for the dataset and storing it with that dataset in an archive
- A "consuming application" can request the digital signature for a given dataset in an archive, verify its public key against a list of acceptable validators and verify the dataset matches what was signed using the digital signature
- This mechanism could be used along with the new concepts of a "Transaction" or "Shape" as well

## Example

- A vendor archive product could run the [dciodvfy](https://www.dclunie.com/dicom3tools/dciodvfy.html) tool against all data it receives. If the data passes, it could use its public key to sign the dataset and expose the signature via a REST API call. A client (like OHIF) could be configured to only load datasets that have been digitally signed using that vendors public key. QIDO-RS/CFIND would be extended to only return results that have been signed with specific public keys (passed in by the SCU/Client). When OHIF goes to load the dataset, it would obtain the digital signature from the archive and verify it against the retrieved dataset. If the signature checks out, it would display the data. If the signature does not pass, an error is displayed
