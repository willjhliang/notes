# Theory
NeRF is a model that creates a 3D scene from multiple images taken from different perspectives. In other words, given a bunch of images of an object, the network learns the color and density of the object at each coordinate in 3-dimensional space.

> Density controls how much light passes through a particular coordinate. This is crucial for transparent objects like colored glass.

The model generates the scene by outputting color and density for any given coordinate and viewing direction. We train by overfitting for a particular scene, and the final network predicts only for this scene.

## Volume Rendering
We can render an image of the scene using volume rendering, which finds the color of every pixel by projecting a ray $r$, then taking integral $$C(r) = \int_{t_n}^{t_f}T(t)\sigma(r(t))c(r(t), d)dt$$
where $T(t) = \exp\{-\int_{t_n}^t \sigma(r(s))ds\}$ computes how much light makes it to $t$ along the ray and $d$ is the direction (angles $\theta$ and $\phi$) of the ray. The integral is computed using quadratures in implementation.

This essentially simulates light going through the ray and finds the expected color based on the probability of light reaching each position on the ray.

# Model
The model is an [[✏️ Artificial Neural Network]] that takes in the positional data $(x, y, z, \theta, \phi)$ and outputs the color and density $(r, g, b, \sigma)$.

> In practice, the positional data is represented using positional encodings, which brings it to a higher dimension space and produces better results.

The complete system actually uses two networks, one coarse and one fine: the former gives a rough idea of the density along each ray, and the latter uses this information to sample areas that have the highest density. In doing so, we allocate more samples to regions that are more likely to be visible in the final result.

# Training
NeRFs train on the given images using the $L_2$ loss between coarse and fine network outputs and the actual pixel colors from an image.

# Prediction
To generate a particular view of the scene, we shoot a ray for every pixel and get the predicted color using volume rendering.