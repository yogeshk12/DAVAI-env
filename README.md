DAVAI environment & interface
=============================

This project contains:

* the DAVAI command-line tools, esp. to create DAVAI experiments,
* the configuration files to handle general preferences and machine-dependent installation,
* the documentation

Note that the core of DAVAI (tests templates, jobs sequences, config files and launching wrappers) are hosted
separately, in the [DAVAI-tests](https://github.com/ACCORD-NWP/DAVAI-tests) repository.

Dependencies
------------

DAVAI is mainly written in Python3. Make sure you have Python3.6 at least.
It also uses Git, make sure you have a "recent enough" version of it, or some commands may not work properly.
DAVAI works over a number of NWP packages, tools, software, that need to be installed on the machine with their own
procedures. These include:

* [_**Vortex**_](https://opensource.umr-cnrm.fr/projects/vortex):
  scripting system used for the definition of tasks (resources, executables launch, ...) and the running
  of the jobs. It embeds a number of necesary-as-well sub-packages.
* [_**ecbundle**_](https://git.ecmwf.int/projects/ECSDK/repos/ecbundle):
  a utility from ECMWF to gather codes from several repositories, in the required version for each,
  based on a YAML descriptive file (called _bundle_)
* [_**IAL-build**_](https://github.com/ACCORD-NWP/IAL-build):
  wrappers around `git` and `gmkpack` (and eventually other building tools) to build IAL executables from Git
* [_**IAL-expertise**_](https://github.com/ACCORD-NWP/IAL-expertise):
  tools to analyse automatically the outputs of NWP configurations -- norms, Jo-tables, fields in FA/GRIB files, ...
* [_**EPyGrAM**_](https://github.com/UMR-CNRM/EPyGrAM): a Python library for handling output data from the IAL models;
  it is used here within _IAL-expertise_.

These packages may already be pre-installed on MF's HPC or other platforms where DAVAI is already ported.
Cf. the "Local complements" in "Installation" section, in this case.

To install them on a new machine, cf. the projects' installation instructions.

Installation
------------

1. Clone this repository, e.g. in `~/repositories/`:\
   `git clone https://github.com/ACCORD-NWP/DAVAI-env.git`
2. Initialize your DAVAI environment:
   - `cd DAVAI-env`
   - if you want to inspect possible customizations: `bin/davai-init -s`
   - `make init` (or `bin/davai-init`) --- Note that this will also clone the _**DAVAI-tests**_ repository
3. Get command-lines in your PATH (preferably in your `.bash_profile`):\
   `export PATH=$PATH:~/.davairc/bin`

Local complements:
* for [`belenos`@MF](doc/belenos.md)

Documentation
-------------

The documentation is available under `doc/` directory.
Part of the documentation needs to be compiled from `.tex` sources, using `pdflatex`.
To do so:

* `make doc`

and the generated PDF document will be found under `doc/pdf/Davai_User_Guide.pdf`.

The User Guide is also available for main releases on: https://github.com/ACCORD-NWP/DAVAI-env/releases

Quick start
-----------

A Tutorial is available in the User Guide (cf. above).

For a quick start:

1. Prepare an experiment based on version `<v>` of the tests, to validate an IAL Git reference `<r>`:\
   `davai-prep_xp <r> -v <v> [-h]`\
   (you may need to specify the path to your IAL repository by argument, cf. options with `-h`)\
   To know what version of the tests to use, cf. [README.md in DAVAI-tests](https://github.com/ACCORD-NWP/DAVAI-tests#readme)
2. Go to the prompted directory of the experiment (ending with `.../dv-<platform>@<user>/davai/nrv/`)
3. Run the tests: `./RUN_XP.sh` and monitor (standard output for the build, then job scheduler).

Explanations to be found in the User Guide.

Lexicon
-------

* **DAVAI** stands for: _"Device Aiming at the VAlidation of IAL"_
* **IAL** = IFS-Arpege-LAM

