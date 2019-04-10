---
title: ft_standalone
---
```
 FT_STANDALONE is the entry function of the compiled FieldTrip application.
 The compiled application can be used to execute FieldTrip data analysis
 scripts.

 This function can be started on the interactive MATLAB command line as
   ft_standalone script.m
   ft_standalone script1.m script2.m ...
   ft_standalone jobfile.mat
 or after compilation on the Linux/macOS command line as
   fieldtrip.sh <MATLABROOT> script.m
   fieldtrip.sh <MATLABROOT> script1.m script2.m ...
   fieldtrip.sh <MATLABROOT> jobfile.mat

 It is possible to pass additional options on the MATLAB command line like
 this on the MATLAB command line
   ft_standalone --option value scriptname.m
 or on the Linux/macOS command line
   fieldtrip.sh <MATLABROOT> --option value scriptname.m
 The options and their values are automaticallly made available as local
 variables in the script execution environment.

 See also FT_COMPILE_STANDALONE
```
