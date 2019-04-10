---
title: ft_prepare_vol_sens
---
```
 FT_PREPARE_VOL_SENS does some bookkeeping to ensure that the volume
 conductor model and the sensor array are ready for subsequent forward
 leadfield computations. It takes care of some pre-computations that can
 be done efficiently prior to the leadfield calculations.

 Use as
   [headmodel, sens] = ft_prepare_vol_sens(headmodel, sens, ...)
 with input arguments
   headmodel = structure with volume conductor definition
   sens      = structure with gradiometer or electrode definition

 The headmodel structure represents a volume conductor model of the head,
 its contents depend on the type of model. It is described in more detail
 in FT_DATATYPE_HEADMODEL. The sens structure represents a electrode or
 gradiometer array. It is described in more detail in FT_DATATYPE_SENS.

 Additional options should be specified in key-value pairs and can be
   'channel'  = cell-array with strings (default = 'all')

 The detailed behavior of this function depends on whether the input
 consists of EEG or MEG and furthermoree depends on the type of volume
 conductor model:
 - in case of EEG single and concentric sphere models, the electrodes are
   projected onto the skin surface.
 - in case of EEG boundary element models, the electrodes are projected on
   the surface and a blilinear interpoaltion matrix from vertices to
   electrodes is computed.
 - in case of MEG and a localspheres model, a local sphere is determined
   for each coil in the gradiometer definition.
  - in case of MEG with a singleshell Nolte model, the volume conduction
    model is initialized
 In any case channel selection and reordering will be done. The channel
 order returned by this function corresponds to the order in the 'channel'
 option, or if not specified, to the order in the input sensor array.

 See also FT_COMPUTE_LEADFIELD, FT_READ_HEADMODEL, FT_READ_SENS
```
