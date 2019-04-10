---
title: ft_artifact_muscle
---
```
 FT_ARTIFACT_MUSCLE reads the data segments of interest from file and
 identifies muscle artifacts.

 Use as
   [cfg, artifact] = ft_artifact_muscle(cfg)
 with the configuration options
   cfg.dataset     = string with the filename
 or
   cfg.headerfile  = string with the filename
   cfg.datafile    = string with the filename
 and optionally
   cfg.headerformat
   cfg.dataformat

 Alternatively you can use it as
   [cfg, artifact] = ft_artifact_muscle(cfg, data)
 where the input data is a structure as obtained from FT_PREPROCESSING.

 In both cases the configuration should also contain
   cfg.trl        = structure that defines the data segments of interest. See FT_DEFINETRIAL
   cfg.continuous = 'yes' or 'no' whether the file contains continuous data

 The data is preprocessed (again) with the following configuration parameters,
 which are optimal for identifying muscle artifacts.
   cfg.artfctdef.muscle.bpfilter    = 'yes'
   cfg.artfctdef.muscle.bpfreq      = [110 140]
   cfg.artfctdef.muscle.bpfiltord   = 8
   cfg.artfctdef.muscle.bpfilttype  = 'but'
   cfg.artfctdef.muscle.hilbert     = 'yes'
   cfg.artfctdef.muscle.boxcar      = 0.2

 Artifacts are identified by means of thresholding the z-transformed value
 of the preprocessed data.
   cfg.artfctdef.muscle.channel     = Nx1 cell-array with selection of channels, see FT_CHANNELSELECTION for details
   cfg.artfctdef.muscle.cutoff      = z-value at which to threshold (default = 4)
   cfg.artfctdef.muscle.trlpadding  = 0.1
   cfg.artfctdef.muscle.fltpadding  = 0.1
   cfg.artfctdef.muscle.artpadding  = 0.1

 The output argument "artifact" is a Nx2 matrix comparable to the
 "trl" matrix of FT_DEFINETRIAL. The first column of which specifying the
 beginsamples of an artifact period, the second column contains the
 endsamples of the artifactperiods.

 To facilitate data-handling and distributed computing you can use
   cfg.inputfile   =  ...
 If you specify this option the input data will be read from a *.mat
 file on disk. This mat files should contain only a single variable named 'data',
 corresponding to the input structure.

 See also FT_REJECTARTIFACT, FT_ARTIFACT_CLIP, FT_ARTIFACT_ECG, FT_ARTIFACT_EOG,
 FT_ARTIFACT_JUMP, FT_ARTIFACT_MUSCLE, FT_ARTIFACT_THRESHOLD, FT_ARTIFACT_ZVALUE
```
