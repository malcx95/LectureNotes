# Compound descriptors

## Feature constellations

Both local appearance and constellations contribute to recognition.

### Deformable part models

A coarse global model where a fixed number of part models are used, with flexible
spatial arrangement.

Detection is done in a coarse pattern. Constellations are used as a verification step.

### Bags of features / Visual words

Related terms: Bags of keypoints, Bags of words, Texton histograms.

Used to quickly index large dataset, as it disregards the spatial arrangement
of the features. Spatial arrangement is verified in second step.

Descriptor space is vector quantized into K parts on a large training set.
The clustering is done in a whitened space, and each descriptor is approximated
by a visual word according to the quantization.

