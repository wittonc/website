---
title: besa2fieldtrip
---
```
 BESA2FIELDTRIP reads and converts various BESA datafiles into a FieldTrip
 data structure, which subsequently can be used for statistical analysis
 or other analysis methods implemented in Fieldtrip.

 Use as
   [data] = besa2fieldtrip(filename)
 where the filename should point to a BESA datafile (or data that
 was exported by BESA). The output is a MATLAB structure that is
 compatible with FieldTrip.

 The format of the output structure depends on the type of datafile:
   *.avr is converted to a structure similar to the output of FT_TIMELOCKANALYSIS
   *.mul is converted to a structure similar to the output of FT_TIMELOCKANALYSIS
   *.swf is converted to a structure similar to the output of FT_TIMELOCKANALYSIS (*)
   *.tfc is converted to a structure similar to the output of FT_FREQANALYSIS     (*)
   *.dat is converted to a structure similar to the output of FT_SOURCANALYSIS
   *.dat combined with a *.gen or *.generic is converted to a structure similar to the output of FT_PREPROCESSING

 (*) If the BESA toolbox by Karsten Hochstatter is found on your
 MATLAB path, the readBESAxxx functions will be used (where xxx=tfc/swf),
 alternatively the private functions from FieldTrip will be used.

 See also EEGLAB2FIELDTRIP, SPM2FIELDTRIP
```
