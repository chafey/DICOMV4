# DICOMV4

## Benefits

- Improved Security
- Improved Performance
- Improved Safety

## Strategy

- Backwards compatible with DICOMv3
  - Example - All DICOMv3 SOP Instances shall be importable to DICOMv4 but not necessarily the reverse
- Deprecate things that are not in line with the target benefits
  - Example - deprecate Implicit Little Endian Transfer syntax since VRs are needed to safely parse the object (Safety Benefit)
  - Example - deprecate transfer syntaxes that are slow (e.g. JPEG2000) or limited (e.g. do not support signed 16 bit pixel data) (Performance Benefit)
  - Example - deprecate non RGB uncompressed photometric interpretation (to eliminate US Green image issue!) (Safety Benefit)
  - Example - deprecate support for unencrypted DIMSE connetions (require TLS) (Security Benefit)
  - Example - deprecate support for undefined lengths in DICOM P10 (require lengths be emitted) (Performance Benefit)
- Constrain things that are not in line with the target benefits
  - Example - Promote some T2/T3 attributes to T1 (e.g. patient name, patient id, issuer of patient id) (Safety Benefit)
- Clarify things that are not in line with the target benefits
  - Example -
- Expand capabilities that are in line with the target benefits
  - Example: Change VR for Rows/Columns to support images > 65535x65535 (Performance Benefit)
  - Example: Change VR for Accession number to support longer real world values (Safety Benefit)

## Discuss

A [discord server](https://discord.gg/DwGrgSQh) has been setup for discussion purposes, [message me on linkedin](https://www.linkedin.com/in/chafey/) if the link expires
