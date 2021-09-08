## 1. Why did you use padding?
For the below 2 mentioned points, a single method could be used with a small tweak. hence the parameter padding was used.

- In the paper, for point aggregator if the point reached an edge then it could either move from left to right or from top to bottom of edge and vice versa.
- While checking if the point is attaching to another point, the adjacent positions needed to be looked upon.
	
## 2. In def_get_random_pos - it will find any random empty cell in the matrix.. why not consider the position among adjacent cells
- get_random_pos() is invoked after a point has successfully attached itself to another point.
- get_adjacent_points() id invoked during a random walk.
The probabilty of a point getting selected near to an adjacent point of the existing structure is same as getting selected from the farthest region of the structure in point aggregator. So a random position was selected.

## 3. first start point should be from the boundaries?
The code implementation was for only point aggregator, and according to the paper it has to be center of the matrix.

## 4. data = scaler.fit_transform(dataset) --- should you also transform target variable??
Theoritically transforming the feature+target together causes no concern, At the end it needs to be converted to its inverse form. But development in such a way is not efficient. The target variable needs to be transformed with another scaler object separately.

In this case, target variable is already in the range of 0 to 1. So this could have been avoided.

## 5. What is a more optimized way to make a random walk?
I have thought of trying 3 approaches for this.
- Reduce the exploration space for the walk by marking visited or not visited
- find radii of all adjacent points with the center and choose the smaller one.
- Use Monte carlo markov chain approach to select a point from the distribution such that its dependent upon the previous step.

I didn't had any success to the MCMC approach.

## 6. How is the dependencies on filter size and number of points
Instead of looking at the full matrix and then try to estimate the stikiness paramter, we are looking at an area that covers the most of the points. Here I have selected 60% of the area around origin.
And so the number of points within that area is an important information to be considered.

## 7. Given a matrix to estimate stickiness - how would you consider Crowd density of points?
Crowd density was calculated using the surface area captured by the points to the total area of the matrix. Doing simulations and in paper it was observed that decreasing the stickiness increased the crowd density of the points.