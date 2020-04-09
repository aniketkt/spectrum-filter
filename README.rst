==========
spectrum-filter
==========

**spectrum-filter** is command-line-interface to compute the effective spectrum of a polychromatic x-ray beam passing through user-selected filters and illuminating a user-selected scintillator crystal.


Installation
============

::

    $ git clone https://github.com/tomography/tomopy-cli.git
    $ cd tomopy-cli
    $ python setup.py install

in a prepared virtualenv or as root for system-wide installation.

.. warning:: If your python installation is in a location different from #!/usr/bin/env python please edit the first line of the bin/tomopy file to match yours.

After the installation you will be prompted to::

    $ source /Users/userid/complete_tomopy.sh

This enable the autocompletition of all tomopy recon options. Just press tab after::

    $ tomopy recon --<TAB> <TAB>
    
to select and optional parameter and show its default value.
 
.. warning:: in some systems you are required to set omplete_tomopy.sh as executable with::

    $ chmod +x /Users/userid/complete_tomopy.sh

Update
======

**tomopy** is constantly updated to include new features. To update your locally installed version::

    $ cd tomopy-cli
    $ git pull
    $ python setup.py install


Dependencies
============

Install the following package::

    $ conda install -c conda-forge tomopy

Optionally, *dxchange* may be needed for file I/O::

    $ conda install -c conda-forge dxchange


Usage
=====

Reconstruction
--------------

To do a tomographic reconstruction::

    $ tomopy recon --file-name /local/data.h5

from the command line. To get correct results, you may need to append
options such as `--rotation-axis` to set the rotation axis position::

    $ tomopy recon --rotation-axis 1024.0 --file-name /local/data.h5

to list of all available options::

    $ tomopy recon -h


Configuration File
------------------

Reconstruction parameters are stored in **tomopy.conf**. You can create a template with::

    $ tomopy init

**tomopy.conf** is constantly updated to keep track of the last stored parameters, as initalized by **init** or modified by setting a new option value. For example to re-run the last reconstrusction with identical parameters just use::

    $ tomopy recon

To run a reconstruction with a different and previously stored configuration file **old_tomopy.conf** just use::

    $ tomopy recon --config old_tomopy.conf


Find Center
-----------

To automatically find the rotation axis location of all tomographic hdf data sets in a folder (/local/data/)::

    $ tomopy find_center --file-name /local/data/


this generates in the /local/data/ directory a **rotation_axis.json** file containing all the automatically calculated centers::

            {"0": {"proj_0000.hdf": 1287.25}, "1": {"proj_0001.hdf": 1297.75},
            {"2": {"proj_0002.hdf": 1287.25}, "3": {"proj_0003.hdf": 1297.75},
            {"4": {"proj_0004.hdf": 1287.25}, "5": {"proj_0005.hdf": 1297.75}}

to list of all available options::

    $ tomopy find_center -h


After using **find_center**, to do a tomographic reconstruction of all tomographic hdf data sets in a folder (/local/data/)::

    $ tomopy recon --file-name /local/data/


Help
----

::

    $ tomopy -h
    usage: tomopy [-h] [--config FILE] [--version]  ...

    optional arguments:
      -h, --help     show this help message and exit
      --config FILE  File name of configuration file
      --version      show program's version number and exit

    Commands:
      
        init         Create configuration file
        recon        Run tomographic reconstruction
        find_center  Find rotation axis location for all hdf files in a directory

Testing
=======

Tomopy-cli contains partial test coverage. For development and
testing, a developer installation is recommended::

    $ git clone https://github.com/tomography/tomopy-cli.git
    $ cd tomopy-cli
    $ python setup.py develop

Tests can be run using the pytest runner::

    $ pip install pytest
    $ pytest