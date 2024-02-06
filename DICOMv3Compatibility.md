# DICOM v3 Compatibility

1. DICOMv3 will continue to evolve in parallel with DICOMv4
2. DICOMv4 compliant systems shall be able to import/read DICOM v3 P10 data without any loss/degradation of data
3. DICOMv4 will make breaking changes that may not map cleanly to DICOMv3 systems (e.g. rows/columns > 65535) and could result in data loss (e.g. longer v4 accession number truncated when exported to v3)
   - DICOMv4 efforts should be mindful of how it may impact compatibility with v3 sytems, but not be restricted by this
