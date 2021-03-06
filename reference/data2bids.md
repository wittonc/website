---
title: data2bids
layout: default
tags: 
---
```
 DATA2BIDS is a helper function to convert MEG, EEG, iEEG or anatomical MRI data to
 the Brain Imaging Data Structure. This function starts from an existing dataset on
 disk and creates the required sidecar files. The overall idea is that you would
 write a MATLAB script in which you call this function multiple times, once for each
 of the data files. For each data file it will write the corresponding JSON file.
 When operating on MEG data files, it will also write a corresponding channels.tsv
 and events.tsv file.

 Use as
   data2bids(cfg)
 or as
   data2bids(cfg, data)

 The first input argument "cfg" is the configuration structure, which contains the
 details for the (meta)data and which specifies the sidecar files you want to write.
 The optional "data" argument corresponds to preprocessed raw data according to
 FT_DATAYPE_RAW or an anatomical MRI according to FT_DATAYPE_VOLUME. The optional
 data argument allows you to write a preprocessed and realigned anatomical MRI to
 disk, or to write a preprocessed electrophysiological dataset to disk.

 The configuration structure should contains
   cfg.dataset                 = string, filename of the input data
   cfg.outputfile              = string, optional filename for the output data, see below
   cfg.keepnative              = string, 'yes' or 'no' (default = 'no')
   cfg.presentationfile        = string, optional filename for the presentation log file, see below
   cfg.mri.deface              = string, 'yes' or 'no' (default = 'no')
   cfg.mri.writesidecar        = string, 'yes', 'replace', 'merge' or 'no' (default = 'yes')
   cfg.mri.dicomfile           = string, filename of a matching DICOM file (default = [])
   cfg.meg.writesidecar        = string, 'yes', 'replace', 'merge' or 'no' (default = 'yes')
   cfg.eeg.writesidecar        = string, 'yes', 'replace', 'merge' or 'no' (default = 'yes')
   cfg.ieeg.writesidecar       = string, 'yes', 'replace', 'merge' or 'no' (default = 'yes')
   cfg.events.writesidecar     = string, 'yes', 'replace', 'merge' or 'no' (default = 'yes')
   cfg.events.trl              = trial definition, see below
   cfg.coordystem.writesidecar = string, 'yes', 'replace', 'merge' or 'no' (default = 'yes')
   cfg.channels.writesidecar   = string, 'yes', 'replace', 'merge' or 'no' (default = 'yes')

 If you specify cfg.dataset without cfg.outputfile, this function will only
 construct and write the appropriate sidecar files matching the header details that
 it will get from the dataset.

 If you also specify cfg.outputfile, this function will furthermore read the data
 from the input dataset and (if cfg.keepnative is no), convert and write
 it to the output file. The output format is NIFTI for anatomical MRIs,
 and BrainVision for EEG and iEEG. Note that in principle you can also
 convert MEG data to BrainVision, but that is not recommended.

 You can specify cfg.presentationfile for a NBS Presentation log file that
 is to be used to construct the events.tsv file for task data.

 You can specify cfg.mri.dicomfile in combination with a NIFTI file. This will
 cause the detailled header information with MR scanner and sequence details to be
 read from the DICOM file and used to fill in the details of the JSON file.

 You can specify cfg.events.trl as a Nx3 matrix with the trial definition (see
 FT_DEFINETRIAL) or as a MATLAB table. When specified as table, the first three
 columns containing integer values corresponding to the begsample, endsample and
 offset, the additional colums can be of another type and can have any name. If you
 do not specify the definition of trials, the events will be read from the dataset.

 You can specify cfg.presentationfile with a NBS presentation log file, which will
 be aligned with the data based on triggers (MEG/EEG/iEEG) or on volumes (fMRI). You
 should also specify
   cfg.trigger.eventtype       = string (default = [])
   cfg.trigger.eventvalue      = string or number
   cfg.presentation.eventtype  = string (default = [])
   cfg.presentation.eventvalue = string or number
   cfg.presentation.skip       = 'last'/'first'/'none'
 to indicate how triggers or volumes match the presentation events.

 General BIDS options that apply to all data types are
   cfg.TaskName                    = string
   cfg.InstitutionName             = string
   cfg.InstitutionAddress          = string
   cfg.InstitutionalDepartmentName = string
   cfg.Manufacturer                = string
   cfg.ManufacturersModelName      = string
   cfg.DeviceSerialNumber          = string
   cfg.SoftwareVersions            = string

 General BIDS options that apply to all functional data types are
   cfg.TaskDescription             = string
   cfg.Instructions                = string
   cfg.CogAtlasID                  = string
   cfg.CogPOID                     = string

 There are many more BIDS options for the JSON files for specific datatypes. Rather
 than listing them here in the help, please open this function in the MATLAB editor
 to see what those are.

 Example with a CTF dataset on disk that needs no conversion
   cfg = [];
   cfg.dataset                     = 'sub-01_ses-meg_task-language_meg.ds';
   cfg.TaskName                    = 'language';
   cfg.meg.PowerLineFrequency      = 50;
   cfg.InstitutionName             = 'Radboud University';
   cfg.InstitutionalDepartmentName = 'Donders Institute for Brain, Cognition and Behaviour';
   data2bids(cfg)

 Example with an anatomical MRI on disk that needs no conversion
   cfg = [];
   cfg.dataset                     = 'sub-01_ses-mri_T1w.nii';
   cfg.mri.dicomfile               = '00080_1.3.12.2.1107.5.2.43.66068.2017082413175824865636649.IMA'
   cfg.mri.MagneticFieldStrength   = 3; % this is usually not needed, as it will be obtained from the DICOM file
   cfg.InstitutionName             = 'Radboud University';
   cfg.InstitutionalDepartmentName = 'Donders Institute for Brain, Cognition and Behaviour';
   data2bids(cfg)

 Example with a NeuroScan EEG dataset on disk that needs to be converted
   cfg = [];
   cfg.dataset                     = 'subject01.cnt';
   cfg.outputfile                  = 'sub-001_task-visual_eeg.vhdr';
   cfg.InstitutionName             = 'Radboud University';
   cfg.InstitutionalDepartmentName = 'Donders Institute for Brain, Cognition and Behaviour';
   data2bids(cfg)

 Example with preprocessed EEG data in memory
   cfg = [];
   cfg.dataset                     = 'subject01.cnt';
   cfg.bpfilter                    = 'yes';
   cfg.bpfreq                      = [0.1 40];
   data = ft_preprocessing(cfg);
   cfg = [];
   cfg.outputfile                  = 'sub-001_task-visual_eeg.vhdr';
   cfg.InstitutionName             = 'Radboud University';
   cfg.InstitutionalDepartmentName = 'Donders Institute for Brain, Cognition and Behaviour';
   data2bids(cfg, data)

 Example with realigned and resliced anatomical MRI data in memory
   cfg = [];
   cfg.outputfile                  = 'sub-01_ses-mri_T1w.nii';
   cfg.mri.MagneticFieldStrength   = 3;
   cfg.InstitutionName             = 'Radboud University';
   cfg.InstitutionalDepartmentName = 'Donders Institute for Brain, Cognition and Behaviour';
   data2bids(cfg, mri)

 This function corresponds to version 1.1.1 of the BIDS specification.
 See http://bids.neuroimaging.io/ for further details.
```
