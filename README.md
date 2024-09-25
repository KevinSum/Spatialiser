# Overview

This is little hobby project where a binaural HRTF spatialisation algorithm is implemented in JUCE. The spatialisation algorithm is taken from the [3D Tune-In Toolkit](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0211899).

[Demo video](https://www.youtube.com/watch?v=HG9u9gKIuLM)

# Algorithm

The spatialisation algorithm involves extracting the HRIR data from a SOFA. For any chosen azimuth/elevation angle, barycentric interpolation is used on the three closest HRIRs to generate the HRIR for that position. We then perform overlapping FFT convolution with this HRIR.

![Some](https://storage.googleapis.com/plos-corpus-prod/10.1371/journal.pone.0211899/1/pone.0211899.g006.PNG_L?X-Goog-Algorithm=GOOG4-RSA-SHA256&X-Goog-Credential=wombat-sa%40plos-prod.iam.gserviceaccount.com%2F20240925%2Fauto%2Fstorage%2Fgoog4_request&X-Goog-Date=20240925T185549Z&X-Goog-Expires=86400&X-Goog-SignedHeaders=host&X-Goog-Signature=50e7bb4caa8df49cc6b8f0aeb77fdf93f22b936409c1a30a133aa4a2721692d8f990b9a4989a18ad6ea7b9cc37bce927e52b0a816cc57cd57f06cee607d1215be9ce698aa3808c8c8020dc69675111ebd8b10d4ce2c9db41760ac9b87ea7366e8c222c44cd0552dc036b4a216413240603b9c85c32a4dda3383350e5bb7db2407982d81d0b8448fed93470d1b3c444170c76a5b494971ca100459581a68ae0ea6309a7b68c0547f6a496bb4f4ec9b946bcf3992b27c1cdb609d8174ee0be92d02b80d70ab3f4a6a0027f65c53d337fc1f4037cffc042f36191051c8bf18ed8513e544b3c8e52bae0e97ce55dc983e856724f1a909a001917199d322b66bada92)

The interaural time differences (ITDs) are generated by time-stretching the input audio signal to produce the time difference between the left signal and the right signal.

# JUCE Project Setup

Projucer Exporter Settings
- Add "${LIBSOFA}", "libcurl_imp_x64.lib", "libhdf5_hl_x64.lib", "libhdf5_x64.lib", "netcdf_x64.lib" and "zlib_x64.lib" to External Librarys to Link
- Add "../../Libraries/libsofa/lib" and "../../Libraries/libsofa/dependencies/lib/win" to Extra Library Search Paths
- For Debug config, set LIBSOFA = libsofa_debug_x64.lib in Preprocessor Definitions and set Runtime Library setting to "Use static runtime"
- For Release config, set LIBSOFA = libsofa_x64.lib in Preprocessor Definitions

# Improvements that could be made
- Better ITD onset detection algorithm
