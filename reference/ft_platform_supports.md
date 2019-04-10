---
title: ft_platform_supports
---
```
 FT_PLATFORM_SUPPORTS returns a boolean indicating whether the current platform
 supports a specific capability

 Use as
   status = ft_platform_supports(what)
 or
   status = ft_platform_supports('matlabversion', min_version, max_version)

 The following values are allowed for the 'what' parameter, which means means that
 the specific feature explained on the right is supported:

   'which-all'                     which(...,'all')
   'exists-in-private-directory'   exists(...) will look in the /private subdirectory to see if a file exists
   'onCleanup'                     onCleanup(...)
   'alim'                          alim(...)
   'int32_logical_operations'      bitand(a,b) with a, b of type int32
   'graphics_objects'              graphics sysem is object-oriented
   'libmx_c_interface'             libmx is supported through mex in the C-language (recent MATLAB versions only support C++)
   'images'                        all image processing functions in FieldTrip's external/images directory
   'signal'                        all signal processing functions in FieldTrip's external/signal directory
   'stats'                         all statistical functions in FieldTrip's external/stats directory
   'program_invocation_name'       program_invocation_name() (GNU Octave)
   'singleCompThread'              start MATLAB with -singleCompThread
   'nosplash'                      start MATLAB with -nosplash
   'nodisplay'                     start MATLAB with -nodisplay
   'nojvm'                         start MATLAB with -nojvm
   'no-gui'                        start GNU Octave with --no-gui
   'RandStream.setGlobalStream'    RandStream.setGlobalStream(...)
   'RandStream.setDefaultStream'   RandStream.setDefaultStream(...)
   'rng'                           rng(...)
   'rand-state'                    rand('state')
   'urlread-timeout'               urlread(..., 'Timeout', t)
   'griddata-vector-input'         griddata(...,...,...,a,b) with a and b vectors
   'griddata-v4'                   griddata(...,...,...,...,...,'v4') with v4 interpolation support
   'uimenu'                        uimenu(...)
   'weboptions'                    weboptions(...)
   'parula'                        parula(...)
   'html'                          html rendering in desktop

 See also FT_VERSION, VERSION, VER, VERLESSTHAN
```
