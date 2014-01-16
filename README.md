Talk proposal submitted to the European Geosciences Union General Assembly 2014

# Gravity inversion in spherical coordinates using tesseroids

**Leonardo Uieda and Valéria C. F. Barbosa**


Satellite observations of gravitational fields have provided geophysicists
with exceptionally dense and uniform coverage of data over vast areas.
This enables regional or global scale
high resolution geophysical investigations.
Techniques like forward modeling and inversion of gravity anomalies
are routinely used to investigate large geologic structures,
such as large igneous provinces, suture zones, intracratonic basins, and the
Moho.
Accurately modeling such large structures
requires taking the sphericity of the Earth into account.
A reasonable approximation is to assume a spherical Earth and
use spherical coordinates.

In recent years, efforts have been made
to advance forward modeling in spherical coordinates using tesseroids,
particularly with respect to speed and accuracy.
Conversely, traditional space domain inverse modeling methods
have not yet been adapted to use spherical coordinates and tesseroids.
In the literature there are a range of inversion methods
that have been developed for Cartesian coordinates and right rectangular prisms.
These include methods for estimating the relief of an interface,
like the Moho or the basement of a sedimentary basin.
Another category includes methods
to estimate the density distribution in a medium.
The latter apply many algorithms to solve the inverse problem,
ranging from analytic solutions to random search methods
as well as systematic search methods.

We present an adaptation for tesseroids of the systematic search method
of "planting anomalous densities".
This method can be used to estimate the geometry of geologic structures.
As prior information, it requires knowledge of the approximate densities and
positions of the structures.
The main advantage of this method is its computational efficiency,
requiring little computer memory and processing time.
We demonstrate the shortcomings and capabilities of this approach using
applications to synthetic and field data.
Performing the inversion of gravity and gravity gradient data,
simultaneously or separately,
is straight forward and requires no changes to the existing algorithm.
Such feature makes it ideal for inverting
the multicomponent gravity gradient data from the GOCE satellite.

An implementation of our adaptation is freely available
in the open-source modeling and inversion package Fatiando a Terra
(http://www.fatiando.org).
