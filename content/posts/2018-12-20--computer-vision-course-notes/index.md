---
title: Computer Vision Course Notes
category: "notes"
cover: cv_thumbnail.jpg
---


linear filters allow you to perform the operations to arrive to an aggregate filter kernel instead of applying multiple filters separately.

correlation — take the first tile straight.
convolution — is the 180 degrees rotation, both up and down, right and left.

normalized correlation — make a chunk of the image as a filter, normalize it to standard deviation of 1. when applied to the image, where that chunk is detected the value is the highest.

filters as templates — take masked kernel template and do normalized correlation on an image, the brightest spot would show where the template is the most matching.

partial derivative — derivative with respect to one variable in a multivariate function.

gradient of image — composed of derivatives in x and y direction.

the gradient points in the direction of most rapid increase in intensity.

correlation vs convolution — convolution tends to flip the order.

linearity of functions allows you to apply derivative function on the filter then only perform one convolution, saving an operation.

take the derivative of operator then apply operator to image.

laplacian filter is used for second derivative.

a parametric model can represent a class of instances where each is defined by the values of its parameters.

hough transform main idea
- each edge point votes for compatible lines.
- look for lines that get many votes.

hough space
- using the remaining parameters (usually constants) in a function as the basis for a space.
- a line in image space corresponds to a point in hough space.
- a point in hough space corresponds to a line in hough space.

hough transform logic
- all points in image space corresponding to lines in hough space.
- the bin in hough space with the most line intersections is a successfully voted line.

polar representation of line
- d: perpendicular distance from line to origin.
- theta: angle the perpendicular makes with x-axis.

non-analytic models — parameters express variation in pose or scale of fixed but arbitrary shape.

visual code-word based features — not edges but detected templates learned from models now.

frequency analysis — any image can be decomposed to a set of features that describe it.

basis set — a basis set of a vector space V is linearly independent subset of V that spans V

Fourier transform — represent the image as an infinite weighted sum of an infinite number of sinusoids.

power is usually mentioned when talking about the presence of frequency in signal or image.

aliasing — signals ‘traveling in disguise’ as other frequencies, as the number of sample size we take aren’t sufficient to differentiate the between high and low frequencies.

antialiasing — should be done when you are down sampling the image to prevent inaccurate representation and preserve variation.

image capturing system — a system that captures light projected into a sensor.

you can calculate the ideal distance between target and the sensor to have the camera capture the entire field of vision of the target.

affine transform — translate, rotate, and skew an image, 6 degrees of freedom, requires 3 pairs of points to calculate matrix

homography — can be used to rectify an image to achieve a square expected view of one aspect of the image; requires 4 pairs of points to calculate.

calibrated cameras — a relationship between two cameras, as in you know how to get to the other camera given your have one camera and calibration variables.

features — reliably detectable points that can be found in other images, found precisely - well localized, found reliably - well matched.

good features
- repeatability and precision
    - the same feature can be found in several images despite geometric and photometric transformations.
- compactness and efficiency
    - fewer features than image pixels.
- locality
    - a feature occupies a relatively small area of the image; robust to clutter and occlusion.

corners — have gradients in all directions, any shift in any direction would lead to a detectable change.

harris corners 
- invariant to rotationl 
- mostly invariant to additive and multiplicative intensity changes.
- not invariant to scale, depends on degree.

scale independent corner detectors
- SIFT
- harris-laplacian

descriptor — description of the neighborhood where the interest point is that is going to allow us to match.

SIFT — scale invariant feature transform
- invariant to translation, rotation, scale and other image parameters.

SIFT procedure
- scale space extrema detection
- key point localization
- (or use harris Laplace or other methods)
- orientation assignment
- key point description
    - histogram
    - projection of the dominant direction
    - 128 histogram number

RANSAC — random sample consensus, randomly pick some points to define your line (model). Repeat enough times until you find a good line (model) - on with many inliers.

