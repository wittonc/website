---
title: ft_omri_align_init
---
```
 function model = ft_omri_align_init(Vr,flags)

 Ripped out of SPM 8 and modified (2010, S.Klanke)

 Estimation of within modality rigid body movement parameters
 FORMAT P = spm_realign(P,flags)

 P     - matrix of filenames {one string per row}
         All operations are performed relative to the first image.
         ie. Coregistration is to the first image, and resampling
         of images is into the space of the first image.
         For multiple sessions, P should be a cell-array, where each
         cell should be a matrix of filenames.

 flags - a structure containing various options.  The fields are:
         quality - Quality versus speed trade-off.  Highest quality
                   (1) gives most precise results, whereas lower
                   qualities gives faster realignment.
                   The idea is that some voxels contribute little to
                   the estimation of the realignment parameters.
                   This parameter is involved in selecting the number
                   of voxels that are used.

         fwhm    - The FWHM of the Gaussian smoothing kernel (mm)
                   applied to the images before estimating the
                   realignment parameters.

         sep     - the default separation (mm) to sample the images.

         PW      - a filename of a weighting image (reciprocal of
                   standard deviation).  If field does not exist, then
                   no weighting is done.

         interp  - B-spline degree used for interpolation

__________________________________________________________________________

 Inputs
 A series of *.img conforming to SPM data format (see 'Data Format').

 Outputs
 If no output argument, then an updated voxel to world matrix is written
 to the headers of the images (a .mat file is created for 4D images).
 The details of the transformation are displayed in the
 results window as plots of translation and rotation.
 A set of realignment parameters are saved for each session, named:
 rp_*.txt.
__________________________________________________________________________

 The voxel to world mappings.

 These are simply 4x4 affine transformation matrices represented in the
 NIFTI headers (see http://nifti.nimh.nih.gov/nifti-1 ).
 These are normally modified by the `realignment' and `coregistration'
 modules.  What these matrixes represent is a mapping from
 the voxel coordinates (x0,y0,z0) (where the first voxel is at coordinate
 (1,1,1)), to coordinates in millimeters (x1,y1,z1).
  
 x1 = M(1,1)*x0 + M(1,2)*y0 + M(1,3)*z0 + M(1,4)
 y1 = M(2,1)*x0 + M(2,2)*y0 + M(2,3)*z0 + M(2,4)
 z1 = M(3,1)*x0 + M(3,2)*y0 + M(3,3)*z0 + M(3,4)

 Assuming that image1 has a transformation matrix M1, and image2 has a
 transformation matrix M2, the mapping from image1 to image2 is: M2\M1
 (ie. from the coordinate system of image1 into millimeters, followed
 by a mapping from millimeters into the space of image2).

 These matrices allow several realignment or coregistration steps to be
 combined into a single operation (without the necessity of resampling the
 images several times).  The `.mat' files are also used by the spatial
 normalisation module.
__________________________________________________________________________
 Ref:
 Friston KJ, Ashburner J, Frith CD, Poline J-B, Heather JD & Frackowiak
 RSJ (1995) Spatial registration and normalization of images Hum. Brain
 Map. 2:165-189
__________________________________________________________________________
 Copyright (C) 2008 Wellcome Trust Centre for Neuroimaging
```
