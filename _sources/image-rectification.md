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

Here in the above case, both cameras are considered to have the same intrinsic parameter matrix $K$. Else, $K_1$, $K_2$.

In short, to find the matrix $H$, we need to know:
1. Intrinsic parameters of the cameras
2. The pose of the camera.

The translation is considered to be $0$ here.

## Fundamental matrix

<span class = 'high'>The epipolar geometry is the intrinsic projective geometry between two views. It is independent of scene structure, and only depends on the internal parameters and the relative pose.</span>

The fundamental matrix $F$ encapsulates this intrinsic geometry. It is a $3 \times 3$ matrix of <span class ='high'>rank 2</span>. If a point in a 3-space $X$ is images as $x_1$ in the first view and $x_2$ in the second, then the image points satisfy the relation:

```{math}
:label: fundamental
x_2^TFx = 0
```

### Calculating fundamental matrix

$$
P_r = R(P_l-T)
$$






