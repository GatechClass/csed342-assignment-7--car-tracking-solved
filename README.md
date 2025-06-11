# csed342-assignment-7--car-tracking-solved
**TO GET THIS SOLUTION VISIT:** [CSED342 Assignment 7- Car Tracking Solved](https://mantutor.com/product/csed342-assignment-7-car-tracking-solved-2/)


---

**For Custom/Order Solutions:** **Email:** mantutorcodes@gmail.com  

*We deliver quick, professional, and affordable assignment help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;114113&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;1&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (1 vote)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CSED342  Assignment 7- Car Tracking Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (1 vote)    </div>
    </div>
General Instructions

You should write both types of answers in submission.py between

# BEGIN_YOUR_ANSWER and

# END_YOUR_ANSWER

You can implement other helper functions outside the answer block if you want, but must not add other libraries. Do not make changes to files other than submission.py.

Your code will be evaluated on two types of test cases, basic and hidden, which you can see in grader.py. Basic tests, which are fully provided to you, do not stress your code with large inputs or tricky corner cases. Hidden tests are more complex and do stress your code. The inputs of hidden tests are provided in grader.py, but the correct outputs are not. To run all the tests, type

python grader.py

This will tell you only whether you passed the basic tests. On the hidden tests, the script will alert you if your code takes too long or crashes, but does not say whether you got the correct output. You can also run a single test (e.g., 2a-0-basic) by typing

python grader.py 3a-0-basic

We strongly encourage you to read and understand the test cases, create your own test cases, and not just blindly run grader.py.

$ conda create -n assn7 python=3.9

$ conda activate assn7

Introduction

This assignment is a modified version of the Driverless Car assignment written by Chris Piech.

A study by the World Health Organisation found that road accidents kill a shocking 1.24 million people a year worldwide. In response, there has been great interest in developing autonomous driving technology that can drive with calculated precision and reduce this death toll. Building an autonomous driving system is an incredibly complex endeavor. In this assignment, you will focus on the sensing system, which allows us to track other cars based on noisy sensor readings.

Getting started. Let’s start by trying to drive manually:

python drive.py -l lombard -i none

You can steer by either using the arrow keys (↑, ←, →) or ’w’, ’a’, and ’d, and quit drive.py by using ’q’. Note that you cannot reverse the car or turn in place. Your goal is to drive from the start to finish (the green box) without getting in an accident. How well can you do on crooked Lombard street without knowing the location of other cars? Don’t worry if you aren’t very good; the staff was only able to get to the finish line 4/10 times. This 60% accident rate is pretty abysmal, which is why we’re going to build an AI to do this.

Flags for python drive.py:

• -a: Enable autonomous driving (as opposed to manual).

• -i &lt;inference method&gt;: Use none, exactInference, particleFilter to (approximately) compute the belief distributions.

• -l&lt;map&gt;: Use this map (e.g. small or lombard). Defaults to small.

• -d: Debug by showing all the cars on the map.

• -p: All other cars remain parked (so that they don’t move).

Modeling car locations. We assume that the world is a two-dimensional rectangular grid on which your car and K other cars reside. At each time step t, your car gets a noisy estimate of the distance to each of the cars. As a simplifying assumption, we assume that each of the K other cars moves independently and that the noise in sensor readings for each car is also independent. Therefore, in the following, we will reason about each car independently (notationally, we will assume there is just one other car).

At each time step t, let Ct ∈ R2 be a pair of coordinates representing the actual location of the single other car (which is unobserved). We assume there is a local conditional distribution p(ct | ct−1) which governs the car’s movement. Let at ∈ R2 be your car’s position, which you observe and also control. To minimize costs, we use a simple sensing system based on a microphone. The microphone provides us with Dt, which is a Gaussian random variable with mean equal to the distance between your car and the other car and variance σ2 (in the code, σ is Const.SONAR_STD, which is about two-thirds the length of a car). In symbols,

Dt ∼ N(∥at − Ct∥,σ2). (1)

For example, if your car is at at = (1,3) and the other car is at Ct = (4,7), then the actual distance is 5 and Dt might be 4.6 or 5.2, etc. Use util.pdf(mean, std, value) to compute the probability density function (PDF) of a Gaussian with given mean and standard deviation, evaluated at value. Note that the PDF does not return a probability (densities can exceed 1), but for the purposes of this assignment, you can get away with treating it like a probability. The Gaussian probability density function for the noisy distance observation Dt, which is centered around your distance to the car µ = ∥at − Ct∥:

The figure below shows another example where one black car and our (orange) car are located in the 2D grid and the sensor estimates the distances of the black car from our car. Note that we can access the information of distances (Dt) measured by the sensor, but we’re not provided with the exact locations (Ct) of the black car.

Theory. Here’s what the Bayesian network (it’s an HMM, in fact) for car tracking looks like:

p(ct | d1:t) = p(ct | d1:t−1,dt)

∝ p(dt | d1:t−1,ct)p(ct | d1:t−1) (∵ Bayes rule)

= p(dt | ct)p(ct | d1:t−1), (∵ Markov model/independence)

and

p(ct | d1:t−1) = Xp(ct,ct−1 | d1:t−1)

ct−1

= Xp(ct | ct−1,d1:t−1)p(ct−1 | d1:t−1) (∵ Conditional prob.)

ct−1

= Xp(ct | ct−1)p(ct−1 | d1:t−1), (∵ Markov model/independence)

ct−1

where d1:t is also the observations from 1 to t time steps. We can see that p(ct | d1:t) is defined recursively over time. The following problems can be solved with this idea.

Your job is to implement a car tracker that (approximately) computes the posterior distribution P(Ct | D1:t = d1:t) (your beliefs of where the other car is) and update it for each t = 1,2,…. We will take care of using this information to actual drive the car (i.e., set at as to avoid collision with ct), so you don’t have to worry about that part.

To simplify things, we will discretize the world into tiles represented by (row, col) pairs, where 0 ≤ row &lt; numRows and 0 ≤ col &lt; numCols. For each tile, we store a probability distribution whose values can be accessed by self.belief.getProb(row, col). To convert from a tile to a location, use util.rowToY(row) and util.colToX(col).

In Problem 1, you will warm up to a more simplified problem. In Problems 2 and 3, you will implement ExactInference, which computes a full distribution over tiles (row, col). In Problem 4, you will implement ParticleFilter, which works with particle-based representation of this distribution.

Problem 1: Simplification

Before we start implementing car tracking, let us look at a simplified version of the car tracking problem.

Problem 1a [4 points]

For this problem only, let Ct ∈ {0,1} be the actual location of the car, and Dt ∈ {0,1} be a sensor reading for the location of that car measured at time t. The distribution over the initial car position c1 ∈ {0,1} is defined as:

.

The following local conditional distribution governs the movement of the car (with probability ϵ, the car moves). For each t,

.

The following local conditional distribution governs the noise in the sensor reading (with probability η, the sensor reports the wrong position). For each t,

( p(dt | ct) = η if dt ̸= ct

1 − η if dt = ct.

We have obtained sensor readings by time t, D1:t = d1:t, (D1 = d1,D2 = d2,…,Dt = dt). Implement all necessary methods for ConditionalProb class in submission.py to compute the posterior distribution P(Ct = ct | D1:t).

Problem 2: Emission Probabilities

In this problem, we assume that the other car is stationary (e.g., Ct = Ct−1 for all time steps t). You will implement a function observe that upon observing a new distance measurement Dt = dt updates the current posterior probability from

P(Ct | D1 = d1,…,Dt−1 = dt−1)

to

P(Ct | D1 = d1,…,Dt = dt) ∝ P(Ct | D1 = d1,…,Dt−1 = dt−1)p(dt | ct), where we have multiplied in the emission probabilities p(dt | ct) described earlier. The current posterior probability is stored as self.belief in ExactInference, which you should update self.belief in place.

Problem 2a [4 points]

Fill in the observe method in the ExactInference class of submission.py. This method should update the posterior probability of each tile given the observed noisy distance. After you’re done, you should be able to find the stationary car by driving around it (-p means cars don’t move): Notes: • You can start driving with exact inference now. python drive.py -a -p -d -k 1 -i exactInference You can also turn off -a to drive manually.

• Remember to normalize the updated posterior probability (see useful functions provided in util.py).

• On the small map, the autonomous driver will sometimes drive in circles around the middle block before heading for the target area. In general, don’t worry too much about driving the car. Instead, focus on if your car tracker correctly infers the location of other cars.

• Don’t worry if your car crashes once in a while! Accidents do happen, whether you are human or AI. However, even if there was an accident, your driver should have been aware that there was a high probability that another car was in the area.

Problem 3: Transition Probabilities

Now, let’s consider the case where the other car is moving according to transition probabilities p(ct+1 | ct). We have provided the transition probabilities for you in self.transProb. Specifically, self.transProb[(oldTile, newTile)] is the probability of the other car being in newTile at time step t + 1 given that it was in oldTile at time step t.

In this part, you will implement a function elapseTime that updates the posterior probability about the location of the car at a current time t

P(Ct = ct | D1 = d1,…,Dt = dt)

to the next time step t + 1 conditioned on the same evidence, via the recurrence:

.

Again, the posterior probability is stored as self.belief in ExactInference.

Problem 3a [4 points]

Finish ExactInference by implementing the elapseTime method. When you are all done, you should be able to track a moving car well enough to drive autonomously:

python drive.py -a -d -k 1 -i exactInference Notes:

• You can also drive autonomously in the presence of more than one car: python drive.py -a -d -k 3 -i exactInference

• You can also drive down Lombard: python drive.py -a -d -k 3 -i exactInference -l lombard

Problem 4: Particle Filtering

Though exact inference works well for the small maps, it wastes a lot of effort computing probabilities for cars being on unlikely tiles. We can solve this problem using a particle filter which has complexity linear in the number of particles rather than linear in the number of tiles. Implement all necessary methods for the ParticleFilter class in submission.py. When complete, you should be able to track cars nearly as effectively as with exact inference.

Problem 4a [6 points]

Some of the code has been provided for you. For example, the particles have already been initialized randomly. You need to fill in the observe and elapseTime functions. These should modify self.particles, which is a map from tiles (row, col) to the number of times that particle occurs, and self.belief, which needs to be updated after you resample the particles.

You should use the same transition probabilities as in exact inference. The belief distribution generated by a particle filter is expected to look noisier compared to the one obtained by exact inference.

python drive.py -a -i particleFilter -l lombard

To debug, you might want to start with the parked car flag (-p) and the display car flag

(-d).
