---
title: ft_conjunctionanalysis
---
```
 FT_CONJUNCTIONANALYSIS finds the minimum statistic common across two or
 more contrasts, i.e. data following ft_xxxstatistics. Furthermore, it
 finds the overlap of sensors/voxels that show statistically significant
 results (a logical AND on the mask fields).

 Alternatively, it finds minimalistic mean power values in the
 input datasets. Here, a type 'relative change' baselinecorrection
 prior to conjunction is advised.

 Use as
   [stat] = ft_conjunctionanalysis(cfg, stat1, stat2, .., statN)

 where the input data is the result from either FT_TIMELOCKSTATISTICS,
 FT_FREQSTATISTICS, or FT_SOURCESTATISTICS

 No configuration options are yet implemented.

 See also FT_TIMELOCKSTATISTICS, FT_FREQSTATISTICS, FT_SOURCESTATISTICS
```
