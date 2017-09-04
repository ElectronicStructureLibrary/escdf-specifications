Introduction
============

ESCDF are data representation standards based on
`HDF5 <https://hdfgroup.org/HDF5/>`__ for large data sets
(wave-functions, expansion coefficients, electron density, local density
of states, etc.).

These standards are the result of a collaboration between the ESL, the
`NOMAD Center of Excellence <https://nomad-coe.eu/>`__, and the `EUSpec
Network <http://www.euspec.eu/>`__.

Tools for the simpler reading and writing of these representations are
coded in the library `libescdf <http://esl.cecam.org/Libescdf>`__, which is under
development.

Both the standards and the tools originate from a first standardisation
effort done in the European Nanoquanta Network of Excellence, which
resulted in the `ETSF File Format
Specifications <http://esl.cecam.org/ETSF_File_Format_Specifications>`__.


Motivations
-----------

The main objectives of this data format are the following:

-  enable a platform-independent exchange of data between
   electronic-structure programs;
-  provide specifications which are both flexible and suitable for
   High-Performance Computing (HPC);
-  hide the gory details of the I/O implementation, in particular the
   way parallelism is handled;
-  facilitate, strengthen and extend interdisciplinary collaborations
   within and without the electronic-structure community.

Use cases
---------

The current version of the format is intended to support the following
use cases:

-  restarting a calculation;
-  exchanging data between 2 codes in a multi-step calculation;
-  visualisation.

