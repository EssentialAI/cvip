# Introduction and the Pinhole camera

Have you ever wondered what complex mathematics runs behind the miniature camera that we use in our every day life. Point and shoot cameras are ubiquotous to a point that we take camera technology for granted.

Consider an image of a railway track. 

```{image} /imgs/railway.jpg
:alt: railways
:class: bg-primary mb-1
:align: center
```

The rails look as if they converge at the end, however, we know that they do not. The depth of the scene is lost in the image (as the picture is a 2D image). The imperative question arises <span class = 'high'>How do we map a 3D object onto a 2D image?</span> Better yet, How to map a 3D point in space on a 2D plane? While making this 3D to 2D mapping, what is the information about the scene that is lost? What illusions would arise?

This section aims at answering the above questions while providing a detailed explanation of the pinhole camera.

**Computer Vision Overview**
1. Low-level vision
   1. Image processing
   2. Edge detection
   3. Feature detection
   4. Cameras
   5. Image formation
2. Geometry and algorithms
   1. Projective Geometry
   2. Stereo Vision
   3. Structure from motion
3. Recognition
   1. Face detection/recognition
   2. Category recognition
   3. Image segmentation

To model a camera, one must make sure to preserve both geometry and semantics. Some applications of computer vision include but not limited to [Single View modelling](https://www.semanticscholar.org/paper/Single-view-modeling-of-free-form-scenes-Zhang-Dugas-Phocion/0193a8ca0dc5c34cb81cccb8070666d6275738c7), Detection and Recognition, [Visual Question and Answering](https://www.sciencedirect.com/science/article/pii/S1077314217301170), Optical Character Recognition, Entertainment (e.g., Snapchat), Shape Reconstruction using depth sensors, [Building rome in a day!](https://grail.cs.washington.edu/rome/), 3D Scanning, Medical Imaging and so on.

# Image Formation

How a colorful image is formed? All the images are a resultant of the following entities:
1. Lighting Conditions
2. Scene Geometry
3. Surface Properties
4. Camera Properties

<span class = 'high'>The focus of this course is predominantly on the Camera Properties.</span> The image formation requires a light source (e.g., sun) continuously emits photons. These photons are reflected by the surface and a portion of this light is directed towards the camera.

**The sensor plane (the film) has physical existence, but the image plane is virtual.** The image plane is flipped upside down as compared to the sensor plane.

# Pinhole camera model

The pinhole camera makes sure that every unique point in the physical space falls on the film.

```{figure} /imgs/pinhole_1.PNG

---
height: 150px
name: pinhole_1
---

Pinhole camera
```

```{figure} /imgs/pinhole_2.PNG

---
height: 150px
name: pinhole_2
---

Pinhole camera Model
```

The image that we see on the screen after taking an image is virtual image plane. Same phenomenon happens in human eyes.

Zooming in and Zooming out changes the focal length of a camera. (Not digital zoom, optical zoom)

```{figure} /imgs/focal_length.PNG

---
height: 150px
name: focal length
---

Pinhole camera 2D representation
```
The above diagram gives us the first equation for image formation in computer vision. Given a 3D point $P =(X,Y,Z)^T$, the camera projects this point to onto a $2D$ image plane to $p = (x,y)^T$. From the above figure:

\begin{gather*}
\frac{\text{Object size}}{\text{Object distance}} = \frac{\text{Image size}}{\text{Focal Length}}
\end{gather*}

```{math}
:label: first_equation
\frac{X}{Z} = \frac{x}{f}, \frac{Y}{Z} = \frac{y}{f}
```

$$x=f \frac{X}{Z}, y = f\frac{Y}{Z}$$

This is the simplest form of perspective projection. You can change the size of the image by changing any of the above 3 parameters. For a simple example of human face, the image size can be increased by i) actually having a bigger object size $Y$, ii) increasing the focal length $f$, and iii) bringing the object closer to the camera (decreasing $Z$)

In the above figure the focal length is the only parameter that can be changed (as the size of the object and the distance from camera is assumed to be fixed.) This means that upon increasing the focal length the size of the image increases proportionally. When we zooom in, we increase the focal length.


```{admonition} If I zoom in/out of a picture after taking a picture, will focal length change?
:class: tip
After taking a picture, if you zoom in and zoom out, it is a digital zoom. It does not change the focal length of the camera.
```

```{admonition} How to calculate the default focal length of a smartphone camera?
:class: tip
[Calculating the focal length of camera](https://aapt.scitation.org/na101/home/literatum/publisher/aip/journals/content/pte/2019/pte.2019.57.issue-1/1.5084932/20181219/1.5084932.fp.png_v03)
```

**The aim of a camera is to map each of the 3D point in the 3D world to a location in the 2D image plane. Camera does the 3D-2D mapping.** It is also called as the Perspective projection. This leads to a question about how to recover a 3D location of a point from a 2D image.

While projecting from 3D to 2D, the depth information is lost (also the angles between objects in 3D) are lost. <span class = 'high'>Each ray becomes a pixel on the image plane.</span>

```{note}
In the above perspective projection, the angle between lines is not preserved and the depth information is lost.
```

When the distance between camera and the object is too large (god’s view), the difference in sizes of closer objects and far objects is not preserved.

