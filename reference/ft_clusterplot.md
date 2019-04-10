---
title: ft_clusterplot
---
```
 FT_CLUSTERPLOT plots a series of topographies with highlighted clusters.

 Use as
   ft_clusterplot(cfg, stat)
 where the input data is obtained from FT_TIMELOCKSTATISTICS or FT_FREQSTATISTICS.

 The configuration options can be
   cfg.alpha                     = number, highest cluster p-value to be plotted max 0.3 (default = 0.05)
   cfg.highlightseries           = 1x5 cell-array, highlight option series  with 'on', 'labels' or 'numbers' (default {'on', 'on', 'on', 'on', 'on'} for p < [0.01 0.05 0.1 0.2 0.3]
   cfg.highlightsymbolseries     = 1x5 vector, highlight marker symbol series (default ['*', 'x', '+', 'o', '.'] for p < [0.01 0.05 0.1 0.2 0.3]
   cfg.highlightsizeseries       = 1x5 vector, highlight marker size series   (default [6 6 6 6 6] for p < [0.01 0.05 0.1 0.2 0.3])
   cfg.highlightcolorpos         = color of highlight marker for positive clusters (default = [0 0 0])
   cfg.highlightcolorneg         = color of highlight marker for negative clusters (default = [0 0 0])
   cfg.subplotsize               = layout of subplots ([h w], default [3 5])
   cfg.saveaspng                 = string, filename of the output figures (default = 'no')
   cfg.visible                   = string, 'on' or 'off' whether figure will be visible (default = 'on')

 You can also specify most configuration options that apply to FT_TOPOPLOTER or FT_TOPOPLOTTFR,
 except for cfg.xlim, any of the highlight options, cfg.comment and cfg.commentpos.

 To facilitate data-handling and distributed computing you can use
   cfg.inputfile   =  ...
 If you specify this option the input data will be read from a *.mat
 file on disk. This mat files should contain only a single variable named 'data',
 corresponding to the input structure.

 See also FT_TOPOPLOTTFR, FT_TOPOPLOTER, FT_MOVIEPLOTTFR, FT_MOVIEPLOTER
```
