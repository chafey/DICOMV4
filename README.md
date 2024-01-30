# DICOMV4

## Benefits

- Improved Security
- Improved Performance
- Improved Safety

## Strategy

- Backwards compatible with DICOMv3
  - Example - All DICOMv3 SOP Instances shall be importable to DICOMv4 but not necessarily the reverse
- Deprecate things that are not in line with the target benefits
  - Example - deprecate Implicit Little Endian Transfer syntax since VRs are needed to safely parse the object
  - Example - deprecate transfer syntaxes that are slow (e.g. JPEG2000) or limited (e.g. do not support signed 16 bit pixel data)
  - Example - deprecate non RGB uncompressed photometric interpretation (to eliminate US Green image issue!)
- Constrain things that are not in line with the target benefits
  - Example - Promote some T2/T3 attributes to T1 (e.g. patient name, patient id, issuer of patient id)
- Clarify things that are not in line with the target benefits
  - Example -
- Expand capabilities that are in line with the target benefits
  - Example: Change VR for Rows/Columns to support images > 65535x65535