$x = sX, y = sY, \text{ where } s=\frac{f}{Z_0}$, $Z_0$ is the distance between camera and the object.

## Projection Matrix and the Intrinsic parameters
```{math}
:label: second_eq
Z \begin{pmatrix}
\frac{fX}{Z} \\
\frac{fY}{Z} \\
1
\end{pmatrix}
=
\begin{pmatrix}
fX \\
fY \\
Z
\end{pmatrix} = \begin{bmatrix}
f & 0 & 0 & 0\\
0 & f & 0  & 0\\
0 & 0 & 1 & 0
\end{bmatrix}\begin{pmatrix}
X\\
Y\\
Z\\
1
\end{pmatrix}
```

The simplest form of perspective projection in matrix form is given by the above equation.

```{admonition} What is the need for extra row in the 3D coordinate?
:class: tip

The extra column of zeros and the extra 1 in the 3D coordinate is added to incorporate the translation.
```

```{admonition} What do the distances $X, Y, Z$ mean here?
:class: note
$X,Y,Z$ are the relative coordinates of a 3D point from the camera origin. This means that when the object is moved or the camera is moved, the values of $X,Y,Z$ change.
```
This leads us to the question, What about the values of $x,y$? These pixel values are relative to the origin `Principal point` of the image plane. Typically the origin of an image is located at the bottom left or the top left.

Hence, there is a need to make sure the principal point overlaps with the image origin, and we add an **offset** $p_x$ and $p_y$ within the image plane to resolve this issue. **Keep in mind that this offset is not caused by the movement of the object or the camera. It an intrinsic parameter of every camera.**

The {eq}`second_eq` becomes:

```{math}
:label: third_eq

\begin{pmatrix}
fX + Zp_x \\
fY + Zp_y\\
Z
\end{pmatrix} = \begin{bmatrix}
f & 0 & p_x & 0\\
0 & f & p_y  & 0\\
0 & 0 & 1 & 0
\end{bmatrix}\begin{pmatrix}
X\\
Y\\
Z\\
1
\end{pmatrix}
```
$$
K = \begin{bmatrix}
f & 0 & p_x \\
0 & f & p_y  \\
0 & 0 & 1 
\end{bmatrix}
$$

**This is the (Intrinsic) calibration matrix.**

There is an advanced version of the above matrix. It is called Camera Calibration matrix.

```{math}
:label: intrinsic_eq
K = \begin{bmatrix}
\gamma f & s & p_x \\
0 & f & p_y  \\
0 & 0 & 1 
\end{bmatrix}
```

$\gamma$ - when you zoom in and zoom out, the $x$ and $y$ co-ordinates are changed proportionally. However if there is an unproportional change in $x$ and $y$ axes, $\gamma$ takes care of that. $\gamma$ is also called the `aspect ratio` of the pixel.

$s$ - skew of the sensor pixel, i.e., if the pixel is a parallelogram and not a square.

**There are 5 intrinsic parameters for a camera.** Refer {eq}`intrinsic_eq`

## Extrinsic parameters of a camera
The extrinsic parameters come into picture, even before shooting an image. Where the camera is located and it's angle. **(Rotation and Translation)**.

These are the parameters that identify uniquely the transformation between the `unknown camera reference frame` and the `known world reference frame`.

Determining these parameters includes:
1. Finding the translation vector between the relative positions of the origins of the two reference frames.
2. Finding the rotation matrix that brings the corresponding axes of the two frames into alignment (i.e., onto each other).

```{figure} /imgs/rot_translate.PNG

---
height: 150px
name: rot_translate
---

Rotation and Translation from world coordinates to camera coordinates.
```

Using the extrinsic camera parameters, we can find the relation between the coordinates of a point $P$ in the world $(P_w)$ and camera $(P_c)$ coordinates:

```{math}
:label: extrinsic

P_c = R(P_w-T)

```
where

```{math}
:label: extrinsic 1
R = \begin{bmatrix}
r_{11} & r_{12} & r_{13}  \\
r_{21} & r_{22} & r_{23}   \\
r_{31} & r_{32} & r_{33} 
\end{bmatrix}
```

$$ \text{If } $P_c =  \begin{bmatrix}
X_c \\
Y_c \\
Z_c 
\end{bmatrix}$ \text{ and } $P_w = \begin{bmatrix}
X_w \\
Y_w \\
Z_w 
\end{bmatrix}$, \text{ then}
$$

```{math}
:label: extrinsic_final

\begin{bmatrix}
X_c \\
Y_c \\
Z_c 
\end{bmatrix} = \begin{bmatrix}
r_{11} & r_{12} & r_{13}  \\
r_{21} & r_{22} & r_{23}   \\
r_{31} & r_{32} & r_{33} 
\end{bmatrix}\begin{bmatrix}
X_w-T_x \\
Y_w-T_y \\
Z_w-T_z 
\end{bmatrix}
```
In other words, we first translate the coordinates to match the camera coordinates and then rotate the axes so that both camera axes and world coordinate axes overlap.

$$
X_c = R_1^T(P_w-T) \\
Y_c = R_2^T(P_w-T) \\
Z_c = R_3^T(P_w-T)
$$

where $R_i^T$ corresponds to the $i^{th}$ row of the rotation matrix.
















