# Slide notes

## 1

* Each year our knowledge of the gravity field has been getting better and better
* Coverage is almost uniform with satellite data from GRACE and GOCE
* This enables large-scale interpretations even in areas where data coverage
  was bad (like Brazil, most of Africa, oceans)
* We need to start adapting modeling and inversion from Cartesian coordinates
  (usually uses rectangular prisms) to spherical coordinates using spherical
  prisms (tesseroids)

## 2

* To my knowledge the only inversion method using tesseroids is the one by
  Chaves and Ussami (2013)
* They invert geoid height anomalies in a space domain formulation
* Gravity inversion is notoriously BAD-behaved
* It requires a lot of regularization with depth-weighting so that the
  solution doesn't always stick to the surface)
* Chaves and Ussami use depth-weighted minimum volume regularization
* and also a similarity constraint to a previous solution, which in their
  paper came from a seismic tomography

## 3

* From our part, I'm working on the adaptation of one of our inversion methods
  for tesseroids
* The method is called "planting anomalous densities" and was published by us
  in 2012

## 4

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

## 5 - 17

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

## 18

* The best way to test a new method is to run it on synthetic data
* This way we can analyse possible applications, advantages and shortcomings
* For this, I looked at some results from the literature and made some very
  simple models based on them to see if what kinds of sources I could recover
  and how well

## 19

* The first model I'll use is of a lineament in the crust composed of dense
  rocks
* This is inspired by the model of the Chad lineament, in Africa, by
  Braitenberg et al (2011)

## 20

* This is the Bouguer anomaly map, highlighted by the black arrows is the Chad
  lineament anomaly that is composed of two "threads"

## 21

* And this is a model proposed by the authors for a possible cause of the Chad
  anomaly as a dense and elongated tesseroid at 1km depth

## 22

* Here is the model I made inspired by the Braitenberg et al model
* It is composed of two elongated bodies
* Both are 10 degrees long, 0.5 degrees wide, and 8 km thick
* The density contrast is 300 kg.m-3 and the top is at 1km depth

## 23

* I used that model to generate noisy gzz data at 20km height

## 24

* As you'll recall, I need to provide seeds to start my inversion
* In this case, I used one seed per body, located at the top and with the
  correct density contrast
* This choice of seeds symbolises that I know the top of the source

## 25

* I ran the inversion using those seeds
* As you can see, the inversion is able to perfectly fit the noisy data

## 26

* And this is the solution I obtained shown in blue
* The red lines are the contours of the true model
* The inversion is able to correctly estimate the geometry of the source
* The top of the body is estimated correctly in most places
* It is also able to separate between the two where they become close

## 27

* What happens if I increase the height to 120 km?

## 28

* This is the gzz field at 120km
* Notice from that the data it is not possible to distinguish between the two
  lineaments

## 29

* Once again the inversion fits the data within the error limits

## 30

* This is the results we get, compared to the one obtained for 20km height
* The inversion underestimates the depth of the sources
* It is no longer able to distinguish between the two lineaments
* However, it resembles the general shape of the true sources

## 31

* What if we increase the height even further to 270km?

## 32

* This is the gzz observed at 270 km

## 33

* You can see that the result is even worse than at 270km
* The inversion completely misses the bend in the southern part of the source
  to the right and underestimates the top

## 34

* Now lets consider another model, this time of a magmatic underplating
  (or a somehow denser lower crust)
* This is based on the model proposed by Mariani et al for the Parana Basin in
  Southern Brazil

## 35

* This is the Bouguer anomaly for the Parana basin region, corrected for the
  Moho and sediments
* You can see a positive residual anomaly over the basin
* This is explained by the authors as a magmatic underplating resulting from
  the flood basalts of the Serra Geral formation
* Taking a look at their inversion result for the a-a' profile

## 36

* They tested three different reference levels and obtained the thickness of
  the underplating

## 37

* So I made a simple model based on this solution
* The model is 10 x 5 degrees and 15 km thick
* The top is at 30km and the density contrast is 200 kg.m-3

## 38

* This is the gzz field calculated at 250km altitude and noise corrupted

## 39

* Again, the seed used to start the inversion was located at the top and has
  the correct density contrast

## 40

* This is the result I get after running the inversion
* Notice that it fits the data and recovers a slightly smoothed version of the
  true model

## 41

* But what happens if I use the wrong the density?
* In reality there would be no way to know the exact value of the density
* So what I want to test here is how sensitive is the result to the given
  density

## 42

* On the top, is the result I get if I assign a higher density to the initial
  seed
* And on the bottom, if I assign a lower density
* As you can see, the effect is merely a thickening or thinning of the estimate
* The overall relief is maintained
* This is something that is know to happen in traditional non-linear inversions
  and this is just to show that the same thing happens here

## 43-44-45

* In conclusion, I have adapted the inversion method of planting anomalous
  densities for tesseroids

## 46

* The tests on synthetic data show for what types of geometries this inversion
  works well
* Lineaments, flat slabs, and plumes work well
* What still doesn't work well are dipping models, for example a subducting
  slab
* I'm still trying to come up with a clever trick to make those work

## 47

* Height matters, specially for crustal structure
* So calculate your data as close as possible
* But not too close because the tesseroid forward modeling becomes slow

## 48

* Missing the density contrast doesn't affect the general geometry of the
  solution
* One way to overcome the restraint of having to know the density is to test
  different values and see which solution agrees more with other data

## 49

* What I'm working on for the future is testing different combinations of
  tensor components to see if/how they impact the inversion
* Find a way to make dipping models work
* Apply to this to real data


-------------------------------------------------------------------------------

## Extra

## 19

* The first model I used is of a hypothetical mantle plume
* I say hypothetical because I don't want to get into the mantle plume debate
* It is based on the one used for the synthetic data test in Chaves
  and Ussami (2013)

## 20

* They used this simple tesseroid model to  calculate a synthetic geoid height
  anomaly

## 21

* This is the model I'll use
* It is a bit different from the Chaves and Ussami one
* I created a sort of "plume head" that is 200km thick and 2x2 degrees wide
* Bellow it there is a 700km tail
* The top is at 100km depth and the density contrast is -50 kg.cm-3, which is
  the same used by Chaves and Ussami

## 22

* I used my plume model to produce synthetic noisy gzz data at 250km altitude
* I placed this model under Hawaii just for fun

## 23

* As you'll recall, I need to provide a seed to start my inversion
* For this case, I used a single seed placed at the top with the correct
  density contrast of -50

## 24

* Running the inversion I get the result in blue on the right
* As you can see, the inversion recovers the major characteristics of the model
* It underestimates the bottom depth a bit but getting the bottom right in
  gravity inversion is always difficult
* On the left, you can see that the estimate fits the data perfectly


