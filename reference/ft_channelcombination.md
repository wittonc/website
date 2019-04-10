---
title: ft_channelcombination
---
```
 FT_CHANNELCOMBINATION creates a cell-array with combinations of EEG/MEG
 channels for subsequent cross-spectral-density and coherence analysis

 You should specify channel combinations as a two-column cell-array,
   cfg.channelcmb = {  'EMG' 'MLF31'
                       'EMG' 'MLF32'
                       'EMG' 'MLF33' };
 to compare EMG with these three sensors, or
   cfg.channelcmb = { 'MEG' 'MEG' };
 to make all MEG combinations, or
   cfg.channelcmb = { 'EMG' 'MEG' };
 to make all combinations between the EMG and all MEG channels.

 For each column, you can specify a mixture of real channel labels
 and of special strings that will be replaced by the corresponding
 channel labels. Channels that are not present in the raw datafile
 are automatically removed from the channel list.

 When directional connectivity measures will subsequently be computed, the
 interpretation of each channel-combination is that the direction of the
 interaction is from the first column to the second column.

 Note that the default behavior is to exclude symmetric pairs and
 auto-combinations.

 See also FT_CHANNELSELECTION
```
