# Introduction

## Object categorization

Marr's Vision (1970):

1. Input image: percieved intensities
2. Primal sketch: zero-crossings, blobs, edges, boundaries.
3. 2 1/2-D sketch: local surface orientation and discontinuities in depth
4. 3D model representation: 3D models, hierarchically organized in terms of surface and
    volume primitives.

## Traditional recognition pipeline

Image pixels -> hand-crafted features -> trainable classifier -> object class

### Local and global image representations

Gobal:

+ Works for small articulations
+ Handles lower resolutions
- Struggles with occlusions
- Requires lots of data

Local:

+ Handles occlusions, rotations, view changes, scale variations
- Struggles with lower resolutions

