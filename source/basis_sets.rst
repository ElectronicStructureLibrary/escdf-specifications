Basis Sets
==========
	 
General overview
----------------

Basis set information within an ESCDF HDF5 file is stored within the
**basis\_sets** group and its subgroups.

The ESCDF specifications provide support for two types of basis sets:
cell-dependent basis sets spreading over the whole simulation cell and
atom-centered basis sets associated to the local environment of atoms.
Each type of basis set is stored in a different subgroup. Therefore the
**basis\_sets** group must contain one of the following subgroups:

-  **cell\_dependent**
-  **atom\_centered**

Cell-dependent
~~~~~~~~~~~~~~

The **cell\_dependent** group stores information on a basis set covering
the whole simulation cell. If more than one cell-dependent basis set are
to be stored in the same **cell\_dependent** group, then each should go
to its own subgroup. The choice of name for the subgroup is left to the
user, with the restriction that it cannot be any of the names already in
use in these specifications. If only one cell-dependent basis set is to
be specified, then it can be stored directly in the **cell\_dependent**
group or in its own subgroup.

The current specification support three types of cell-dependent basis
sets:

-  plane waves
-  real-space grids
-  wavelets

The group must have the following attributes:

-  **kind**
-  **number\_of\_physical\_dimensions**
-  **number\_of\_coefficients**

The remaining datasets and attributes that need to or might be set
depend on the kind of basis set.

Plane waves
^^^^^^^^^^^

The group must include the following dataset:

-  **reduced\_coordinates\_of\_plane\_waves**

Real-space grids
^^^^^^^^^^^^^^^^

The group must have the following attribute:

-  **number\_of\_grid\_points**

The group must include the following dataset:

-  **coordinates\_of\_basis\_grid\_points**

Wavelets
^^^^^^^^

The group must have the following attributes:

-  **number\_of\_grid\_points**
-  **order\_of\_daubechies\_wavelets**

The group must include the following dataset:

-  **coordinates\_of\_basis\_grid\_points**

The group might include the following dataset:

-  **number\_of\_coefficients\_per\_grid\_points**

Atom-centered
~~~~~~~~~~~~~

TODO. See discussion page for more details.

Detailed description of variables
---------------------------------

Variables relating to cell-dependent basis sets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  **kind**: attribute, char(80)
   String representing the type of basis set used. Must be one of
   ``plane_waves``, ``wavelets``, or ``realspace_grids``.

-  **number\_of\_physical\_dimensions**: attribute, unsigned int (always
   3)
   The number of physical dimensions in space. Note that this is not the
   same as the number of periodic directions, which might be less than
   or equal to this number.

-  **number\_of\_coefficients**: attribute, unsigned int
   Total number of basis function coefficients.

-  **number\_of\_grid\_points**: attribute, unsigned int
   Number of grid points where coefficients can be stored.

-  **coordinates\_of\_basis\_grid\_points**: dataset, double
   [**number\_of\_grid\_points**][**number\_of\_physical\_dimensions**]
   (dimensional variable: length)
   Coordinates of the grid points where coefficients can be stored. This
   is used to define a real-space basis set where a reduced set of
   points is used. This array may be used in conjunction with the
   variable **number\_of\_coefficients\_per\_grid\_points**.

-  **number\_of\_coefficients\_per\_grid\_points**: dataset, unsigned
   int [**number\_of\_grid\_points**]
   This array gives the number of coefficients stored on basis set grid
   points. The coordinates of corresponding grid points are given in the
   **coordinates\_of\_basis\_grid\_points** array. If it is omitted, all
   the values are assumed to be 1, that is, there is only one
   coefficient stored on each basis set grid point. The sum of all its
   values must be equal to **number\_of\_coefficients**.

-  **order\_of\_daubechies\_wavelets**: attribute, unsigned int
   This number gives the order of the Daubechies wavelet basis, e.g. if
   **order\_of\_daubechies\_wavelets** is 14, the Daubechies wavelets
   are made from a piecewise polynomial of order 14.

-  **reduced\_coordinates\_of\_plane\_waves**: dataset, double
   [**number\_of\_coefficients**][**number\_of\_physical\_dimensions**]
   Plane-wave G-vectors in relative / reduced coordinates.

Variables relating to atom-centered basis sets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TODO. See discussion page for more details.

