These are two COMSOL program files to simulate the laser-generated heat transfer in vitrified EM grids descriped in the paper titled : '  Effects of base temperature, immersion medium, and EM grid material on devitrification thresholds in cryogenic optical super-resolution microscopy'. Citation: to be mentioned.

**How to use the heat transfer simulation program**:

* Simulation parameters:

 -mesh size, support film thickness, ice thickness, heat conductivities, peak laser intensity, etc, are defined in the parameter table under:
Global Definitions/Parameters.

-The Gaussian beam profile is named ‘GaussianBeam’ and is defined under: 
Component/Definitions/analytic.

-The Gaussian distribution is fed in laser expression named ‘LaserHeat’ and is defined under:
Component/Definitions/variables.


* Geometry:

The geometry is defined as follows:

1-The support film empty hole specified by hole/ice radius named ‘iceRad’ under:
Geometry: work plane: plane geometry: circle. 

2- making an array of holes under: work plane: transform: Array; where the number of holes along x and y directions as well as the displacement between hole-to-hole centers named ‘iceSpacing’ is specified.

3- a square with the size of ‘squareSize’ is defined.

4- the array of holes is subtracted from the square under: work plane/Boolean and partitions/Difference to make the support film 2D geometry.

5- the 2D geometry is extruded with the size of support film thickness named ‘supportThick’ (15 nm for carbon and 50 nm for gold/silver). 

Note 1: depending on the support film material, this parameter needs to be set in the parameters table.

6- a homogenous flat ice layer with the same lateral size as the support film and the thickness of ‘iceThick’ is defined on top of the support film under: Geometry/Block.

Note 2: In the case of heat transfer simulation in HFE-7200 (cryo-immersion), the additional material layers, i.e., glass coverslip and HFE-7200 (considered as solid at 133 K), are added to the geometry as ‘Blocks’ with corresponding thicknesses mentioned for Fig. 1c.

* Physics:

The physics module used is ‘heat transfer in solids (ht)’. The boundary condition for the geometry in nitrogen gas and base temperature of 77 K is defined as:
1-The initial temperature is set under: Initial values: Physics/Domains/Initial values.

2-The fixed temperatures at the surrounding surfaces of support film and ice are set under: Physics/Boundaries/Temperature.

3- The convective heat transfer is defined as ‘convective heat flux’ at the upper and lower surfaces of the geometry, a constant coefficient ‘h’, and external temperature ‘ T_ext’ under: Physics/Boundaries/Heat Flux. H is set to zero for the simulation of the vacuum cryostats.

4-The laser-generated heat source is defined as ‘laserHeat/(supportThick+iceThick)’. (laserHeat was already defined under ‘Definitions’).

Note 3: In the case of heat transfer simulation in HFE-7200 (cryo-immersion), we assume that the objective lens and the sample holder are infinitely spread parallel surfaces facing each other compared to the simulated small grid square. To ensure a temperature gradient from the warm objective (173 K) to the cold specimen holder (133 K), we define periodic boundary conditions at the opposite side surfaces of HFE-7200 and glass coverslip domains.

* Mesh:
‘Physics-controlled mesh’ was selected based on free tetrahedral physics with a normal element size.

* Study:
We calculate the temperature for different laser intensities and different light absorption coefficients at one run under Study/Parametric sweep where parameter names and values (for instance, laser intensity: ‘laserInt’ and gold film absorption at 488 nm: ‘goldAbs488’) can be set.

* Results:

1- The maximum temperature value in the ice layer under: Results/More Derived Values/Volume maximum is considered to assess the devitrification laser intensity.

2- To interpret the temperature distributions, one can define the desired directions/lines under: Results/Cut Line 3D. Secondly, the temperature distribution can be plotted against the defined lines under: Results/1D plot groups/Line Graph.


 

