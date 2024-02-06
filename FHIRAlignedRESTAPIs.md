# FHIR Aligned REST APIs

Misc notes

1. Map each IOD Module to an independet FHIR Resource
   1. For overlapping data items (like Patient Resource / Patient IOD Module) use the existing FHIR resource(s)
   2. For non overlapping resources (like CT Image, Series, etc), create new resources
2. Use FHIR types rather than DICOM Types (VRs)
3. Binary data (pixel data, luts, etc) would be stored externally to the resource with a link to that resource embedded in it
   1. Last time I checked, FHIR didn't have good support for large binary objects so this may need to be enhanced
   2. Alternatively, DICOM could define a mechanism to load large binary data independently of FHIR
4. Binary data should be referencable using a hash of the data
   1. Eliminates duplicate id issues
   2. Adds a level of verification of the data contents
   3. Enables data to be de-duped reducing costs
5. It is assumed that these FHIR aligned resources would be standardized and maintained as part of the DICOM standard, not the HL7 FHIR standard
   1. This would introduce a dependency of the DICOM standard on HL7 FHIR. Need to explore what this means to the DICOM standard
   2. An alternative is to make this an HL7 FHIR initiative, but would require revisiting the [agreement between HL7 and DICOM to not compete with each other](https://dicom.nema.org/Partnerships/HL7/DICOM_HL7_MOA.pdf)
6. Private Tags would not be stored in these FHIR resources.
   1. FHIR Custom resources could be used for this
   2. Alternatively, DICOM could define a service for these somehow - perhaps overlapped with the large binary storage mechanism described above
7. There would be no support for transcoding - clients would need to be able to decode all transfer syntax/codecs that are part of DICOMv4 (hopefully a smaller number)
   1. Transcoding increases costs and slows performance so should be avoided
8. FHIR's [search](https://www.hl7.org/fhir/search.html)/[bundling](https://build.fhir.org/bundle.html) mechanisms can be used to do partial metadata loads for improved performance compared to DICOMweb
   1. For example, if a client just needs to display an image, it only needs to get the [Image Pixel](https://dicom.nema.org/medical/dicom/current/output/chtml/part03/sect_C.7.6.3.html) Resource and the actual pixel data
      a. NOTE - most image compression codecs include a header with everything needed to display the image which may eliminate the need for some (or all) of the Image Pixel module attributes
9. This strategy does not mean that an EHR would replace the need for a VNA or PACS archive. An EHR could certainly do this, but a stand alone FHIR server (HAPPI) could also do it and a PACS/VNA could also implement it (along witht he patient resource, etc).
   1. There is some work being done in the area of [federating multiple FHIR stores](http://hl7.org.au/fhir/pd/federation.html) together which could be used to integrate EHR and PACS/VNA FHIR stores together
10. Would bring FHIR infrastructure to the DICOM world.
    1. SMART on FHIR for AuthC/AuthZ
    2. Ability to update/delete data
    3. Bundles
    4. Search

## References

- [Grahame Grieve BLOG on DICOM and FHIR](http://www.healthintersections.com.au/?p=1328)
- [Example of DICOM/FHIR combined in real world](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9299327/)
- [NAMIC project on mapping DICOm to FHIR](https://projectweek.na-mic.org/PW30_2019_GranCanaria/Projects/DICOMSRTID1500-FHIR/)
