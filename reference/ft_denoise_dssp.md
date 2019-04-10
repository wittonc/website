---
title: ft_denoise_dssp
---
```
 FT_DENOISE_DSSP implements a dual signal subspace projection algorithm
 to suppress interference outside a predefined source region of
 interest. It is based on: Sekihara et al. J. Neural Eng. 2016 13(3), and
 Sekihara et al. J. Neural Eng. 2018 15(3).

 Use as
   dataout = ft_denoise_dssp(cfg, datain)
 where cfg is a configuration structure that contains
   cfg.channel          = Nx1 cell-array with selection of channels (default = 'all'), see FT_CHANNELSELECTION for details
   cfg.trials           = 'all' or a selection given as a 1xN vector (default = 'all')
   cfg.sourcemodel      = structure, source model with precomputed leadfields, see FT_PREPARE_LEADFIELD
   cfg.dssp             = structure with parameters that determine the behavior of the algorithm
   cfg.dssp.n_space     = 'all', or scalar. Number of dimensions for the
                          initial spatial projection.
   cfg.dssp.n_in        = 'all', or scalar. Number of dimensions of the
                          subspace describing the field inside the ROI.
   cfg.dssp.n_out       = 'all', or scalar. Number of dimensions of the
                          subspace describing the field outside the ROI.
   cfg.dssp.n_intersect = scalar (default = 0.9). Number of dimensions (if
                          value is an integer>=1), or threshold for the
                          included eigenvalues (if value<1), determining
                          the dimensionality of the intersection.

 See also FT_DENOISE_PCA, FT_DENOISE_SYNTHETIC, FT_DENOISE_TSR
```
