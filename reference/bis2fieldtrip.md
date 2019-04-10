---
title: bis2fieldtrip
---
```
 BIS2FIELDTRIP reads BioImage Suite .mgrid files and converts them 
 into a FieldTrip-compatible elec datatype structure and converts electrode
 positions from BioImage Suite mgrid that are in 'xyz' to head coordinates
 of the corresponding MRI volume 

 Use as
   elec = bis2fieldtrip('Subject_grid.mgrid', 'Subject_MR.nii')

 See also FIELDTRIP2BIS, FT_READ_SENS, READ_BIOIMAGE_MGRID
```
