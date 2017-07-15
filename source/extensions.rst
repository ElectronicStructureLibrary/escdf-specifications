.. raw:: mediawiki

   {{techbox |
   data standards = 
   <li>[[ESCDF - Electronic Structure Common Data Format]]</li>
   <li>[[ESCDF - System]]</li>
   <li>[[ESCDF - Basis sets]]</li>
   <li>[[ESCDF - Densities]]</li>
   <li>[[ESCDF - Potentials]]</li>
   <li>[[ESCDF - States]]</li> |
   software = <li>[[libescdf]]</li> |}}

Version
-------

File format version number:

General overview
----------------

A data format cannot cover all possible use cases. In some situations,
the user may repeatedly need some data that is of interest to only one
particular software project and which is not part of the core of the
format. This additional piece of data may even be absolutely necessary
to make the file format of interest for this user or to make it possible
to exchange data with collaborators. In such a case, an ***extension***
can be added to the specifications.

In order to be valid, an extension must:

-  select one and only one **** lower-case keyword that actually
   represents the corresponding software project;
-  use **/extensions/** as root namespace;
-  follow the general guidelines of the file format regarding the
   contents of the group;
-  provide an up-to-date documentation on the ESL wiki.

A list of currently reserved keywords for project-specific extensions is
provided hereafter. Please add yours to the table preserving
alphabetical order before providing an extension.

Reserved keywords
-----------------

The following table summarises the keywords reserved for the projects
currently participating to the data format initiative.

+--------------+------------------+-------------------------------------------+
| Keyword      | Project          | Website                                   |
+==============+==================+===========================================+
| abinit       | Abinit           | http://www.abinit.org/                    |
+--------------+------------------+-------------------------------------------+
| berkeleygw   | BerkeleyGW       | http://www.berkeleygw.org/                |
+--------------+------------------+-------------------------------------------+
| octopus      | Octopus          | http://www.tddft.org/programs/octopus/    |
+--------------+------------------+-------------------------------------------+
| wien2k       | WIEN2k           | http://www.wien2k.at/                     |
+--------------+------------------+-------------------------------------------+
| yambo        | Yambo            | http://www.yambo-code.org/                |
+--------------+------------------+-------------------------------------------+
| sprkkr       | Munich SPR-KKR   | http://ebert.cup.uni-muenchen.de/sprkkr   |
+--------------+------------------+-------------------------------------------+

--------------

Back to `ESCDF - Electronic Structure Common Data
Format <ESCDF_-_Electronic_Structure_Common_Data_Format>`__

`Category:ESL entries <Category:ESL_entries>`__ Category:I/O
`Category:Data standards <Category:Data_standards>`__
