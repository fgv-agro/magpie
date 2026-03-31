# MagPIE-Brazil - Regionalized framework for modeling land-use systems in Brazil

Based on the original MAgPIE model developed by the Potsdam Institute for Climate Impact Research (PIK).

## WHAT IS MAGPIE-BRAZIL?
MagPIE-Brazil is a regionalized version of the MAgPIE (Model of Agricultural Production and its Impact on the Environment) framework, adapted to represent land-use dynamics, agricultural systems, and environmental processes in Brazil.

It builds upon the original MAgPIE model developed by the Potsdam Institute for Climate Impact Research (PIK), maintaining its core structure while introducing modifications to better capture Brazilian geographic, biophysical, and economic conditions.

Like the original framework, MagPIE-Brazil combines economic optimization (e.g., demand for agricultural commodities, production costs, and trade) with biophysical constraints (e.g., crop yields, land availability, and water constraints). The model derives land-use patterns and production outcomes under different scenarios, with a focus on applications relevant to Brazil.

This repository is not the official MAgPIE repository.
Original project: https://github.com/magpiemodel/magpie

## DOCUMENTATION
A framework description paper has been published in
Geoscientific Model Development (GMD): https://doi.org/10.5194/gmd-12-1299-2019

The model documentation for version 4.13.0 can be found at
https://rse.pik-potsdam.de/doc/magpie/4.13.0/

