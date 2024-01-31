# DICOMV4

This repository contains collective thoughts about what DICOMv4 could possibly be from a community of people that coordinate on a [discord server](https://discord.gg/DwGrgSQh). Anyone is welcome
to join the community to learn, observe and contribute. Feel free to submit pull requests against this repo with your changes and they will be reviewed there before merging. If
the discord link expires, please [message me on linkedin](https://www.linkedin.com/in/chafey/) to update it.

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

1. Deprecate transfer syntaxes to reduce the number of codecs required

   - 1.2 - Implict Little Endian - all data should be explicit
   - 1.2.1.99 - Deflated Explict - Compression should be done via HTTP content encoding
   - 1.2.2 - Explicit Big Endian - No need for big endian anymore
   - 1.2.4.50 - JPEG Baseline (lossy 8 bit) - replace with new transfer syntax JPEG-XL which is faster, higher compression ratio and does not degrade JPEG Baseline images
   - 1.2.4.51 - JPEG Baseline (lossy 12 bit) - rarely used, slower than other codecs, limited to 12 bits
   - 1.2.4.57 - JPEG Lossless - limited to unsigned data, poor compression ratio, slower than HTJ2K
   - 1.2.4.70 - JPEG Lossless - limited to unsigned data, poor compression ratio, slower than HTJ2K
   - 1.2.4.80 - JPEG LS Lossless - slower thank HTJ2K, limited to unsigned data
   - 1.2.4.81 - JPEG LS Lossy - slower thank HTJ2K, limited to unsigned data
   - 1.2.4.90 - JPEG 2000 Lossless - slower thank HTJ2K
   - 1.2.4.91 - JPEG 2000 Lossy - slower thank HTJ2K
   - 1.2.4.92 - JPEG 2000 Multicomponent Lossless - rarely used
   - 1.2.4.93 - JPEG 2000 Multicomponent Lossy - rarely used
   - 1.2.5 - RLE - poor compression ratio

2. Deprecate non RGB uncompressed photometric interpretation (to eliminate US Green image issue!)
3. Deprecate support for unencrypted DIMSE connetions (require TLS)
4. Deprecate support for undefined lengths in DICOM P10 (require lengths be emitted)
5. Promote some T2/T3 attributes to T1
   - Patient Name
   - Patient ID
   - Issuer of Patient ID
   - Min/Max Pixel Value
6. Replace use of split DA/TM attributes (e.g. Study Date/Time) with a timestamp that includes the timezone
7. Deprecate uncompressed transfer syntaxes (require use of a compressed transfer syntax)
8. Deprecate transcoding functionality
9. Deprecate frame fragmentation
10. Require Basic Offset Table for multi-frame instances

### Breaking Changes

1. Change VR for Rows/Columns to support images > 65535x65535 (lower costs/higher performance for Digital Pathology images via JPIP)
2. Change VR for Accession Number to LO to support longer real world values

### New Capabilities

1. Add transfer syntax for JPEG-XL. JPEG-XL is a better "JPEG baseline" - higher compression ratios, faster encode/decode and does not degrade lossy JPEG image quality
2. Add new "FHIR aligned" REST APIs
   - Expose IOD Modules as individual resources
   - Adopt FHIR type system
   - Utilize/Integrate with FHIR resources that overlap with DICOM information model (e.g. Patient, ServiceRequest, DiagnosticReport resources)
   - SMART on FHIR for AuthC/AuthZ
3. Make pixel data immutable and referencable via a hash
4. New concepts:
   - Transaction - refers to a group of instances created together (e.g. all images in a single acquisition). Will help solve the problem "do I have all instances?"
   - Shape - refers to how a group of ImageFrames should be displayed - 2D Image, 3D Volume, 4D Volume, Cine Clip.

## Open Issues

1. How can we make the data more reliable? Some tags like Min/Max Pixel value are useful but unreliable (may not be present or just plain wrong)
2. How can we establish authenticity/lineage of data?
   - Probably some kind of digital signature
3. Add a concept of "validator" which digitally signs DICOM objects once they have been validated. This will allow clients to validate against the public key of known validators to improve the level of interoperability

## TODO

- Add pages for each of the items above with expanded descriptions/information/links/diagrams
- Review Kevin O'Donnels list of changes and add things to deprecate/clarify/constrain that align with benefits above
- Review this [linked in post](https://www.linkedin.com/posts/chafey_securitythe-state-of-being-free-from-d-activity-7153796612874493952-sC_7?utm_source=share&utm_medium=member_desktop) for things to add to this list

## Other related links

[Link](https://atlas.mindmup.com/2024/01/124350c0bfa311eeb7518d9e25e196ca/security_the_state_of_being_free_from_d/index.html) to a mindmap I created on security/safety issues in DICOM
