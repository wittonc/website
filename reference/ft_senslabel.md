---
title: ft_senslabel
---
```
 FT_SENSLABEL returns a list of predefined sensor labels given the
 EEG or MEG system type which can be used to detect the type of data.

 Use as
  label = ft_senslabel(type)

 The input sensor array type can be any of the following
  'ant128'
  'biosemi64'
  'biosemi128'
  'biosemi256'
  'bti148'
  'bti148_planar'
  'bti248'
  'bti248_planar'
  'btiref'
  'ctf151'
  'ctf151_planar'
  'ctf275'
  'ctf275_planar'
  'ctfheadloc'
  'ctfref'
  'eeg1005'
  'eeg1010'
  'eeg1020'
  'ext1020'
  'egi32'
  'egi64'
  'egi128'
  'egi256'
  'neuromag122'
  'neuromag122_planar'
  'neuromag306'
  'neuromag306_planar'
  'itab28'
  'itab153'
  'itab153_planar'
  'yokogawa9'
  'yokogawa64'
  'yokogawa64_planar'
  'yokogawa160'
  'yokogawa160_planar'
  'yokogawa440'
  'yokogawa440_planar'

 It is also possible to specify
  'eeg'
  'electrode'
 although for these an empty set of labels (i.e. {}) will be returned.

 See also FT_SENSTYPE, FT_CHANNELSELECTION
```
