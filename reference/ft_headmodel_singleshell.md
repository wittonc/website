---
title: ft_headmodel_singleshell
---
```
 FT_HEADMODEL_SINGLESHELL creates a volume conduction model of the
 head for MEG based on a realistic shaped surface of the inside of
 the skull.

 The method implemented in this function allows for a simple and
 fast method for the MEG forward calculation for one shell of arbitrary
 shape, based on a correction of the lead field for a spherical
 volume conductor by a superposition of basis functions, gradients
 of harmonic functions constructed from spherical harmonics.

 This function implements
   G. Nolte, "The magnetic lead field theorem in the quasi-static
   approximation and its use for magnetoencephalography forward calculation
   in realistic volume conductors", Phys Med Biol. 2003 Nov 21;48(22):3637-52.

 Use as
   headmodel = ft_headmodel_singleshell(mesh, ...)

 Optional input arguments should be specified in key-value pairs and can include
   order        = number of iterations in series expansion (default = 10)

 See also FT_PREPARE_VOL_SENS, FT_COMPUTE_LEADFIELD
```