General RANSAC algorithm:
- randomly select s points (or point pairs) to form a sample
- instantiate the model
- get a consensus set C_i - the points within error bounds (distance threshold) of the model
- if |C_i| > T, terminate and return model
- repeat for N trials, return the model with max |C_i|

transforms — points requires
- 1 for translations
- 2 for similarity
- 3 for affine
- 4 for homography

RANSAC PROs
- simple and general
- applicable to many different problems, often works well in practice
- robust to a large number of outliers
- applicable for large number of parameters than hough transform

RANSAC CONs
- computational time grows quickly with the number of model parameters
- not as good for getting multiple fits
- really not good for approximate models

RANSAC applications
- computing a homography (image stitching) or other image transform
- estimating fundemental matrix (relating two views)
- pretty much every problem in robot vision

irradiance — light per unit area incident on a surface, the stuff landing on surface.

radiance — light from the surface reflected in a given direction, within a given solid angle, the stuff coming out of light source.

diffuse reflection — the most light is reflected perpendicular to the the surface and it falls off as it is more parallel to the surface, but it appears equally bright from all directions.

gloss vs reflection
- reflection is that all light rays are flecked exactly along the same angle ray.
- gloss means that there exists a some spread along this angle that is correlated to the level of glossiness.

optical flow is the apparent motion of objects or surfaces.

Lucas Kanade -> calculate flow or moment for every point on image, can be applied hierarchal by downsampling to capture longer variations of motion.

Lucas Kanade errors — the motion is large (larger than a pixel) - Taylor doesn’t hold.

difference of gaussians is approximately laplacian.

apply Lucas Kanade & good features to track.

Shi-Tomasi feature tracker & good features to track.

tracking — prediction of new state based on the current state to make it easier to detect the same object in the future frame, focus in on an area to focus.

tracking with dynamics — have a model of motion and able to update that model.

linear dynamics model 
- state undergoes linear transformation plus guardian noise.
- you have the power to design the model.

kalman filter
- method of tracking linear dynamic systems with gaussian noise
- only maintaining means and variances 
- general steps: shift->expand->measure->correct->shrink
- slave to the model specified
- PROs
    - simple updates, compact, and efficient
- CONs
    - unimodal distribution, only single hypothesis
    - restricted class of motions defined by linear models

bayes filter
- model prediction based on current input and previous states
- bayes rule

particle filters
- use particle densities to model a distribution instead of just mean and variance.

color distribution — what are good ways track it — mean shift filtering.

mean shift object tracking 
- keep track of region
- use quantized color space of color distribution in that region to describe it 
- think of region as gaussian kernel, which is differentiable and allows you to follow along the gradient to predict where to move next.

tracking issues
- initialization
    - manual
    - background subtraction
    - detection
- obtaining observations and dynamic models
    - dynamic model: learn from real data (pretty difficult), learn from clean data (easier), or specify using domain knowledge.
    - generative observation model: have some sort of ground truth.
- prediction vs correction
    - if dynamic models are too strong will end up ignoring data
- data association
    - clutter
    - determine which measurement goes with which track
- drift
    - sticks to model too much
    - how much to change model or how much to stay

supervised classification — two general strategies:
- use training data to build representative probability models; separately model class condition densities and priors (generative) — model the class.
- directly construct a good decision boundary, model the posterior (discriminative) — model the decision.

generative model
- PROS
    - pure probability
    - allows you to use prior knowledge
    - parametric modeling of likelihood permits using a small number of examples
    - new classes do not perturb previous models
    - can be used to generate data
    - can take advantage of unlabeled data
- CONS
    - where do we get the priors
    - why model not-C points
    - lots of data doesn’t help
    - the hard example cases aren’t special

principle component analysis
- principle components are all about the directions in the feature space along which points have the greatest variance.
- the first principle component is the direction of maximum variance.
- subsequent principle components are orthogonal to previous principle components and describe maximum residual variance.
- limitations
    - global appearance method not robust to misalignment, background variation.
    - the direction of maximum variance is not always good for classification. 

