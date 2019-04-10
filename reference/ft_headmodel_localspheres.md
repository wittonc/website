---
title: ft_headmodel_localspheres
---
```
 FT_HEADMODEL_LOCALSPHERES constructs a MEG volume conduction model in
 with a local sphere fitted to the head or brain surface for each separate
 channel

 This implements
   Huang MX, Mosher JC, Leahy RM. "A sensor-weighted overlapping-sphere
   head model and exhaustive head model comparison for MEG." Phys Med
   Biol. 1999 Feb;44(2):423-40

 Use as
   headmodel = ft_headmodel_localspheres(mesh, grad, ...)

 Optional arguments should be specified in key-value pairs and can include
   radius    = number, radius of sphere within which headshape points will
               be included for the fitting algorithm
   maxradius = number, if for a given sensor the fitted radius exceeds
               this value, the radius and origin will be replaced with the
               single sphere fit
   baseline  = number
   feedback  = boolean, true or false

 See also FT_PREPARE_HEADMODEL, FT_PREPARE_VOL_SENS, FT_COMPUTE_LEADFIELD
```
