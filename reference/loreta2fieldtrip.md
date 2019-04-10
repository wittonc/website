---
title: loreta2fieldtrip
---
```
 LORETA2FIELDTRIP reads and converts a LORETA source reconstruction into a
 FieldTrip data structure, which subsequently can be used for statistical
 analysis or other analysis methods implemented in Fieldtrip.

 Use as
   [source]  =  loreta2fieldtrip(filename, ...)
 where optional arguments can be passed as key-value pairs.

 filename can be the binary file from LORETA or a LORETA file exported as
 a text file (using the format converter in LORETA-KEY).

 The following optional arguments are supported
   'timeframe'  =  integer number, which timepoint to read (default is to read all)

 See also EEGLAB2FIELDTRIP, SPM2FIELDTRIP, NUTMEG2FIELDTRIP, SPASS2FIELDTRIP
```
