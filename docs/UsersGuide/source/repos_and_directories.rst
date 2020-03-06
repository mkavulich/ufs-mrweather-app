.. _repos_and_directories:

=========================================
Code repositories and directory structure
=========================================

This chapter describes the code repositories that comprise the UFS MR Weather App,
without describing, in detail, any of the components.

Hierarchical Repository Structure
---------------------------------

The umbrella repository for the UFS MR Weather App is named ufs-mrweather-app and is
available on GitHub at https://github.com/ufs-community/ufs-mrweather-app. An umbrella
repository is defined as a repository that includes links, called externals, to additional
repositories.  The UFS MR Weather App includes the ``checkout_externals`` tools along with a
configuration file called ``Externals.cfg``, which describes the external repositories
associated with this umbrella (see :numref:`Table %s <top_level_repos>`).

.. _top_level_repos:

.. table::  List of top-level repositories that comprise the UFS MR Weather App.

   +----------------------------+---------------------------------------------------------+
   | **Repository Description** | **Authoritative repository URL**                        |
   +============================+=========================================================+
   | Umbrella repository for    | https://github.com/ufs-community/ufs-mrweather-app      |
   | the UFS Weather App        |                                                         |
   +----------------------------+---------------------------------------------------------+
   | Umbrella repository for    | https://github.com/ufs-community/ufs-weather-model      |
   | the UFS Weather Model      |                                                         |
   +----------------------------+---------------------------------------------------------+
   | CIME CSS                   | https://github.com/ESMCI/cime                           |
   +----------------------------+---------------------------------------------------------+
   | Layer required for CIME to | https://github.com/ESCOMP/fv3gfs_interface              |
   | build ufs-weather-model    |                                                         |
   +----------------------------+---------------------------------------------------------+
   | Layer required for CIME to | https://github.com/ESCOMP/NEMS_interface                |
   | build NEMS driver          |                                                         |
   +----------------------------+---------------------------------------------------------+

The UFS MR Weather Model is itself an umbrella repository and contains a number of sub-repositories
used by the model as documented `here
<https://ufs-mr-weather-app.readthedocs.io/projects/ufs-weather-model/en/latest/CodeOverview.html>`_.
The CIME repository contains the workflow and build system for the prognostic model.  The last
two repositories provide interfaces to allow CIME to properly build the ufs-weather-model and the NEMS driver.

.. note::

   Note that the prerequisite libraries (including NCEP Libraries) are not included in the UFS MR
   Weather App repository.  The source code for these components resides in the umbrella
   repositories `NCEPLIBS <https://github.com/NOAA-EMC/NCEPLIBS>`_ and
   `NCEPLIBS-external <https://github.com/NOAA-EMC/NCEPLIBS-external>`_. The former has links to the
   `chgres_cube preprocessor repository <https://github.com/NOAA-EMC/UFS_UTILS>`_ and to `UPP
   <https://github.com/NOAA-EMC/EMC_post>`_.

These external components are already built on the preconfigured platforms
listed `here <https://github.com/ufs-community/ufs/wiki/Supported-Platforms-and-Compilers>`_.
However, they must be cloned and built on other platforms according to the instructions provided in the
wiki pages of those repositories: <https://github.com/NOAA-EMC/NCEPLIBS/wiki>` and
<https://github.com/NOAA-EMC/NCEPLIBS-external/wiki>.

Directory Structure
-------------------

The directory structure on disk for users of the MR Weather App depends on whether one is using
a pre-configured platform. Users working on pre-configured platforms will only have the
files associated with the ufs-mrweather-app in their disk space. The directory structure is set
in configuration file ``Externals.cfg``, which is in the top directory where the umbrella repository
has been cloned. A listing of the directory structure is shown :ref:`here <top_level_dir_structure>`.

The directory structures for the standalone UFS Weather Model and the UFS Weather Model included with
the UFS MR Weather App are equal in that they contain subdirectories for FMS, FV3, NEMS and
stochastic_physics. However, in the UFS Weather App, subdirectories are located under ``src/model``.
The UFS MR Weather App also includes directories for CIME, such as the ``src/model/FV3/cime`` and
``src/model/NEMS/cime`` directories.

Users working outside of preconfigured platforms will have additional files on disk associated with
the libraries, pre- and post-processing.  The resulting directory structure is determined by the path
settings in the NCEPLIBS ``.gitmodules`` file.