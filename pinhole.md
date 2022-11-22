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
The above diagram gives us the first equation for image formation in computer vision.

\begin{gather*}
\frac{\text{Object size}}{\text{Object distance}} = \frac{\text{Image size}}{\text{Focal Length}}
\end{gather*}

```{math}
:label: focal_length
\frac{Y}{Z} = \frac{y}{f}
```

\begin{gather*}
y = f\frac{Y}{Z}
\end{gather*}



This is the simplest form of perspective projection. You can change the size of the image by changing any of the above 3 parameters. For a simple example of human face, the image size can be increased by i) actually having a bigger object size $Y$, ii) increasing the focal length $f$, and iii) bringing the object closer to the camera (decreasing $Z$)

In the above figure the focal length is the only parameter that can be changed (as the size of the object and the distance from camera is assumed to be fixed.) This means that upon increasing the focal length the size of the image increases proportionally. When we zooom in, we increase the focal length.

```{admonition} How to calculate the default focal length of a smartphone camera?
:class: tip
[Calculating the focal length of camera](https://aapt.scitation.org/na101/home/literatum/publisher/aip/journals/content/pte/2019/pte.2019.57.issue-1/1.5084932/20181219/1.5084932.fp.png_v03)
```

**The aim of a camera is to map each of the 3D point in the 3D world to a location in the 2D image plane. Camera does the 3D-2D mapping.** It is also called as the Perspective projection. This leads to a question about how to recover a 3D location of a point from a 2D image.

While projecting from 3D to 2D, the depth information is lost (also the angles between objects in 3D) are lost. `Each ray becomes a pixel on the image plane.`








