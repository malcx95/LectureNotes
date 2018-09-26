# Terminology

A feature is an aspect of an image which is useful in recognition.

An observation consists of detection and then description, that is,
where to sample and how to sample. This results in a descriptor vector.
The descriptor should be invariant to nuisance parameters, such as
illumination, translation and scale, and should have discriminant power,
such that different objects can be told apart.

# Descriptor learning

- Option 1: Train explicitly to discriminate using e.g. triplet loss.
- Option 2: Repurpose a network trained on generic problem, and use 
    intermediate layer activations as pre-trained features.

## Pros and cons

+ A learned descriptor can improve performance over hand-coded ones.
- Domain shift risk if feature training was done on different data
- More computationally expensive than designed ones

# Designed descriptors

Common in practical applications since it saves computations.
Even designed descriptors have parameters that need tuning, so a form
of learning is used here as well.

## Intensity normalisation

A very simple descriptor is the intensity normalized patch:

```
v = (vtilde - mean(vtilde))/std(vtilde)
```

where `v = [f(x1), ... f(xn)]^T`, `xn` is part of a patch

This is invariant to some nuisance parameters, such as illumination.

## The HOG descriptor

Histogram of oriented gradients. Compute gradients, compute histogram of these,
organize into blocks and normalize them.

## SIFT

Scale invariant feature transform. An interest point detector and descriptor.
Uses 4x4 HOG cells.

## Gabor Jet

A filter bank. A set of responses from oriented and organized Gabor wavelets.
Typically used for textures.

## Binary descriptors

Local binary patterns are used to save memory and time. Sign of intensity
difference is monotonically invariant to illumination. The BRIEF descriptor
uses only 256 bits. Descriptor comparison is done by `bitcnt(XOR(p, q))` which
is very efficient in some machine instruction sets.

## Gist

Global feature for images. Useful in scene categorization. Uses Gabor jets in 
4x4 grid.

## Color histograms

Transform ROI to Lab color space, use coarse binning (5x10x10 bins), select
the 218 bins that fall within the RGB gamut.

Shift insensitive, scale insensitive.

## Shape descriptors

Attempt to capture depth discontinuities and/or object boundaries. Typcially requires
segmentation.

