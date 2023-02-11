# Theory
The key idea behind diffusion is to destroy images through gaussian noise, then learn a  way to reverse time and recreate the original image. If we successfully learn such a model, then we can generate any picture from random noise.

Diffusion models destroy the training distribution of images $q(x)$ by repeatedly applying gaussian noise for $T$ time-steps, known as the forward process. $x_t$ represents the distribution after applying noise for $t$ steps; $x_0$ is the original image, and $x_T$ is isotropic noise. The forward process equation is $$q(x_t \vert x_{t-1}) = \mathcal{N}(\sqrt{1-\beta_t} x_{t-1}, \beta_t \mathbf{I})$$
where $\beta_t$ is controlled by a variance schedule, which dictates how much noise to add at every time step $t$. $\beta_t$ usually increases as $t$ increases.

Since we're applying gaussians, we can compute $x_t$ directly from $x_0$. Let $\alpha_t = 1 - \beta_t$ and all $\epsilon \sim \mathcal{N}(0, \mathbf{I})$, and observe that $x_t$ can be expressed in terms of $x_{t-2}$. $$\begin{align}x_t &= \sqrt{\alpha_t}x_{t-1} + \sqrt{1-\alpha_t}\epsilon_{t-1} \\ &= \sqrt{\alpha_t}(\sqrt{\alpha_{t-1}}x_{t-2} + \sqrt{1-\alpha_{t-1}}\epsilon_{t-2}) + \sqrt{1-\alpha_t}\epsilon_{t-1} \\ &= \sqrt{\alpha_t\alpha_{t-1}}x_{t-2} + \sqrt{\alpha_t(1-\alpha_{t-1})}\epsilon_{t-2} + \sqrt{1-\alpha_t}\epsilon_{t-1} \\ &= \sqrt{\alpha_t\alpha_{t-1}}x_{t-2} + \sqrt{\alpha_t(1-\alpha_{t-1}) + (1 - \alpha_t)}\epsilon \\ &= \sqrt{\alpha_t\alpha_{t-1}}x_{t-2} + \sqrt{1-\alpha_t\alpha_{t-1}}\epsilon \end{align}$$
> Note that to combine the two gaussians $\epsilon_{t-1}$ and $\epsilon_{t-2}$, our new gaussian's variance is the sum of the two variances. In other words, the combination of $\mathcal{N}(0, \sigma_1^2 \mathbf{I})$ and $\mathcal{N}(0, \sigma_2^2 \mathbf{I})$ is $\mathcal{N}(0, (\sigma_1^2 + \sigma_2^2) \mathbf{I})$.

Applying this pattern all the way down, we get $$x_t = \sqrt{\bar{\alpha_t}}x_0 + \sqrt{1-\bar{\alpha}}\epsilon$$
where $\bar{\alpha_t} =  \prod_{i=1}^t \alpha_i$. This will be especially helpful during training later.

Our goal is to learn the reverse process $p_\theta(x_{t-1} \vert x_t) = \mathcal{N}(\mu_\theta(x_t, t), \Sigma_\theta(x_t, t))$, which is also a gaussian. Predicting $x_{t-1}$, the noise $\epsilon_t$, and the mean of the noise (assuming we set variance constant) $\mu_t$ is equivalent, but most models choose the second option. We optimize the log likelihood of $p_\theta(x_0)$, which, after a series of derivations, is equivalent to minimizing the $L_2$ loss between the actual applied noise and the predicted noise.

The diffusion forward and reverse processes are depicted below.
![[20230102121606.png]]

# Model
The model itself takes in $x_t$ and the time-step $t$ to predict noise $\epsilon_t$. This is commonly done using a [[👁️ Convolutional Neural Network]] or [[🦿 Vision Transformer]].

# Training
We train our model to minimize loss defined as $$\Vert\epsilon - \epsilon_\theta(\sqrt{\bar{\alpha_t}}x_0 + \sqrt{1-\bar{\alpha_t}}\epsilon, t)\Vert^2$$
where $\epsilon \sim \mathcal{N}(0, \mathbf{I})$, and $t$ is uniformly chosen from $1\ldots T$ at each gradient descent step.

# Prediction
To sample an image, we first generate random noise $x_T = \mathcal{N}(0, \mathbf{I})$. Then, for $T$ iterations,
1. Let $z \sim \mathcal{N}(0, \mathbf{I})$ if $t > 1$, else $z = 0$.
2. $x_{t-1} = \frac{1}{\sqrt{\alpha_t}}(x_t - \frac{1-\alpha_t}{\sqrt{1-\bar{\alpha_t}}}\epsilon_\theta(x_t, t)) + \sigma_t \mathbf{z}$.
Finally, $x_0$ is our generated image.