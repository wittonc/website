---
title: ft_plot_ortho
---
```
 FT_PLOT_ORTHO plots 3 orthographic slices through a 3-D volume and interpolates if needed

 Use as
   ft_plot_ortho(dat, ...)
 or
   ft_plot_ortho(dat, mask, ...)
 where dat and mask are equal-sized 3-D arrays.

 Additional options should be specified in key-value pairs and can be
   'style'        = string, 'subplot' or 'intersect' (default = 'subplot')
   'orientation'  = 3x3 matrix specifying the directions orthogonal through the planes which will be plotted
   'parents'      = (optional) 3-element vector containing the handles of the axes for the subplots (when style = 'subplot')
   'surfhandle'   = (optional) 3-element vector containing the handles of the surfaces for each of the sublots (when style = 'subplot'). Parents and surfhandle are mutually exclusive
   'update'       = (optional) 3-element boolean vector with the axes that should be updated (default = [true true true])

 The following options are supported and passed on to FT_PLOT_SLICE
   'clim'                = [min max], lower and upper color limits
   'transform'           = 4x4 homogeneous transformation matrix specifying the mapping from voxel space to the coordinate system in which the data are plotted
   'location'            = 1x3 vector specifying the intersection point at which the three slices will be plotted. The coordinates should be expressed in the coordinate system of the data. 
   'datmask'             = 3D-matrix with the same size as the matrix dat, serving as opacitymap if the second input argument to the function contains a matrix, this will be used as the mask
   'maskstyle'           = string, 'opacity' or 'colormix', defines the rendering
   'background'          = needed when maskstyle is 'colormix', 3D-matrix with the same size as the data matrix, serving as grayscale image that provides the background
   'interpmethod'        = string specifying the method for the interpolation, see INTERPN (default = 'nearest')
   'colormap'            = string, see COLORMAP
   'unit'                = string, can be 'm', 'cm' or 'mm (default is automatic)
   'intersectmesh'       = triangulated mesh, see FT_PREPARE_MESH
   'intersectcolor'      = string, color specification
   'intersectlinestyle'  = string, line specification 
   'intersectlinewidth'  = number

 See also FT_PLOT_SLICE, FT_PLOT_MONTAGE, FT_SOURCEPLOT
```
