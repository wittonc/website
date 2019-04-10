---
title: ft_plot_cloud
---
```
 FT_PLOT_CLOUD visualizes spatially sparse scalar data as points, spheres,
 discs, or spherical clouds of points and optionally 2D slices through the 
 spherical clouds

 Use as
   ft_plot_cloud(pos, val, ...)
 where the first argument are the sensor positions and the second argument are the
 sensor values.

 Optional input arguments should come in key-value pairs and can include
   'cloudtype'          = 'point' plots a single 2D point at each sensor position (see plot3)
                          'cloud' (default) plots a group of spherically arranged points at each sensor position
                          'surf' plots a single spherical surface mesh at each sensor position
                          'disc' plots a single cylindrical disc at each sensor position aligned with the mesh (required)
   'scalerad'           = scale radius with val, can be 'yes' or 'no' (default = 'yes')
   'radius'             = scalar, maximum radius of cloud (default = 4)
   'clim'               = 1x2 vector specifying the min and max for the colorscale
   'unit'               = string, convert the sensor array to the specified geometrical units (default = [])
   'mesh'               = string or Nx1 cell-array, triangulated mesh(es), see FT_PREPARE_MESH
   'slice'              = requires 'mesh' as input (default = 'none')
                          '2d', plots 2D slices through the cloud with an outline of the mesh
                          '3d', draws an outline around the mesh at a particular slice

 The following inputs apply when 'cloudtype' = 'cloud'
   'rmin'               = scalar >= 1, minimum radius of cloud if scalerad = 'yes' (default = 1)
   'colormap'           = colormap for functional data, see COLORMAP
   'colorgrad'          = 'white' or a scalar (e.g. 1), degree to which color of points
                          in cloud changes from its center
   'ptsize'             = scalar, size of points in cloud (default = 1)
   'ptdensity'          = scalar, density of points in cloud (default = 20)
   'ptgradient'         = scalar, degree to which density of points in cloud changes
                          from its center, default = .5 (uniform density)

 The following options apply when 'cloudtype' = 'point'
   'marker'          = marker type representing the channels, see plot3 (default = '.')

 The following inputs apply when 'slice' = '2d' or '3d'
   'ori'                = 'x', 'y', or 'z', specifies the orthogonal plane which will be plotted (default = 'y')
   'slicepos'           = 'auto' or Nx1 vector specifying the position of the
                          slice plane along the orientation axis (default = 'auto': chooses slice(s) with
                          the most data)
   'nslices'            = scalar, number of slices to plot if 'slicepos' = 'auto (default = 1)
   'minspace'           = scalar, minimum spacing between slices if nslices>1
                          (default = 1)
   'intersectcolor'     = string, Nx1 cell-array, or Nx3 vector specifying line color (default = 'k')
   'intersectlinestyle' = string or Nx1 cell-array, line style specification (default = '-')
   'intersectlinewidth' = scalar or Nx1 vector, line width specification (default = 2)

 The following inputs apply when 'cloudtype' = 'surf' and 'slice' = '2d'
   'ncirc'           = scalar, number of concentric circles to plot for each
                       cloud slice (default = 15) make this hidden or scale
   'scalealpha'      = 'yes' or 'no', scale the maximum alpha value of the center circle
                       with distance from center of cloud

 See also FT_ELECTRODEPLACEMENT, FT_PLOT_TOPO, FT_PLOT_TOPO3D
```
