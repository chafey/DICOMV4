# JPEG Baseline Deprecation

## Rough notes

1. JPEG Baseline refers to the standard JPEG images that are in common use everywhere (e.g. displayable in a web browser)
2. JPEG Baseline is lossy and 8 bit only
3. Many DICOM images are encoded with JPEG Baseline (Ultrasound in particular)
4. JPEG Baseline is generally considered one of the worst codecs due to its age. Many new codecs have been introduced which are better in many ways (e.g. compression ratio, speed, image quality, features)
5. In line with the reduce costs, improve performance benefits, it makes sense to deprecate JPEG Baseline and adopt another codec which is better (particular in compression ratio and speed)
6. JPEG XL is unique in that it can transcode a JPEG Baseline image to a higher compression ratio without losing any image quality (it can be reverted back to the original JPEG baseline image bit for bit)
   1. JPEG XL is proposed to replace JPEG Baseline and provides a backwards compatibility strategy for DICOMv3 images
7. JPEG XL has been adopted by Apple (as part of the OS and Safari), Adobe and possibly Microsoft.
   1. NOTE - All major web browsers (Safari, Chrome, Firefox) integrated JPEG-XL behind a feature flag, but Google decided to deprecate it due to lack of adoption. Various browser politics in this area

## TODO

1. Need to bencmark JPEG-XL vs JPEG Baseline to see if performance is acceptable
   1. Some concern about this as some testing was done previously in this area and JPEG-XL wasn't fast enough for echo multiframe playback
