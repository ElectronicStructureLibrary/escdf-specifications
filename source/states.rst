States
======
	 
General overview
----------------

All states should be stored in the **states** group of a ESCDF file. If
several sets of states are present, they should be put in subgroups,
with explicit names. The choice of name for the subgroup is left to the
user, with the restriction that it cannot be any of the names already in
use in these specifications. If only one set of states is to be
specified, then it can be stored directly in the **states** group or in
its own subgroup.

The group must have the following attributes:

-  **number\_of\_spins**
-  **number\_of\_spinor\_components**
-  **number\_of\_components**
-  **k\_dependent**
-  **max\_state\_index**
-  **min\_state\_index**
-  **numbers\_of\_states**
-  **number\_of\_kpoints**

The group must contain the following datasets:

-  **eigenvalues**
-  **occupations**
-  **reduced\_coordinates\_of\_kpoints**
-  **kpoint\_weights**
-  **coefficients\_of\_wavefunctions**

The group may contain the following optional datasets:

-  **highest\_state\_index**
-  **lowest\_state\_index**

Detailed description of variables
---------------------------------

General variables
~~~~~~~~~~~~~~~~~

-  **number\_of\_spins**: unsigned int
   Used to distinguish collinear spin-up and spin-down components:

   -  ``1`` for non-spin-polarized or spinor wavefunctions
   -  ``2`` for collinear spin (spin-up and spin-down)

-  **number\_of\_spinor\_components**: unsigned int
   For non-spinor wavefunctions, this dimension must be present and
   equal to ``1``. For spinor wavefunctions, this dimension must be
   equal to ``2``.

-  **number\_of\_components**: unsigned int
   Used for the spin components of spin-density matrices:

   -  ``1`` for non-spin-polarized
   -  ``2`` for collinear spin (spin-up and spin-down)
   -  ``4`` for non-collinear spin

-  **max\_state\_index**: int
-  **min\_state\_index**: int
-  **highest\_state\_index**: int
   Highest index of a state for each kpoint, if varying (the attribute
   **k\_dependent** must be set to ``yes``). Otherwise (the attribute
   **k\_dependent** must be set to ``no``), might not contain any
   information, the highest index of states being set to
   **max\_state\_index**.

-  **lowest\_state\_index**: int
   Lowest index of a state for each kpoint, if varying (the attribute
   **k\_dependent** must be set to ``yes``). Otherwise (the attribute
   **k\_dependent** must be set to ``no``), might not contain any
   information, the lowest index of states being set to
   **min\_state\_index**. This variable is useful for passing data from
   a ground-state calculation to an optical calculation in which only a
   subset of bands around the Fermi level are typically used.

-  **eigenvalues**
   double[**number\_of\_spins**][**number\_of\_kpoints**][**max\_number\_of\_states**]
   One-particle eigenvalues/eigenenergies (real-part). The **units**
   attribute is required. The attribute **scale\_to\_atomic\_units**
   might also be mandatory.

-  **k\_dependent**: bool
   Needed for the variables **number\_of\_states**,
   **number\_of\_coefficients**, and
   **reduced\_coordinates\_of\_plane\_waves**.

-  **numbers\_of\_states**: int[**number\_of\_spins**]
   [**number\_of\_kpoints**]
   The attribute **k\_dependent** must be defined

-  **occupations**:
   double[**number\_of\_spins**][**number\_of\_kpoints**][**max\_number\_of\_states**]
   Occupation numbers. Full occupation for spin-unpolarized cases
   (**number\_of\_spins** = ``1`` AND **number\_of\_spinor\_components**
   = ``1``) is ``2``, otherwise it is ``1``.

-  **eigenvalues\_imaginary**:
   double[**number\_of\_spins**][**number\_of\_kpoints**][**max\_number\_of\_states**]
   One-particle eigenvalues/eigenenergies (imaginary part), *i.e.* for
   complex-scaled Hamiltonian or self-energies.

Variables relating to k-points
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  **number\_of\_kpoints**: int
   The number of kpoints.

-  **reduced\_coordinates\_of\_kpoints**:
   double[**number\_of\_kpoints**] [**number\_of\_dimensions**]
   k-point in relative / reduced coordinates, *e.g.* in the interval [0,
   1]. The values in non-periodic dimensions should be zero.

-  **kpoint\_weights**: double[**number of kpoints**]
   k-point integration weights. The weights must sum to 1.

Optional information that could generate the k-grid:

-  **kpoint\_grid\_numbers**: int[**number of dimensions**]
   Number of k-points in each direction of Monkhorst-Pack k-grid [*Phys.
   Rev. B* **13**, 5188 (1976)].

-  **kpoint\_grid\_shift**: double[**number\_of\_dimensions**]
   Shift for offset of Monkhorst-Pack k-grid, in fractional units (e.g.
   (-1, 1)).

-  **kpoint\_energy\_cutoff**: double
   Like plane-wave kinetic energy cutoff, but applied to generating a
   sphere of k-points. This is the way of specifying the k-grid in some
   codes (eg. SIESTA).

Variables relating to wavefunctions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  **coefficients\_of\_wavefunctions**:
   Wavefunction coefficients. Note that each wavefunction must be
   normalized to 1.