A most recent version of the documentation can also be extracted from the
model source code via the R package goxygen
(https://github.com/pik-piam/goxygen). To extract the documentation, install the
package and run the main function (goxygen) in the main folder of the model.
The resulting documentation can be found in the folder "doc".

Please find a set of tutorials here https://magpiemodel.github.io/tutorials.
This guide will give you a brief technical introduction in how to install, run and use the model
and how to analyse the model output.

Please pay attention to the MAgPIE Coding Etiquette when you modify the code.
The Coding Etiquette you find at the beginning of the documentation mentioned above.
The Coding Etiquette explains also the naming conventions and other
structural characteristics.

## COPYRIGHT
Copyright 2008-2025 Potsdam Institute for Climate Impact Research (PIK)

Modifications and extensions for MagPIE-Brazil: FGV-Agro.

## LICENSE
This program is free software: you can redistribute it and/or modify
it under the terms of the **GNU Affero General Public License** as published by
the Free Software Foundation, **version 3** of the License or later. You should
have received a copy of the GNU Affero General Public License along with this
program. See the LICENSE file in the root directory. If not, see
https://www.gnu.org/licenses/agpl.txt

Under Section 7 of AGPL-3.0, you are granted additional permissions described
in the MAgPIE License Exception, version 1.0 (see LICENSE file).

## NOTES
Following the principles of good scientific practice it is recommended
to make the source code available in the events of model based publications
or model-based consulting.

This repository represents a modified version of MAgPIE.
To distinguish it from the original model, the suffix **MagPIE-Brazil** is used.

## HARDWARE REQUIREMENTS
The model is quite resource heavy and works best on machines with high CPU clock
and memory. Recommended is a machine with at least 16GB of memory and a Core i7 CPU or similar.

Commands formatted as `code` should generally be run in a terminal (PowerShell on Windows).

### List of Requirements
- license for gams incl. CONOPT solver
- gams >= 50.1.0
- git >= 2.23
- R >= 4.3 (+ matching Rtools on Windows)
- pandoc >= 2.14.2
- TeX >= 3.14159265

### OS specific setup
Choose your operating system and follow the instructions there. You can also
install requirements differently (e.g. using only installers on Windows), in
the end it is only important that all requirements are installed in a suitable
version and added to the PATH environment variable, so MAgPIE can use them.

#### Ubuntu
1. make sure you have a gams license incl. the CONOPT solver
1. [install gams](https://www.gams.com/46/docs/UG_UNIX_INSTALL.html)
1. install git, R, and pandoc with `sudo apt install git r-base pandoc`
1. install TinyTeX with `Rscript -e 'install.packages("tinytex"); tinytex::install_tinytex()'`

In case R package installations fail during compilation, install the following system packages:
```
sudo apt install build-essential cmake gdal-bin libcurl4-gnutls-dev libcurl4-openssl-dev libfontconfig1 libfreetype-dev libfribidi-dev libgdal-dev libgit2-dev libglpk-dev libharfbuzz-dev libjpeg-dev libnetcdf-dev libpng-dev libpoppler-cpp-dev libssl-dev libtiff5-dev libudunits2-dev libxml2-dev pari-gp qpdf
```
This list is highly system specific and most likely incomplete. Pay close attention to error messages, usually they state which system package needs to be installed.

#### macOS
We recommend to NOT have an active conda environment (if you're unsure what this means you likely don't have conda) when working with magpie (`conda deactivate`). We recommend installing system packages via [brew](https://brew.sh/).
Install R from https://cran.r-project.org/bin/macosx/
Choose the right version: arm for Apple Silicon (M1, M2, …), x86_64 for older Intel-based Macs.
Install gfortran from https://cran.r-project.org/bin/macosx/tools/
1. make sure you have a gams license incl. the CONOPT solver
1. [install gams](https://www.gams.com/46/docs/UG_MAC_INSTALL.html)
1. install git and pandoc with `brew install git pandoc`
1. install TinyTeX with `Rscript -e 'install.packages("tinytex",repos="https://cloud.r-project.org"); tinytex::install_tinytex()'`

Usually macOS users can download precompiled binary R packages, but in case R package installations fail during compilation, install the following system packages:
```
brew install abseil cmake fribidi gdal harfbuzz libgit2 libpng libtiff libxml2 pkg-config
```
This list is highly system specific and most likely incomplete. Pay close attention to error messages, usually they state which system package needs to be installed.

#### Windows
Most of the installation steps require administrator rights.
1. make sure you have a gams license incl. the CONOPT solver
1. [install gams](https://www.gams.com/46/docs/UG_WIN_INSTALL.html)
1. [download .msi pandoc file](https://github.com/jgm/pandoc/releases/latest) and run installer (`choco install pandoc` did not work in testing)
1. [install chocolatey](https://chocolatey.org/install)
1. install git, rig (R installer), and tinytex with `choco install -y git rig tinytex`
1. restart terminal
1. install R and Rtools with `rig add release; rig add rtools`

### check setup is complete
- restart terminal (now without administrator privileges)
- `gams` should print many lines including "The installed license is valid."
- `git --version`
- `Rscript --version`
- `pandoc --version`
- `tex --version`

If any of these are not found: Find the path to that executable
(gams/git/Rscript/pandoc/tex, on Windows ending in '.exe') and add it to your account's
PATH environment variable. Search for a tutorial online if you are unsure how to do that,
or take a look at the detailed Windows instructions and troubleshooting below.

### download and run MAgPIE
1. download MAgPIE with `git clone https://github.com/magpiemodel/magpie.git`
1. go into the MAgPIE folder `cd magpie`
1. start a MAgPIE run with `Rscript start.R`, first time: installs all required R packages (takes a while)
1. choose "1" for a default run
1. then select "1" for direct execution

### troubleshooting
Please check [this discussion](https://github.com/magpiemodel/magpie/discussions/650) for known problems and solutions and to report new problems you encounter while setting up MAgPIE.

## HOW TO CONFIGURE
Model run settings are set in `config/default.cfg` (or another config file of
the same structure). New model scenarios can be created by adding a column to
`config/scenario_config.csv`

## HOW TO RUN
To run the model execute `Rscript start.R` (or `source("start.R")` from within
R) in the main folder of the model.
This will give you a list of available run scripts you can choose from. You can
also add your own run scripts by saving them in the folder scripts/start. To run
a single model run with settings as stated in default.cfg you can choose start
script "default". Make sure that the config file has been set correctly before
starting the model.

## HOW TO CONTRIBUTE
We welcome contributions related to the development and application of MagPIE-Brazil.

For contributions to the original MAgPIE framework, please refer to:
https://github.com/magpiemodel/magpie

## DEPENDENCIES
Model dependencies **must be publicly available** and should be Open Source.
Development aim is to rather minimize than expand dependencies on non-free
and/or non open source software. That means that besides currently existing
dependencies on GAMS, the GDXRRW R package and the corresponding solvers there
should be no additional dependencies of this kind and that these existing
dependencies should be resolved in the future if possible.

If a new R package is added as dependency this package should fulfill the
following requirements:
* The package is published under an Open Source license
* The package is distributed through CRAN or PIK-CRAN (the PIK-based,
  but publicly available package repository).
* The package source code is available through a public, version controlled
  repository such as GitHub

For other dependencies comparable measures should apply. When a dependency is
added this dependency should be added to the *HOW TO INSTALL* section in the
README file of the model framework (mentioning the dependency and explaining
how it can be installed). If not all requirements can be fulfilled by the new
dependency this case should be discussed with the model maintainer
(magpie@pik-potsdam.de) to find a good solution for it.

## INPUT DATA

In order to allow other researchers to reproduce and use work done with MAgPIE
one needs to make sure that all components necessary to perform a run can be
shared. One of these components is the input data. As proprietary data usually
does not allow its free distribution it should generally be avoided.

When adding a new data source, make sure that it can be freely shared with
others. If this is not the case please consider using a different source or
solution.

Data preparation should ideally be performed with the **madrat** data processing
framework (https://github.com/pik-piam/madrat). This makes sure that the
processing is reproducible and links properly to the already existing data
processing for MAgPIE.

In case that these recommendations can not be followed we would be happy if you
could discuss that issue with the MAgPIE development team
(magpie@pik-potsdam.de).

## MODEL OUTPUT

By default the results of a model run are written to an individual results folder within the "output/" folder of the model. The two most important output files are the fulldata.gdx and the report.mif. The fulldata.gdx is the technical output of the GAMS optimization and contains all quantities that were used during the optimization in unchanged form. The mif-file is a csv file of a specific format and is synthetized from the fulldata.gdx by post-processing scripts. It can be read in any text editor or spreadsheet program and is well suited for a quick look at the results and for further analysis.

## CONTACT
For MagPIE-Brazil: 
(project-mail)

For original MAgPIE:
magpie@pik-potsdam.de

## CITATION
See file CITATION.cff or the documentation.

When using MagPIE-Brazil, clearly indicate that results are based on a modified version of MAgPIE.

## AUTHORS
See list of authors in CITATION.cff

(Additional contributors for MagPIE-Brazil)

## CHANGELOG
See MAgPIE-Brazil log on GitHub (https://github.com/fgv-agro/magpie)
See original log on GitHub (https://github.com/magpiemodel)

