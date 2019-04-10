---
title: ft_headmodel_halfspace
---
```
 FT_HEADMODEL_HALFSPACE creates an EEG volume conduction model that
 is described with an infinite conductive halfspace. You can think
 of this as a plane with on one side a infinite mass of conductive
 material (e.g. water) and on the other side non-conductive material
 (e.g. air).

 Use as
    headmodel = ft_headmodel_halfspace(mesh, Pc, ...)
 where
   mesh.pos = Nx3 vector specifying N points through which a plane is fitted
   Pc       = 1x3 vector specifying the spatial position of a single point that
              is lying in the conductive halfspace

 Additional optional arguments should be specified as key-value pairs and can include
   'sourcemodel'  = string, 'monopole' or 'dipole' (default = 'dipole')
   'conductivity' = number,  conductivity value of the conductive halfspace (default = 1)

 See also FT_PREPARE_VOL_SENS, FT_COMPUTE_LEADFIELD
```
