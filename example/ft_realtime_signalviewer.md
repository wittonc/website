---
title: Example real-time signal viewer
tags: [example, realtime]
---

# Example real-time signal viewer

The simplest example for continuous data without any events or triggers is a simple data viewer that lets the data scroll by in a figure, while the data streams from the acquisition system. This example is implemented in the **[ft_realtime_signalviewer](/reference/ft_realtime_signalviewer)** function. You can of course take this function as starting point for your BCI system and modify it to your own needs.

## Flowchart

{% include image src="/assets/img/example/ft_realtime_signalviewer/realtime_signalviewer.png" width="300" %}

## Example use

The easiest way to try out the **[ft_realtime_signalviewer](/reference/ft_realtime_signalviewer)** example is by starting two MATLAB sessions. In the first session you create some random signal and write it to the buffe

    cfg                = [];
    cfg.channel        = 1:10;                         % list with channel "names"
    cfg.blocksize      = 1;                            % seconds
    cfg.fsample        = 250;                          % sampling frequency
    cfg.target.dataset = 'buffer://localhost:1972';    % where to write the data
    ft_realtime_signalproxy(cfg)

In the second MATLAB session you start the **[ft_realtime_signalviewer](/reference/ft_realtime_signalviewer)** and point it to the buffe

    cfg                = [];
    cfg.blocksize      = 1;                            % seconds
    cfg.dataset        = 'buffer://localhost:1972';    % where to read the data
    ft_realtime_signalviewer(cfg)

After starting the **[ft_realtime_signalviewer](/reference/ft_realtime_signalviewer)**, you should see a figure that updates itself every second. That figure contains the raw signal. You can also start the two MATLAB sessions on two different computers, where on the second you would then point the reading function to the first computer.

