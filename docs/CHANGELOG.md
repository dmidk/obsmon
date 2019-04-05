# Change Log
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/)
and this project adheres to [Semantic Versioning](http://semver.org/).

## [3.1.0] 2019-04-05
### Added
- Batch mode
### Fixed
- Issue that would cause cache to end up in incorrect files in some occasions
- Issue that would prevent caching from being triggered in some occasions


## [3.0.0] 2019-03-14
### Added
- User-configured "multiPlots"
    - Produce one or more pre-configured plots at once
    - Similar idea as the earlier "pre-defined plots"
        - But configurable by user via config.toml file
- Interactive plots (ability to zoom/pan/hover, etc)
- Vertical profile plots
- Option to export data tables as txt/csv files
- "Cancel plot" button (appears only after clicking in "Plot")
- Better documentation in PDF format (and accessible from the GUI)
- New config options supported (to be set under the "general" section)
    - initCheckDataExists (true/false, default: false)
      - Assert, at initialisation time, whether or not all data files for all
        experiments exist
    - showCacheOptions (true/false, default: false): to show/hide advanced
      cache-related options
        - Options can also be shown by creating a file named ".obsmon_show_cache_options"
          in the obsmon directory
    - maxExtraParallelProcs: control max number of parallel tasks
        - Can also be set via env var OBSMON_MAX_N_EXTRA_PROCESSES

### Fixed
- Show timezone in dates at the end of plot titles instead of "Z"
- Station labels in maps are now consistent with the ones shown in the UI

### Changed
- Experiment path specification via "path" keyword in config file
    - Old "baseDir" and "experiment" now deprecated and will be ignored
        - Warning issued in this case
- Obsmon can now work even if observations are not cached
    - Auto-discovery cache is now performed only for selected date(s) and cycle(s)
        - Caching starts automatically when a new DTG, experiment or database is selected
        - While cache is not finished, the fields in the GUI are populated with all
          possible values they may have
        - The GUI is refreshed once cache finishes as to only show choices available
          according to the relevant data files
- Some UI redesign
- Show a spinner instead of a progress bar when an output is being prepared
- Allow selection of multiple stations in some plots

### Removed
- Progress bars from standard output


## [2.3.0] 2018-10-26
### Added
- Option to select only standard levels/channels
    - The standard levels are considered to be those read from the
      "obsmon" table in the sql data files.
    - Selecting "standard" is equivalent to selecting "all" in v<=2.2.0.
      See "Fixed missing level values" under [Fixed](#Fixed)
- Git repo info printed in the standard output. This is to make it
  easier to provide users with support.

### Fixed
- Missing levels
    - In some occasions, available data would become impossible to select
      because information about non-standard level values would not be
      added to the cache. This is now fixed.
- Experiment selection is kept when updating caching information in the GUI


## [2.2.0] 2018-09-17
### Added
- "AverageMaps" plot category
    - Average First Guess Departure Map
    - Average Analysis Departure Map
    - Average Analysis Increment Map
- Possibility to start obsmon from any directory (obsmon must be in the PATH)
- Support to command line options in (both in the install script as well as in
  obsmon itself)
- Possibility to install R-packages used by obsmon locally (as part of obsmon
  itself), making it independent of R libraries installed in the system. This
  is useful for packaging.
- Support to offline installation
- Support to using pre-compiled R libraries
- Progress of caching process shown in the GUI

### Changed
- Auto-discovery cache is now sqlite-based (Fixes: #148)
- Auto-discovery cache is also done asynchronously now. This means that, if
  multiple experiments are being dealt with, the auto-discovery caching for
  all of them can be performed simultaneously. Any experiment can now be
  selected as soon as it is ready, without the need to wait for the others
  to finish caching.
- Info about installtion moved to INSTALL.md file
- Automatic identification of imported R libraries during install
    - R dependencies recursively determined prior to installation
- obsmon and install executables are now R scripts (used to be bash)

### Fixed
- Bias correction and First Guess Departure+Bias Correction maps are back
- Look for an alternative TCP port if cannot use the one initially chosen
- Some issues dealing with unavailable data


## [2.1.0] - 2017-10-20
### Added
- Date selection for single times
- Cycle selection for date ranges
- Plottype filtering offers only plots valid for selected criteria
- Auto-discovery of obtypes and stations (cached)
- Progress bar for long operations
- Plot registry facilitates adding new plots/plot maintenance

### Changed
- UI retains user choices
- Streamlined UI
- Window resizing supported
- Surface diagnostics moved to more general station diagnostics plottype
- Plottypes split in categories
- Data table interface improved
- Color handling improved
- Cairo based plotting improves plot quality
- TOML based config.toml replaces hardcoded and environment configuration
- Only install missing packages in install.R
- Logging via futile.logger replaces print statements
- Database handling now via object oriented interface
- Plotting via object oriented interface

### Removed
- Pre-defined plots
- Dump database
- Settings tab
- Environment variables for configuration


[3.1.0]: https://git.smhi.se/foum/obsmon/compare/obsmon-3.0.0...obsmon-3.1.0
[3.0.0]: https://git.smhi.se/foum/obsmon/compare/obsmon-2.3.0...obsmon-3.0.0
[2.3.0]: https://git.smhi.se/foum/obsmon/compare/obsmon-2.2.0...obsmon-2.3.0
[2.2.0]: https://git.smhi.se/foum/obsmon/compare/obsmon-2.1.0...obsmon-2.2.0
[2.1.0]: https://git.smhi.se/a002160/obsmon/compare/obsmon-2.0.0...obsmon-2.1.0