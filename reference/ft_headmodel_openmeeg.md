---
title: ft_headmodel_openmeeg
---
```
 FT_HEADMODEL_OPENMEEG creates a volume conduction model of the
 head using the boundary element method (BEM). This function takes
 as input the triangulated surfaces that describe the boundaries and
 returns as output a volume conduction model which can be used to
 compute leadfields.

 This function implements
   Gramfort et al. OpenMEEG: opensource software for quasistatic
   bioelectromagnetics. Biomedical engineering online (2010) vol. 9 (1) pp. 45
   http://www.biomedical-engineering-online.com/content/9/1/45
   doi:10.1186/1475-925X-9-45
 and
   Kybic et al. Generalized head models for MEG/EEG: boundary element method
   beyond nested volumes. Phys. Med. Biol. (2006) vol. 51 pp. 1333-1346
   doi:10.1088/0031-9155/51/5/021

 This link with FieldTrip is derived from the OpenMEEG project
 with contributions from Daniel Wong and Sarang Dalal, and uses external
 command-line executables. See http://openmeeg.github.io/

 Use as
   headmodel = ft_headmodel_openmeeg(bnd, ...)

 Optional input arguments should be specified in key-value pairs and can
 include
   conductivity     = vector, conductivity of each compartment
   tissue           = tissue labels for each compartment

 See also FT_PREPARE_VOL_SENS, FT_COMPUTE_LEADFIELD, FT_SYSMAT_OPENMEEG,
          FT_SENSINTERP_OPENMEEG
```
