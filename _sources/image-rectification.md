# How to rectify two cameras?

Intuitively, to rectify two cameras with each other, we need to rotate the cameras.
1. Rotate right (or left) camera to be in the same pose as left (or right) camera.
2. Then rotate both cameras to be parallel to the baseline.

Before contuining to image rectification, lets define some notations.

$x_1$ is the object location (usually a point), located in image1.

$x_2$ is the object location (usually a point), located in image2.

Before solving the correspondence problem, we are required to rotate the cameras to be in line with eachother.

Let $X = [X,Y,Z]^T$ be the world coordinate of the image coordinates, $x_1$ and $x_2$.

From {eq}`projection` we know that the image location of a point is found by the dot product of intrinsic and extrinsic camera parameters.

$$
x_1 = KR_1X = R_1^{-1}K^{-1}x_1
$$

$$
x_2 = KR_1X = K R_2R_1^{-1}K^{-1}*x_1
$$

This gives us a representation of $x_2$ in terms of $x_1$ after rotation.

```{math}
:label: recitification

x_2 = Hx_1
```

$$
H = KR_2R_1^{-1}K^{-1}
$$
 






