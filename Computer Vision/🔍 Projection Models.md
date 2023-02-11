# Lens Model
Our camera contains sensors and a lens. The lens serves to focus light rays from an object and forms an image behind the lens.

![[20230206195556.png]]

We can find the point's image at the intersection of a ray going from the object point through the lens center and a ray going parallel to the lens, then through the focal focal point, which is focal length $f$ away from the lens center. $f$ is a property of the lens curvature.

If $a$ is the distance from the object to the lens and $b$ is the distance from the lens to the image, we have the following relation. $$1/f = 1/a + 1/b$$

Moreover, if $Y$ is the distance of the object point to the optical axis and $y$ is the distance of the image point to the optical axis, with triangle similarity we get that $\frac{Y}{a} = \frac{y}{b}$, so $$y = b\frac{Y}{a}$$

Note that in a lens model, we must focus the image by placing the image plane exactly $b$ away from the lens. Otherwise, if it's too forward or backward, the image of that object is blurry.

> Choosing where we place the image plane is how we decide to focus on foreground or background.

# Pinhole Model
The pinhole model simplifies the lens model by assuming that our lens is infinitely small (like a pinhole), only big enough for one ray the travel through the center. Then, there's no need for focusing, so we let $b = f$.

Assuming we place the image plane in front (so the image is upright), if $Z$ is the distance from the object point to the lens (equivalent to $a$ above), we have that $$x = f\frac{X}{Z}, \ y = f\frac{Y}{Z}$$

Thus, we can zoom in (increase $y$) by either decreasing $Z$ (moving the object closer) or increasing $f$ (changing the focal length)