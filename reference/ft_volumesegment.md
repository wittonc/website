---
title: ft_volumesegment
---
```
 FT_VOLUMESEGMENT segments an anatomical MRI. The behavior depends on the output requested. It can
 return probabilistic tissue maps of gray/white/csf compartments, a skull-stripped anatomy, or
 binary masks representing the brain surface, skull, or scalp surface.

 Use as
   segmented = ft_volumesegment(cfg, mri)
 where the input mri should be a single anatomical volume that was for example read with
 FT_READ_MRI. For the purpose of creating binary masks of the brain or of the skull, you can also
 provide either the anatomical volume or the already segmented volume (with the probabilistic
 tissue maps) as input.

 The configuration structure can contain
   cfg.output         = string or cell-array of strings, see below (default = 'tpm')
   cfg.spmversion     = string, 'spm2', 'spm8', 'spm12' (default = 'spm12')
   cfg.spmmethod      = string, 'old', 'new', 'mars' (default = 'old'). This pertains 
                        to the algorithm used when cfg.spmversion='spm12', see below.
   cfg.opts           = struct, containing spm-version specific options. See
                        the code and/or the SPM-documentation for more detail.
   cfg.template       = filename of the template anatomical MRI (default = '/spm2/templates/T1.mnc'
                        or '/spm8/templates/T1.nii')
   cfg.tpm            = cell-array containing the filenames of the tissue probability maps
   cfg.name           = string for output filename
   cfg.write          = 'no' or 'yes' (default = 'no'),
                        writes the probabilistic tissue maps to SPM compatible analyze (spm2),
                        or nifti (spm8/spm12) files,
                        with the suffix (spm2)
                         _seg1, for the gray matter segmentation
                         _seg2, for the white matter segmentation
                         _seg3, for the csf segmentation
                        or with the prefix (spm8, and spm12 with spmmethod='old')
                         c1, for the gray matter segmentation
                         c2, for the white matter segmentation
                         c3, for the csf segmentation
                        when using spm12 with spmmethod='new' there'll be 3 additional tissue types
                         c4, for the bone segmentation
                         c5, for the soft tissue segmentation
                         c6, for the air segmentation
                        when using spm12 with spmmethod='mars' the tpms will be
                         postprocessed with the mars toolbox, yielding smoother%                         segmentations in general.
   cfg.brainsmooth    = 'no', or scalar, the FWHM of the gaussian kernel in voxels, (default = 5)
   cfg.scalpsmooth    = 'no', or scalar, the FWHM of the gaussian kernel in voxels, (default = 5)
   cfg.skullsmooth    = 'no', or scalar, the FWHM of the gaussian kernel in voxels, (default = 5)
                        this parameter is only used when the segmentation
                        contains 6 tisuse types, including 'bone'
   cfg.brainthreshold = 'no', or scalar, relative threshold value which is used to threshold the
                       tpm in order to create a volumetric brainmask (see below), (default = 0.5)
   cfg.scalpthreshold = 'no', or scalar, relative threshold value which is used to threshold the
                        anatomical data in order to create a volumetric scalpmask (see below),
                        (default = 0.1)
   cfg.skullthreshold = 'no', or scalar, relative threshold value which is used to threshold the
                        anatomical data in order to create a volumetric scalpmask (see below),
                        (default = 0.5). this parameter is only used when
                        the segmetnation contains 6 tissue types,
                        including 'bone',
   cfg.downsample     = integer, amount of downsampling before segmentation
                       (default = 1; i.e., no downsampling)

 The desired segmentation output is specified with cfg.output as a string or cell-array of strings
 and can contain
   'tpm'         - tissue probability map for csf, white and gray matter
   'brain'       - binary representation of the brain (including csf, white and gray matter)
   'skull'       - binary representation of the skull
   'scalp'       - binary representation of the scalp
   'skullstrip'  - anatomy with only the brain


 Example use:
   cfg        = [];
   segmented  = ft_volumesegment(cfg, mri) will segmented the anatomy and will output the
                segmentation result as 3 probabilistic masks in segmented.gray, white and csf.

   cfg.output = 'skullstrip';
   segmented  = ft_volumesegment(cfg, mri) will generate a skull-stripped anatomy based on a
                brainmask generated from the probabilistic tissue maps. The skull-stripped anatomy
                is stored in the field segmented.anatomy.

   cfg.output = {'brain' 'scalp' 'skull'};
   segmented  = ft_volumesegment(cfg, mri) will produce a volume with 3 binary masks, representing
                the brain surface, scalp surface, and skull which do not overlap.

   cfg.output = {'scalp'};
   segmented  = ft_volumesegment(cfg, mri) will produce a volume with a binary mask (based on the
                anatomy), representing the border of the scalp surface (i.e., everything inside the
                surface is also included). Such representation of the scalp is produced faster,
                because it doesn't require to create the tissue probabilty maps before creating
                the mask.

 It is not possible to request tissue-probability map (tpm)  in combination with binary masks
 (brain, scalp or skull) or skull-stripped anatomy. The output will return only the probabilistic
 maps in segmented.gray, white and csf. However, when a segmentation with the probabilistic gray, white
 and csf representations is available, it is possible to use it as input for brain or skull binary mask.
 For example:
   cfg           = [];
   cfg.output    = {'tpm'};
   segment_tpm   = ft_volumesegment(cfg, mri);
   cfg.output    = {'brain'};
   segment_brain = ft_volumesegment(cfg, segment_tpm);

 For the SPM-based segmentation to work, the coordinate frame of the input MRI needs to be
 approximately coregistered to the templates of the probabilistic tissue maps. The templates are
 defined in SPM/MNI-space. FieldTrip attempts to do an automatic alignment based on the
 coordsys-field in the mri, and if this is not present, based on the coordsys-field in the cfg. If
 none of them is specified the FT_DETERMINE_COORDSYS function is used to interactively assess the
 coordinate system in which the MRI is expressed.

 The template mri is defined in SPM/MNI-coordinates:
   x-axis pointing to the right ear
   y-axis along the acpc-line
   z-axis pointing to the top of the head
   origin in the anterior commissure.
 Note that the segmentation only works if the template MRI is in SPM coordinates.

 If the input mri is a string pointing to a CTF *.mri file, the x-axis is assumed to point to the
 nose, and the origin is assumed to be on the interauricular line. In this specific case, when
 ft_read_mri is used to read in the mri, the coordsys field is automatically attached.

 To facilitate data-handling and distributed computing you can use
   cfg.inputfile   =  ...
   cfg.outputfile  =  ...
 If you specify one of these (or both) the input data will be read from a *.mat file on disk and/or
 the output data will be written to a *.mat file. These mat files should contain only a single
 variable, corresponding with the input/output structure.

 See also FT_READ_MRI, FT_DETERMINE_COORDSYS, FT_PREPARE_HEADMODEL
```
