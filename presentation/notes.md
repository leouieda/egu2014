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

* The best way to test a new method is to run it on synthetic data
* This way we can analyse possible applications, advantages and shortcomings
* For this, I looked at some results from the literature and made some very
  simple models based on them to see if what kinds of sources I could recover
  and how well

# 19

* The first model I'll use is of a lineament in the crust composed of dense
  rocks
* This is inspired by the model of the Chad lineament, in Africa, by
  Braitenberg et al (2011)

# 20

* This is the Bouguer anomaly map, highlighted by the black arrows is the Chad
  lineament anomaly that is composed of two "threads"

# 21

* And this is a model proposed by the authors for a possible cause of the Chad
  anomaly as a dense and elongated tesseroid at 1km depth

# 22

* Here is the model I made inspired by the Braitenberg et al model
* It is composed of two elongated bodies
* Both are 10 degrees long, 0.5 degrees wide, and 8 km thick
* The density contrast is 300 kg.m-3 and the top is at 1km depth

# 23

* I used that model to generate noisy gzz data at 20km height

# 24

* As you'll recall, I need to provide seeds to start my inversion
* In this case, I used one seed per body, located at the top and with the
  correct density contrast
* This choice of seeds symbolises that I know the top of the source

# 25

* I ran the inversion using those seeds
* As you can see, the inversion is able to perfectly fit the noisy data

# 26

* And this is the solution I obtained shown in blue
* The red lines are the contours of the true model
* The inversion is able to correctly estimate the geometry of the source
* The top of the body is estimated correctly in most places
* It is also able to separate between the two where they become close


-------------------------------------------------------------------------------

# Extra

# 19

* The first model I used is of a hypothetical mantle plume
* I say hypothetical because I don't want to get into the mantle plume debate
* It is based on the one used for the synthetic data test in Chaves
  and Ussami (2013)

# 20

* They used this simple tesseroid model to  calculate a synthetic geoid height
  anomaly

# 21

* This is the model I'll use
* It is a bit different from the Chaves and Ussami one
* I created a sort of "plume head" that is 200km thick and 2x2 degrees wide
* Bellow it there is a 700km tail
* The top is at 100km depth and the density contrast is -50 kg.cm-3, which is
  the same used by Chaves and Ussami

# 22

* I used my plume model to produce synthetic noisy gzz data at 250km altitude
* I placed this model under Hawaii just for fun

# 23

* As you'll recall, I need to provide a seed to start my inversion
* For this case, I used a single seed placed at the top with the correct
  density contrast of -50

# 24

* Running the inversion I get the result in blue on the right
* As you can see, the inversion recovers the major characteristics of the model
* It underestimates the bottom depth a bit but getting the bottom right in
  gravity inversion is always difficult
* On the left, you can see that the estimate fits the data perfectly


