---
title: ft_headmodel_concentricspheres
---
```
 FT_HEADMODEL_CONCENTRICSPHERES creates a volume conduction model
 of the head based on three or four concentric spheres. For a 3-sphere
 model the spheres represent the skin surface, the outside of the
 skull and the inside of the skull For a 4-sphere model, the surfaces
 describe the skin, the outside-skull, the inside-skull and the inside of the
 cerebro-spinal fluid (CSF) boundaries.

 The innermost surface is sometimes also referred to as the brain
 surface, i.e. as the outside of the brain volume.

 This function takes as input a single headshape described with
 points and fits the spheres to this surface. If you have a set of
 points describing each surface, then this function fits the spheres
 to all individual surfaces.

 Use as
   headmodel = ft_headmodel_concentricspheres(mesh, ...)

 Optional input arguments should be specified in key-value pairs and can include
   conductivity = vector with the conductivity of each compartment
   fitind       = vector with indices of the surfaces to use in fitting the center of the spheres
   order        = number of iterations in series expansion (default = 60)

 See also FT_PREPARE_VOL_SENS, FT_COMPUTE_LEADFIELD
```
