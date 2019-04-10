---
title: ft_interpolatenan
---
```
 FT_INTERPOLATENAN interpolates time series that contains segments of nans obtained
 by replacing artifactual data with nans using, for example, FT_REJECTARTIFACT, or
 by redefining trials with FT_REDEFINETRIAL resulting in trials with gaps.

 Use as
   outdata = ft_interpolatenan(cfg, indata)
 where cfg is a configuration structure and the input data is obtained from FT_PREPROCESSING.

 The configuration should contain
   cfg.method      = string, interpolation method, see HELP INTERP1 (default = 'linear')
   cfg.prewindow   = value, length of data prior to interpolation window, in seconds (default = 1)
   cfg.postwindow  = value, length of data after interpolation window, in seconds (default = 1)
   cfg.feedback    = string, 'no', 'text', 'textbar', 'gui' (default = 'text')

 This function only interpolates over time, not over space. If you want to
 interpolate using spatial information, e.g. using neighbouring channels, you should
 use FT_CHANNELREPAIR.

 To facilitate data-handling and distributed computing with the peer-to-peer
 module, this function has the following options:
   cfg.inputfile   =  ...
   cfg.outputfile  =  ...
 If you specify one of these (or both) the input data will be read from a *.mat
 file on disk and/or the output data will be written to a *.mat file. These mat
 files should contain only a single variable, corresponding with the
 input/output structure.

 See also FT_REJECTARTIFACT, FT_REDEFINETRIAL, FT_CHANNELREPAIR
```
