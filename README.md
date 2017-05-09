# MiLES v0.3
## Mid-Latitude Evaluation System

May 2017

by P. Davini - ISAC-CNR
p.davini@isac.cnr.it

Contributors: J. von Hardenberg - ISAC-CNR

------------------------------

## WHAT IS MiLES?

**MiLES** is a tool for estimating properties of mid-latitude climate originally thought
for EC-Earth output and then extended to any model data. It is based uniquely on R and CDO.
It works on daily 500hPa geopotential height data and produces climatological figures 
for the chosen time period in 3 different output format. 
Data are interpolated on a common 2.5x2.5 grid using CDO.  
Model data are compated against ECMWF ERA-INTERIM reanalysis for a standard period (1979-2014).
It supports analysis for the 4 standard seasons.

Current version includes:
1. 	**2D Atmospheric blocking**: based on *Davini et al. (2012)*
	It is a 2D version of *Tibaldi and Molteni (1990)* for Northern Hemisphere
	atmospheric blocking evaluating meridional gradient reversal at 500hPa.
	It includes also Meridional Gradient Index and Blocking Intensity index
	and Rossby wave orientation index, computing both Instantenous Blocking and Blocking Events.
	Full timeseries and climatologies are provided in NetCDF4 Zip format.

2. 	**Z500 Empirical Orthogonal Functions**. Based on CDO "eofs" function.
	First 4 EOFs for North Atlantic (over the 90W-40E 20N-85N box) and Northern Hemisphere (20N-85N).
	NAO, EA, and Arctic Oscillation are thus computed. 
	Figures of linear regression are provided.
	PCs and eigenvectors, as well as the variances explained are provided in NetCDF format.

----------------

## MAIN NOTES

Please be aware that this is free tool in continous development, then it may not be 
free of bugs. Please report any issue at p.davini@isac.cnr.it

Please refer to **MiLES** specifing which version has been used in the acknowledgment of any publication.

Please cite *"Davini, P., C. Cagnazzo, S. Gualdi, and A. Navarra, 2012:
Bidimensional Diagnostics, Variability, and Trends of Northern Hemisphere Blocking.
J. Climate, 25, 6496–6509, doi: 10.1175/JCLI-D-12-00032.1."*
in case you  use the blocking index in any publication.


----------------

## SOFTWARE REQUIREMENTS

* a. R version >3.0
* b. CDO version > 1.6.5, compiled with netCDF4
* c. Compiling environment (gcc)

IMPORTANT: there are 2 R packages (maps and ncdf4) needed to run **MiLES**.
You have to run "Rscript config/installpack.R" as first step in order to install the packages.
If everything runs fine, their installation is performed by an automated 
routine that brings the user through the standard web-based installation. 
Packages are also included in **MiLES** and can be installed offline.

The installation of some packages requires specifically gfortran-4.8: there is an issue known on 
Mac OS X (10.11 and later at least) which requires a few turnarounds. See here for help:
http://stackoverflow.com/questions/23916219/os-x-package-installation-depends-on-gfortran-4-8

-----------------

## HOW TO

Before running **MiLES** R packages should installed (see above).
Also, config_$MACHINE.sh should be set accordingly to your local configuration.
It is a trivial configuration, needing only information on CDO/R paths and some folders definition.

**MiLES** is simply run executing in bash environment the "wrapper_miles.sh". 
Options as seasons and file format can be specified at this stage.

**MiLES** is based on a pre-processing of data, performed by "z500_prepare.sh".
This script expects daily 500hPa geopotential height data in a single folder: it interpolates data on a 2.5x2.5 grid,
it selects the NH only and it organizes their structure and their features in order to make them handable by MiLES.
You can use both geopotential or geopotential height data, the former will be automatically converted. 

After that, blocking analysis is performed by two different R script ("blocking_fast.R" and "blocking_figures.R")

EOFs are produced with CDO via the "eof_fast.sh" script and plots are produced by the "eof_figure.R" script

Figures are extremely basic: they can be produced in pdf, png and eps format.

------------

## HISTORY

*v0.3 - May 2017*
- Blocking Events definition by Davini et al. (2012) now avaiable
- Removed dependencies from fields and spam R packages
- Support for figures format in png, pdf or eps - by J. von Hardenberg
- Removed dependencies on R-files saving blocking data (using now NetCDF)
- Blocking timeseries available in NetCDF
- NetCDF4 Zip for blocking output files
- Support for different model calendar: 30-day, Gregorian and No-Leap-Year
- ~36x faster linear regression for EOFs (.fit.lm function)
- Improved speed in blocking for long timeseries: ~2.5x faster for 30years (predeclaration of arrays)
- Minor bugs in axis legends (removal of image.plot)
- Readme in markdown format


*v0.2 - Apr 2017*
- Support for Arctic Oscillation
- External unique configuration file
- Psuedo-universal adaptability to any model data
- Automated script for R package installing
- Adaptation to geopotential/geopotential height data
- Climatological blocking data are stored in NetCDF
- Now on GitHUB

*v0.11 - Mar 2015*

- Update to fast blocking (Blocking2-scheme) computation.

*v0.1 - Oct 2014*

- EOFs and 2D Blocking calculation
- Basic functions implemented
- Support for NetCDF4
- Support for 4 standard season (DJF,MAM,JJA,SON)
- ERAINTERIM comparison via netCDF files
- Parallelization Z500 extraction
- Png outputs from PDF

-----------------
