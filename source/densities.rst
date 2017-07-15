.. raw:: mediawiki

   {{techbox |
   data standards = 
   <li>[[ESCDF - Electronic Structure Common Data Format]]</li>
   <li>[[ESCDF - System]]</li>
   <li>[[ESCDF - Basis sets]]</li>
   <li>[[ESCDF - Potentials]]</li>
   <li>[[ESCDF - States]]</li>
   <li>[[ESCDF - Extensions]]</li> |
   software = <li>[[libescdf]]</li> |}}

Page under construction

Version
-------

File format version number:

General overview
----------------

Overall strategy
~~~~~~~~~~~~~~~~

To represent densities, we have to follow the way they are decomposed
within the different methods in use:

-  norm-conserving pseudopotentials:
   :math:`\tilde{\rho}(r) = \sum_{n} \langle \tilde{\Psi}_n \vert r \rangle \langle r \vert\tilde{\Psi}_n \rangle`;
-  ultrasoft pseudopotentials and PAW:
   :math:`\rho(r) = \tilde{\rho}(r) + \hat{\rho}(r)`;
-  all-electrons:
   :math:`\rho(r) = \left\lbrace \rho_{sph}^{core}(r) + \rho_{sph}^{val}(r) \right\rbrace + \rho_{inter}^{val}(r)`.

Mandatory components
~~~~~~~~~~~~~~~~~~~~

For the use cases considered, the cell-associated electronic density can
be represented in the following ways:

-  norm-conserving pseudopotentials method: :math:`\tilde{\rho}(r)`;
-  ultrasoft pseudopotentials and PAW methods:
   :math:`\tilde{\rho}(r) + \hat{\rho}(r)`;
-  all-electrons methods: :math:`\rho_{inter}^{val}(r)`.

For the use cases considered, the atom-centered electronic density can
be represented in the following ways:

-  all-electrons methods:
   :math:`\rho_{sph}^{core}(r) + \rho_{sph}^{val}(r)`;
-  gaussians (?): :math:`\tilde{\rho}(r)`.

Optional components
~~~~~~~~~~~~~~~~~~~

In the case of PAW, providing the occupancy matrix elements
:math:`\rho_{ij}` in addition to the density components allows the
rebuilding of all necessary quantities to restart a calculation.

Spinors
~~~~~~~

In the presence of spinors, there are 2 possible ways of representing
the 4 density components:

-  total density :math:`\rho(r)` + magnetic moment :math:`\vec{m}(r)`
   (well-suited for visualisation);
-  the matrix elements :math:`\rho^{\alpha\beta}(r)`, for
   :math:`\alpha,\beta = \uparrow,\downarrow`;

which means that the chosen representation must be indicated as
metadata.

Detailed description of variables
---------------------------------

All densities should be stored in the **densities** group of a ESCDF
file.

If several densities are present, they should be put in subgroups, with
explicit names.

Variables relating to the cell associated densities
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cell description
^^^^^^^^^^^^^^^^

The cell description is identical to the one in the `ESCDF -
Geometries <ESCDF_-_Geometries>`__. It must contain the following
information:

-  **number\_of\_physical\_dimensions**: unsigned int (always ``3``)
-  **dimension\_types**: int [**number\_of\_physical\_dimensions**]
   (between ``0`` and ``2``)
-  **lattice\_vectors**: double [**number\_of\_physical\_dimensions**]
   [**number\_of\_physical\_dimensions**] (dimensional variable: length)

Densities description
^^^^^^^^^^^^^^^^^^^^^

These variables are designed to represent densities that are stored on a
regular real-space grid. This grid is defined by its mesh size.

-  **number\_of\_grid\_points**: unsigned int
   [**number\_of\_physical\_dimensions**]
   When a direction is defined as periodic, the grid points in that
   direction do not contain the last plane, while for the other cases,
   the last plane in that direction contains a value.

-  **values\_on\_grid**: double [**'number\_of\_components**,
   product(\ **number\_of\_grid\_points**), **real\_or\_complex**]
   The default order is along z, y, and x (values along x axis are
   contiguous in memory). If the default ordering is not used, the
   attribute **use\_default\_ordering** must be set to false and
   **grid\_ordering** must be provided.

-  **use\_default\_ordering**: int
   This attribute specifies if the default z, y, and x ordering is used
   or not. When false, the optional variable **grid\_ordering** must be
   present.

-  **grid\_ordering**: unsigned int
   [product(**number\_of\_grid\_points**]
   This array provides a lookup table. **``grid_ordering``**\ ``[i]``
   ``=`` ``j`` means that **values\_on\_grid**\ [:,i,:] is the jth
   component of the density. This variable is optional, when not present
   the default ordering for the density is implicit.

--------------

Back to `ESCDF - Electronic Structure Common Data
Format <ESCDF_-_Electronic_Structure_Common_Data_Format>`__

`Category:ESL entries <Category:ESL_entries>`__ Category:I/O
`Category:Data standards <Category:Data_standards>`__
