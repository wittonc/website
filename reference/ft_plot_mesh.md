---
title: ft_plot_mesh
---
```
 FT_PLOT_MESH visualizes a surface or volumetric mesh, for example describing the
 realistic shape of the head. Surface meshes should be described by triangles and
 contain the fields "pos" and "tri". Volumetric meshes should be described with
 tetraheders or hexaheders and have the fields "pos" and "tet" or "hex".

 Use as
   ft_plot_mesh(mesh, ...)
 or if you only want to plot the 3-D vertices
   ft_plot_mesh(pos, ...)

 Optional arguments should come in key-value pairs and can include
   'facecolor'    = [r g b] values or string, for example 'brain', 'cortex', 'skin', 'black', 'red', 'r', or an Nx3 or Nx1 array where N is the number of faces
   'vertexcolor'  = [r g b] values or string, for example 'brain', 'cortex', 'skin', 'black', 'red', 'r', or an Nx3 or Nx1 array where N is the number of vertices
   'edgecolor'    = [r g b] values or string, for example 'brain', 'cortex', 'skin', 'black', 'red', 'r'
   'faceindex'    = true or false
   'vertexindex'  = true or false
   'facealpha'    = transparency, between 0 and 1 (default = 1)
   'edgealpha'    = transparency, between 0 and 1 (default = 1)
   'surfaceonly'  = true or false, plot only the outer surface of a hexahedral or tetrahedral mesh (default = false)
   'vertexmarker' = character, e.g. '.', 'o' or 'x' (default = '.')
   'vertexsize'   = scalar or vector with the size for each vertex (default = 10)
   'unit'         = string, convert to the specified geometrical units (default = [])
   'maskstyle',   = 'opacity' or 'colormix', if the latter is specified, opacity masked color values
                    are converted (in combination with a background color) to rgb. This bypasses
                    openGL functionality, which behaves unpredictably on some platforms (e.g. when
                    using software opengl)

 If you don't want the faces, edges or vertices to be plotted, you should specify the color as 'none'.

 Example
   [pos, tri] = mesh_sphere(162);
   mesh.pos = pos;
   mesh.tri = tri;
   ft_plot_mesh(mesh, 'facecolor', 'skin', 'edgecolor', 'none')
   camlight

 You can plot an additional contour around specified areas using
   'contour'           = inside of contour per vertex, either 0 or 1
   'contourcolor'      = string, color specification
   'contourlinestyle'  = string, line specification 
   'contourlinewidth'  = number

 See also FT_PLOT_HEADSHAPE, FT_PLOT_HEADMODEL, TRIMESH, PATCH
```
