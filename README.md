# DICOMV4

## Benefits

- Improved Security
- Improved Performance
- Improved Safety
- Lower Costs

## Strategy

- Backwards compatible with DICOMv3
- Deprecate things that are not in line with the target benefits
- Constrain things that are not in line with the target benefits
- Clarify things that are not in line with the target benefits
- Expand capabilities that are in line with the target benefits

## List of specific Changes

### Deprecate/Clarify/Constrain V3 of the standard

1. Deprecate Implicit Little Endian Transfer syntax since VRs are needed to safely parse the object
2. Deprecate transfer syntaxes that are slow (e.g. JPEG2000) or limited (JPEG-LS, JPEG Lossless)
3. Deprecate non RGB uncompressed photometric interpretation (to eliminate US Green image issue!)
4. Deprecate support for unencrypted DIMSE connetions (require TLS)
5. Deprecate support for undefined lengths in DICOM P10 (require lengths be emitted)
6. Promote some T2/T3 attributes to T1
   - Patient Name
   - Patient ID
   - Issuer of Patient ID
7. Replace use of split DA/TM attributes (e.g. Study Date/Time) with a timestamp that includes the timezone
8. Deprecate uncompressed transfer syntaxes (require use of a compressed transfer syntax)
9. Deprecate transcoding functionality
10. Deprecate frame fragmentation
11. Require Basic Offset Table for multi-frame instances

### Breaking Changes

1. Change VR for Rows/Columns to support images > 65535x65535 (lower costs/higher performance for Digital Pathology images via JPIP)
2. Change VR for Accession Number to LO to support longer real world values

### New Capabilities

1. Add new "FHIR inspired" REST APIs
   - Expose IOD Modules as individual resources
   - Adopt FHIR type system
   - Utilize/Integrate with FHIR resources that overlap with DICOM information model (e.g. Patient, ServiceRequest, DiagnosticReport resources)
2. Make pixel data immutable and referencable via a hash
3. New concepts:
   - Transaction - refers to a group of instances created together (e.g. all images in a single acquisition). Will help solve the problem "do I have all instances?"
   - Shape - refers to how a group of ImageFrames should be displayed - 2D Image, 3D Volume, 4D Volume, Cine Clip.

## Discuss

A [discord server](https://discord.gg/DwGrgSQh) has been setup for discussion purposes, [message me on linkedin](https://www.linkedin.com/in/chafey/) if the link expires
