# Distortion
Perspective distortion occurs with close objects causing parallel lines in the world to be less parallel the closer they get to the camera.

![[20230206200615.png]]

## Dolly Zoom

![[20230206200616.gif|300]]

Dolly zoom is a special application of perspective distortion. It keeps the object size constant while shrinking or stretching the background.
1. If parallel lines aren't parallel, we have small $Z$ and small $f$. In other words, we're close to the object with a small focal length.
2. If parallel lines are parallel, we have large $Z$ and $f$. In other words, we're far from the object with a large focal length.

If the background shrinks, we're transitioning from (2) to (1), moving closer to the object while zooming out. Conversely, if the background stretches, we go from (1) to (2), moving farther while zooming in.

# Vanishing Points and Parallel Lines
In the real world, parallel lines don't intersection. However, due to the projection onto the image, parallel lines may intersect at vanishing points. On the other hand, intersecting lines in the real world may appear parallel in an image. Both cases are illustrated below.

![[20230206205902.png|300]]
The vanishing point of two real-world parallel lines is the intersection of a parallel ray from the camera to the image plane.

![[20230206205945.png|300]]
Real-world intersecting lines appear parallel when their intersection cannot be projected onto the image plane. In other words, they intersect at a point at infinity, and the ray from the camera to the point is parallel to the image plane.