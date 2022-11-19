# Introduction and the Pinhole camera

Have you ever wondered what complex mathematics runs behind the miniature camera that we use in our every day life. Point and shoot cameras are ubiquotous to a point that we take camera technology for granted.

Consider an image of a railway track. 

```{image} /imgs/railway.jpg
:alt: railway
:class: bg-primary mb-1
:width: 500px
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

```{figure} /imgs/pinhole_1.png
---
<!-- height: 150px -->
name: pinhole_1
---
The pinhole camera.
```







