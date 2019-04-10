---
title: ft_multiplotTFR
---
```
 FT_MULTIPLOTTFR plots the time-frequency representations of power or coherence
 in a topographical layout. The plots of the indivual sensors are arranged
 according to their location specified in the layout.

 Use as
   ft_multiplotTFR(cfg, data)

 The data can be a time-frequency representation of power or coherence
 that was computed using the FT_FREQANALYSIS or FT_FREQDESCRIPTIVES
 functions.

 The configuration can have the following parameters:
   cfg.parameter        = field to be represented as color (default depends on data.dimord)
                          'powspctrm' or 'cohspctrm'
   cfg.maskparameter    = field in the data to be used for masking of data, can be logical (e.g. significant data points) or numerical (e.g. t-values).
                        (not possible for mean over multiple channels, or when input contains multiple subjects
                        or trials)
   cfg.maskstyle        = style used to masking, 'opacity', 'saturation', or 'outline' (default = 'opacity')
                        'outline' can only be used with a logical cfg.maskparameter
                        use 'saturation' or 'outline' when saving to vector-format (like *.eps) to avoid all sorts of image-problems
   cfg.maskalpha        = alpha value between 0 (transparent) and 1 (opaque) used for masking areas dictated by cfg.maskparameter (default = 1)
                        (will be ignored in case of numeric cfg.maskparameter or if cfg.maskstyle = 'outline')   
   cfg.masknans         = 'yes' or 'no' (default = 'yes')
   cfg.xlim             = 'maxmin' or [xmin xmax] (default = 'maxmin')
   cfg.ylim             = 'maxmin' or [ymin ymax] (default = 'maxmin')
   cfg.zlim             = plotting limits for color dimension, 'maxmin', 'maxabs', 'zeromax', 'minzero', or [zmin zmax] (default = 'maxmin')
   cfg.gradscale        = number, scaling to apply to the MEG gradiometer channels prior to display
   cfg.magscale         = number, scaling to apply to the MEG magnetometer channels prior to display
   cfg.channel          = Nx1 cell-array with selection of channels (default = 'all'), see FT_CHANNELSELECTION for details
   cfg.refchannel       = name of reference channel for visualising connectivity, can be 'gui'
   cfg.baseline         = 'yes', 'no' or [time1 time2] (default = 'no'), see FT_FREQBASELINE
   cfg.baselinetype     = 'absolute', 'relative', 'relchange', 'normchange', 'db' or 'zscore' (default = 'absolute')
   cfg.trials           = 'all' or a selection given as a 1xN vector (default = 'all')
   cfg.box              = 'yes', 'no' (default = 'no' if maskparameter given default = 'yes')
                          Draw a box around each graph
   cfg.hotkeys          = enables hotkeys (up/down arrows) for dynamic colorbar adjustment
   cfg.colorbar         = 'yes', 'no' (default = 'no')
   cfg.colormap         = any sized colormap, see COLORMAP
   cfg.showlabels       = 'yes', 'no' (default = 'no')
   cfg.showoutline      = 'yes', 'no' (default = 'no')
   cfg.showscale        = 'yes', 'no' (default = 'yes')
   cfg.showcomment      = 'yes', 'no' (default = 'yes')
   cfg.comment          = string of text (default = date + limits)
                          Add 'comment' to graph (according to COMNT in the layout)
   cfg.limittext        = add user-defined text instead of cfg.comment, (default = cfg.comment)
   cfg.fontsize         = font size of comment and labels (if present) (default = 8)
   cfg.fontweight       = font weight of comment and labels (if present)
   cfg.interactive      = Interactive plot 'yes' or 'no' (default = 'yes')
                          In a interactive plot you can select areas and produce a new
                          interactive plot when a selected area is clicked. Multiple areas
                          can be selected by holding down the SHIFT key.
   cfg.renderer         = 'painters', 'zbuffer', ' opengl' or 'none' (default = [])
   cfg.directionality   = '', 'inflow' or 'outflow' specifies for
                          connectivity measures whether the inflow into a
                          node, or the outflow from a node is plotted. The
                          (default) behavior of this option depends on the dimor
                          of the input data (see below).
   cfg.layout           = specify the channel layout for plotting using one of
                         the supported ways (see below).

 For the plotting of directional connectivity data the cfg.directionality
 option determines what is plotted. The default value and the supported
 functionality depend on the dimord of the input data. If the input data
 is of dimord 'chan_chan_XXX', the value of directionality determines
 whether, given the reference channel(s), the columns (inflow), or rows
 (outflow) are selected for plotting. In this situation the default is
 'inflow'. Note that for undirected measures, inflow and outflow should
 give the same output. If the input data is of dimord 'chancmb_XXX', the
 value of directionality determines whether the rows in data.labelcmb are
 selected. With 'inflow' the rows are selected if the refchannel(s) occur in
 the right column, with 'outflow' the rows are selected if the
 refchannel(s) occur in the left column of the labelcmb-field. Default in
 this case is '', which means that all rows are selected in which the
 refchannel(s) occur. This is to robustly support linearly indexed
 undirected connectivity metrics. In the situation where undirected
 connectivity measures are linearly indexed, specifying 'inflow' or
 'outflow' can result in unexpected behavior.

 The layout defines how the channels are arranged and what the size of each
 subplot is. You can specify the layout in a variety of ways:
  - you can provide a pre-computed layout structure (see ft_prepare_layout)
  - you can give the name of an ascii layout file with extension *.lay
  - you can give the name of an electrode file
  - you can give an electrode definition, i.e. "elec" structure
  - you can give a gradiometer definition, i.e. "grad" structure
 If you do not specify any of these and the data structure contains an
 electrode or gradiometer structure (common for MEG data, since the header
 of the MEG datafile contains the gradiometer information), that will be
 used for creating a layout. If you want to have more fine-grained control
 over the layout of the subplots, you should create your own layout file.

 To facilitate data-handling and distributed computing you can use
   cfg.inputfile   =  ...
 If you specify this option the input data will be read from a *.mat
 file on disk. This mat files should contain only a single variable named 'data',
 corresponding to the input structure. For this particular function, the
 data should be provided as a cell-array.

 See also:
   FT_MULTIPLOTER, FT_SINGLEPLOTER, FT_SINGLEPLOTTFR, FT_TOPOPLOTER, FT_TOPOPLOTTFR,
   FT_PREPARE_LAYOUT
```