boosting
- weighted training examples
- adjust those weights
- come up with final classifier which is a linear combination of weak learners.

haar features
- simple summation of rectangles and differences of those areas across the image
- similar to convolutional kernels
- A Haar-like feature considers adjacent rectangular regions at a specific location in a detection window, sums up the pixel intensities in each region and calculates the difference between these sums. This difference is then used to categorize subsections of an image. 

boosting advantages
- integrates classification with feature selection 
- flexibility in choice of weak learners, boosting scheme
- complexity of training is linear in the number of training examples
- testing is fast
- easy to implement

boosting disadvantages
- needs lots of training examples
- often found to not work as well as an alternative discriminative classifier, support vector machine (SVM)
    - especially for many classes

support vector machine
- discriminative classifier based on optimal departing line
- maximize the margin 

support vectors are the points closes to to the separation boundary that determine the margin and subsequently margin.

use kernel trick to map every data point into high dimensional space via some transformation.

kernel function — a ‘similarity’ function that corresponds to an inner product in some expanded feature space.

SVM for recognition
1. define your representation
2. select a kernel function
3. compute a pairwise kernel values between labeled examples
4. use this ‘kernel matrix’ to solve for SVM sport vectors & weights

multi-class SVMs
- combine a number of binary classifiers
- one vs all
    - training: learn an SVM for each class vs the rest 
    - testing: apply each SVM to test example and assign to it the class of the SVM that returns the highest decision value
- one vs one
    - training: learn an SVM for each pair of classes
    - testing: each learned SVM ‘votes’ for a class to be assigned to the test example

SVM PROs
- many publicly available SVM packages
- kernel based framework is very powerful, flexible
- often a sparse set of support vectors — compact when testing
- works very well in practice, even with very small training sample sizes

common SVM kernels
- linear (no kernel)
- gaussian
- histogram intersection kernel

SVM CONs
- no direct multi class SVM, must combine two-class SVMs
- can be tricky to select best kernel function for a problem 
- nobody writes their own SVMs
- computation, memory
    - during training time, must compute matrix of kernel values for every pair of examples
    - learning can take a very long time for large scale problems

Random forrest method is good to know

visual words
- quantization, index, bags of words

bag of visual words
- summarize entire image based on distribution (histogram) of word occurrence
- analogous to bag of words representation commonly used for documents

background subtraction options
- bg is last frame
- mean filtering 
    - bg is mean of last n frames
- median filtering 
    - bg is median of last n frames

background subtraction PROs
- extremely easy to implement and use
- all pretty fast
- corresponding background models need not be constant, they change over time

background subtraction CONs
- accuracy of frame differencing depends on object speeds and frame rate
- median background model - relatively high background memory requirements 
- setting the global threshold TH

image moments — distribution of image pixels

Hu moments — rotation, translation, scale invariant image moments.

first order Markovian — probability of moving to a given state depends only on the current state.

ingredients of a Markov model
- states
- state transition probabilities
- initial state distribution 

hidden Markov model
- cannot observe the state
- observables are only indicators or evidence of the state
- emission probabilities — symbols being spit out given a probability state
- look for likelihood of seeing a sequence of observations

specification of an HMM
- N — number of states
    - S — set of states
    - Q — sequence of states
- A — state transition matrix
- B — observation probability distribution
- pi — the initial state distribution

given some sequence of observations, what ‘model’ generated those?

HMMs: 
- generative probabilistic models of time series (with hidden state)
- Forward-Backward: algorithm for computing probabilities over hidden states
    - given the forward backward algorithms you can train the models
- best known methods in speech, computer vision, robotics, though for really big data conditional random fields are winning 

HMMs PROs:
- a learning paradigm that acquires spatial and temporal models and does some amount of future selection
- recognition is fast; training is not so fast but not too bad