## MATLAB code

    function ft_realtime_signalviewer(cfg)

    % FT_REALTIME_SIGNALVIEWER is an example realtime application for online
    % viewing of the data. It should work both for EEG and MEG.
    %
    % Use as
    %   ft_realtime_signalviewer(cfg)
    % with the following configuration options
    %   cfg.blocksize  = number, size of the blocks/chuncks that are processed (default = 1 second)
    %   cfg.channel    = cell-array, see FT_CHANNELSELECTION (default = 'all')
    %   cfg.bufferdata = whether to start on the 'first or 'last' data that is available (default = 'last')
    %   cfg.readevent  = whether or not to copy events (default = 'no')
    %   cfg.demean     = 'no' or 'yes', whether to apply baseline correction (default = 'yes')
    %
    % The source of the data is configured as
    %   cfg.dataset       = string
    % or alternatively to obtain more low-level control as
    %   cfg.datafile      = string
    %   cfg.headerfile    = string
    %   cfg.eventfile     = string
    %   cfg.dataformat    = string, default is determined automatic
    %   cfg.headerformat  = string, default is determined automatic
    %   cfg.eventformat   = string, default is determined automatic
    %
    % Some notes about skipping data and catching up with the data strea
    %
    % cfg.jumptoeof='yes' causes the realtime function to jump to the end
    % when the function _starts_. It causes all data acquired prior to
    % starting the RT function to be skipped.
    %
    % cfg.bufferdata=last causes the realtime function to jump to the last
    % available data while _running_. If the RT loop is not fast enough,
    % it causes some data to be dropped.
    %
    % If you want to skip all data that was acquired before you start the
    % RT function, but don't want to miss any data that was acquired while
    % the realtime function is started, then you should use jumptoeof=yes and
    % bufferdata=first. If you want to analyze data from a file, then you
    % should use jumptoeof=no and bufferdata=first.
    %
    % To stop the realtime function, you have to press Ctrl-C

    % Copyright (C) 2008, Robert Oostenveld
    %
    % Subversion does not use the Log keyword, use 'svn log `<filename>` or 'svn -v log | less' to get detailled information

    % set the default configuration options
    if ~isfield(cfg, 'dataformat'),     cfg.dataformat = [];      end % default is detected automatically
    if ~isfield(cfg, 'headerformat'),   cfg.headerformat = [];    end % default is detected automatically
    if ~isfield(cfg, 'eventformat'),    cfg.eventformat = [];     end % default is detected automatically
    if ~isfield(cfg, 'blocksize'),      cfg.blocksize = 1;        end % in seconds
    if ~isfield(cfg, 'overlap'),        cfg.overlap = 0;          end % in seconds
    if ~isfield(cfg, 'channel'),        cfg.channel = 'all';      end
    if ~isfield(cfg, 'bufferdata'),     cfg.bufferdata = 'last';  end % first or last
    if ~isfield(cfg, 'readevent'),      cfg.readevent = 'no';     end % capture events?
    if ~isfield(cfg, 'jumptoeof'),      cfg.jumptoeof = 'no';     end % jump to end of file at initialization
    if ~isfield(cfg, 'demean'),         cfg.demean = 'yes';       end % baseline correction

    if ~isfield(cfg, 'dataset') && ~isfield(cfg, 'header') && ~isfield(cfg, 'datafile')
      cfg.dataset = 'buffer://localhost:1972';
    end

    % translate dataset into datafile+headerfile
    cfg = ft_checkconfig(cfg, 'dataset2files', 'yes');
    cfg = ft_checkconfig(cfg, 'required', {'datafile' 'headerfile'});

    % ensure that the persistent variables related to caching are cleared
    clear read_header
    % start by reading the header from the realtime buffer
    hdr = ft_read_header(cfg.headerfile, 'headerformat', cfg.headerformat, 'cache', true, 'retry', true);

    % define a subset of channels for reading
    cfg.channel = channelselection(cfg.channel, hdr.label);
    chanindx    = match_str(hdr.label, cfg.channel);
    nchan       = length(chanindx);
    if nchan==0
      error('no channels were selected');
    end

    % determine the size of blocks to process
    blocksize = round(cfg.blocksize * hdr.Fs);
    overlap   = round(cfg.overlap*hdr.Fs);

    if strcmp(cfg.jumptoeof, 'yes')
      prevSample = hdr.nSamples * hdr.nTrials;
    else
      prevSample  = 0;
    end
    count       = 0;

    %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
    % this is the general BCI loop where realtime incoming data is handled
    %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
    while true

      % determine number of samples available in buffer
      hdr = read_header(cfg.headerfile, 'headerformat', cfg.headerformat, 'cache', true);

      % see whether new samples are available
      newsamples = (hdr.nSamples*hdr.nTrials-prevSample);

      if newsamples>=blocksize

        % determine the samples to process
        if strcmp(cfg.bufferdata, 'last')
          begsample  = hdr.nSamples*hdr.nTrials - blocksize + 1;
          endsample  = hdr.nSamples*hdr.nTrials;
        elseif strcmp(cfg.bufferdata, 'first')
          begsample  = prevSample+1;
          endsample  = prevSample+blocksize ;
        else
          error('unsupported value for cfg.bufferdata');
        end

        % this allows overlapping data segments
        if overlap && (begsample>overlap)
          begsample = begsample - overlap;
          endsample = endsample - overlap;
        end

        % remember up to where the data was read
        prevSample  = endsample;
        count       = count + 1;
        fprintf('processing segment %d from sample %d to %d\n', count, begsample, endsample);

        % read data segment from buffer
        dat = read_data(cfg.datafile, 'header', hdr, 'dataformat', cfg.dataformat, 'begsample', begsample, 'endsample', endsample, 'chanindx', chanindx, 'checkboundary', false);

        % it only makes sense to read those events associated with the currently processed data
        if strcmp(cfg.readevent, 'yes')
          evt = ft_read_event(cfg.eventfile, 'header', hdr, 'minsample', begsample, 'maxsample', endsample);
        end

        %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
        % from here onward it is specific to the display of the data
        %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

        % put the data in a fieldtrip-like raw structure
        data.trial{1} = dat;
        data.time{1}  = offset2time(begsample, hdr.Fs, endsample-begsample+1);
        data.label    = hdr.label(chanindx);
        data.hdr      = hdr;
        data.fsample  = hdr.Fs;

        % apply some preprocessing options
        if strcmp(cfg.demean, 'yes')
          data.trial{1} = preproc_baselinecorrect(data.trial{1});
        end

        % plot the data just like a standard FieldTrip raw data strucute
        plot(data.time{1}, data.trial{1});
        xlim([data.time{1}(1) data.time{1}(end)]);

        if strcmp(cfg.readevent, 'yes')
          for i=1:length(evt)
            % draw a line and some text to indicate the event
            time = offset2time(evt(i).sample, hdr.Fs, 1);
            if isstr(evt(i).type) && isempty(evt(i).type)
              description = sprintf('%s', evt(i).type);
            elseif isstr(evt(i).type) && isstr(evt(i).type)
              description = sprintf('%s %s', evt(i).type, evt(i).value);
            elseif isstr(evt(i).type) && isnumeric(evt(i).type)
              description = sprintf('%s %s', evt(i).type, num2str(evt(i).value));
            else
              description = 'event';
            end

            h = line([time time], ylim);
            set(h, 'LineWidth', 2, 'LineStyle', ':', 'Color', 'k');
            y = ylim; y = y(1);
            h = text(time, y, description, 'VerticalAlignment', 'bottom');
          end
        end

        % force MATLAB to update the figure
        drawnow

      end % if enough new samples
    end % while true
