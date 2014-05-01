# 1

* Each year our knowledge of the gravity field has been getting better and better
* Coverage is almost uniform with satellite data from GRACE and GOCE
* This enables large-scale interpretations even in areas where data coverage
  was bad (like Brazil, most of Africa, oceans)
* We need to start adapting modeling and inversion from Cartesian coordinates
  (usually uses rectangular prisms) to spherical coordinates using spherical
  prisms (tesseroids)

# 2

* To my knowledge the only inversion method using tesseroids is the one by
  Chaves and Ussami (2013)
* They invert geoid height anomalies in a space domain formulation
* Gravity inversion is notoriously BAD-behaved
* It requires a lot of regularization with depth-weighting so that the
  solution doesn't always stick to the surface)
* Chaves and Ussami use depth-weighted minimum volume regularization
* and also a similarity constraint to a previous solution, which in their
  paper came from a seismic tomography

# 3

* From our part, I'm working on the adaptation of one of our inversion methods
  for tesseroids
* The method is called "planting anomalous densities" and was published by us
  in 2012

# 4

* This is also a space domain formulation, and it was designed for
  multicomponent data
* This means that it can be used with the gravity anomaly, gravity gradients,
  and any combination of them
* It is not a "conventional" inversion in the sense that instead of solving a
  regularized least-squares problem, it uses a "growth" algorithm to build a
  solution from a starting seed
* The advantage of this approach is that it does not involve the solution of
  linear systems
* We can also compute the sensitivity matrix very efficiently
* We actually don't need to compute and store the whole matrix at any time
* This makes the algorithm very fast
* Just to give an example, the largest inversion we ever ran involved 10s of
  thousands of data points and ~1 million parameters. That took about 1h to
  compute in a standard laptop computer.
* All examples I'll show next ran in only a few seconds

# 5 - 17

* To illustrate how this inversion works, I'll walk through a simple example
  with synthetic data
* On top we have the synthetic data that was caused by the red block in the
  bottom
* The inversion starts with one or more seeds given by the user
* The seeds are prisms selected from the mesh that are assigned a target density
* In the middle is the predicted data
* The algorithm then looks at the neighboring elements of the seed (shown here
  in black lines) and chooses one for accretion to the solution
* By successively doing this, the solution grows from the starting seed until
  it is able to fit the observed data

# 18