HMMs CONs:
- not great for on the fly labeling — e.g. segmentation of input streams. requires lots of data for that — much like language
- works well when problem is easy. less clear other times.

Hue — the shade of the color, represent in angle [0, 360], it wraps around
Saturation — the more saturated, the more pure the color
Value — how light a value is

location in color pace to segment out image

in RGB space
- when colors get darker or when colors get brighter, the RGB values each get closer

human eyes are more sensitive to luminance than color — YUV contains variations that are more of a representation for the Y luminance channel.

segmentation — splicing image into different parts.

clustering — choose ‘center’ as representative intensities, label rest of the pixels according to which of these centers it is closest to. 

K-means clustering: algorithm
1. randomly initialize cluster centers c_1, …, c_k
2. determine points in each cluster:
    * for each point p, ring the closes c_i; put p into cluster i
3. given points in each cluster, solve for c_i:
    * set c_i to be the mean of the points in cluster i
4. if any c_i has changed, repeat step 2

segmentation as clustering 
- depending on what we choose as the feature space, we can group pixels in different ways.
- grouping pixels based on intensity + position similarity

K-means
- PROs
    - very simple method
    - converges to a local minimum of the error function
- CONs
    - memory intensive
    - need to pick k
    - sensitive to initialization
    - sensitive to outliers
    - only finds ’spherical’ clusters, doesn’t want any point to be too far away

mean shift clustering
- the mean shift algorithm seeks modes or local maxima of density in the feature space.
- cluster: all data points in the attraction basin of a mode.
- attraction basin:  the region for which all trajectories lead to the same mode.
- PROs
    - automatically finds basins of attraction
    - one parameter choice (window size)
    - does not assume (image) shape on clusters
    - generic technique
    - find multiple modes
- CONs
    - selection of window size
    - does not scale well with dimension of feature space

texture features
- find ‘textons’ by clustering vectors of filter bank outputs
- describe texture in a window based on its texton histogram
- textons are small filter outputs of a given filter applied to a small area of the image

images as graphs
- pixels are the nodes
- edges represent affinity, how similar 
- can segment graph by breaking image into segments
    - delete links between segments
    - easier to delete low affinity edges
- similar pixels in same segment and vice versa

normalized cut
- PROs
    - generic framework
        - flexible to choice of function that computes weights (‘affinities’) between nodes
    - does not require model of the data distribution
- CONs
    - time complexity can be high
        - dense, highly connected graphs
            - many affinity computations
        - solving eigenvalue problem
    - preference for balanced partitions

OTSU’s method for thresholding
- assume your distribution is bimodal and find best threshold

connected components analysis — labels image into components 
 
dilation — expands the connected sets of 1s in binary image
- grow features
- filling holes and gaps

erosion — shrinks  the connected sets of 1s of a binary image
- shrinking features
- removing bridges, branches, protrusion

opening — erosion followed by dilation
- the union of all translations of B that fit entirely within A
- the area we can paint when the brush has a foot print B and we are not allowed to paint outside A
- idempotent: repeated operations has no further effects
- smooth contours 
- break thin connections
- eliminate small islands
- eliminates sharp peaks

closing — dilation followed by erosion
- the complement of all translations of B that do not overlap A
- the area we cannot paint when the brush has a foot print B and we are not allowed to paint inside A
- idempotent: repeated operations has no further effects
- smooth contours at the concavities
- fuse narrow breaks 
- fill in gulfs

opening followed by closing 

boundary extraction 
- object subtracted by the eroded version of it

thinning 
- keep applying to image until you are left with a one pixel wide image
- thickening — vice versa

haar cascade classifier
- purpose is to detection tiles within a frame of the video
- invariant to brightness, color, size, and position of object to be detected
- training takes substantial resources and samples
- implementation details (maybe applicable)
    - median blurring 
    - canny edge detection 
    - find contours

cascade classifiers
- concatenation of a set of weak classifiers used to create a strong classifier
- boosting



