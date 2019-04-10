---
title: ft_selectdata
---
```
 FT_SELECTDATA makes a selection in the input data along specific data
 dimensions, such as channels, time, frequency, trials, etc. It can also
 be used to average the data along each of the specific dimensions.

 Use as
  [data] = ft_selectdata(cfg, data, ...)

 The cfg argument is a configuration structure which can contain
   cfg.tolerance   = scalar, tolerance value to determine equality of time/frequency bins (default = 1e-5)

 For data with trials or subjects as repetitions, you can specify
   cfg.trials      = 1xN, trial indices to keep, can be 'all'. You can use logical indexing, where false(1,N) removes all the trials
   cfg.avgoverrpt  = string, can be 'yes' or 'no' (default = 'no')

 For data with a channel dimension you can specify
   cfg.channel     = Nx1 cell-array with selection of channels (default = 'all'), see FT_CHANNELSELECTION
   cfg.avgoverchan = string, can be 'yes' or 'no' (default = 'no')
   cfg.nanmean     = string, can be 'yes' or 'no' (default = 'no')

 For data with channel combinations you can specify
   cfg.channelcmb     = Nx2 cell-array with selection of channels (default = 'all'), see FT_CHANNELCOMBINATION
   cfg.avgoverchancmb = string, can be 'yes' or 'no' (default = 'no')

 For data with a time dimension you can specify
   cfg.latency     = scalar or string, can be 'all', 'minperiod', 'maxperiod', 'prestim', 'poststim', or [beg end], specify time range in seconds
   cfg.avgovertime = string, can be 'yes' or 'no' (default = 'no')
   cfg.nanmean     = string, can be 'yes' or 'no' (default = 'no')

 For data with a frequency dimension you can specify
   cfg.frequency   = scalar or string, can be 'all', or [beg end], specify frequency range in Hz
   cfg.avgoverfreq = string, can be 'yes' or 'no' (default = 'no')
   cfg.nanmean     = string, can be 'yes' or 'no' (default = 'no')

 If multiple input arguments are provided, FT_SELECTDATA will adjust the individual inputs
 such that either the intersection across inputs is retained (i.e. only the channel, time,
 and frequency points that are shared across all input arguments), or that the union across
 inputs is retained (replacing missing data with nans). In either case, the order (e.g. of
 the channels) is made consistent across inputs.  The behavior can be specified with
   cfg.select      = string, can be 'intersect' or 'union' (default = 'intersect')

 See also FT_DATATYPE, FT_CHANNELSELECTION, FT_CHANNELCOMBINATION
```
