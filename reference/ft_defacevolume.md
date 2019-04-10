---
title: ft_defacevolume
---
```
 FT_DEFACEVOLUME allows you to de-identify an anatomical MRI by erasing specific
 regions, such as the face and ears. The graphical user interface allows you to
 position a box over the anatomical data inside which all anatomical voxel values will
 be replaced by zero. You might have to call this function multiple times when both
 face and ears need to be removed. Following defacing, you should check the result
 with FT_SOURCEPLOT.

 Use as
   mri = ft_defacevolume(cfg, mri)

 The configuration can contain the following options
   cfg.method     = 'box', 'spm' (default = 'box')

 If you specify the box method, the following options apply
   cfg.translate  = initial position of the center of the box (default = [0 0 0])
   cfg.scale      = initial size of the box along each dimension (default is automatic)
   cfg.translate  = initial rotation of the box (default = [0 0 0])
   cfg.selection  = which voxels to keep, can be 'inside' or 'outside' (default = 'outside')
   cfg.smooth     = 'no' or the FWHM of the gaussian kernel in voxels (default = 'no')
   cfg.keepbrain  = 'no' or 'yes', segment and retain the brain (default = 'no')
   cfg.feedback   = 'no' or 'yes', whether to provide graphical feedback (default = 'no')

 If you specify no smoothing, the selected area will be zero-masked. If you
 specify a certain amount of smoothing (in voxels FWHM), the selected area will
 be replaced by a smoothed version of the data.

 The spm method does not have any options, it uses SPM_DEFACE from the
 SPM12 toolbox.

 See also FT_ANONYMIZEDATA, FT_DEFACEMESH, FT_ANALYSISPIPELINE, FT_SOURCEPLOT
```
