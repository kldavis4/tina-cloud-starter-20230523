---
title: 'Mobile App With Facial Recognition Feature: How To Make It Real'
slug: mobile-app-facial-recognition-feature
author: nataliia-illia
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea7ce5bf-2a4b-49b6-95a3-f51ba397e009/training-set-to-data-matrix-opt.png
date: 2018-02-06T15:30:52+01:00
summary: >-
  Given that facial recognition is gaining in popularity but the process of implementation is rather vague, Nataliia and Illia decided to share their experience of dealing with facial recognition algorithms and engines and things they’ve learned.
description: >-
  Given that facial recognition is gaining in popularity but the process of implementation is rather vague, Nataliia and Illia decided to share their experience of dealing with facial recognition algorithms and engines and things they’ve learned.
categories:
  - Apps
  - iOS
  - Machine Learning
---
Imagine an application that can, in real time, analyze a user’s emotional response while they’re interacting with an app or website. Or imagine a home device that recognizes you and tunes in to your favorite TV channel. 

Yes, today’s article is all about facial recognition technology. We’re going to share our first experience of dealing with this technology and the findings we’ve made.

## Why Is Facial Recognition On The Rise?

The technology of facial recognition is not new, but it foresees new growth opportunities in the coming years. The major factor driving progress is an unlimited number of ways to apply facial recognition in various business areas. Here are just a few examples:

- **System Security**  
Facial recognition can be widely applied as a security authentication method. Not so long ago, Amazon invented an authentication method, known as "Image Analysis for User Authentication". It enables users to make a transaction by performing a certain action (a smile or wink) in front of the camera, thus confirming their identity.

- **User Safety**  
Caterpillar has applied facial recognition technology to solve the problem of sleepy drivers. A special program assesses how tired a driver looks. By constantly analyzing the position of their eyes and head, the system can decide whether the plant operator needs a wake-up call. 

- **User Engagement**  
One way to increase the loyalty of customers to cafes, restaurants and hotels is by using facial recognition technology to welcome them in person. 

All of these examples require not only software but also video cameras, servers and other infrastructure. However, there is a less resource-intensive method, which is the focus of our topic.

Mobile app creators have not ignored the growing interest in facial recognition technology. Indeed, they are considering new ways to apply the technology in an unconventional way. My software development company is increasingly working with clients that want to add facial recognition to their mobile apps. Let me tell about one of those experiences and the way we implemented the required feature.

{{% feature-panel %}}

## How Facial Recognition Technology Works

Facial recognition is the enhanced application of image analysis technology. The input is an image or video stream. The output is identification or verification of the object that appears in the image or video. In general, facial recognition systems work in the following way. The process of facial recognition is usually defined as a fiv-step process:

1. Facial detection and tracking,
2. Facial alignment,
3. Feature extraction,
4. Feature matching,
5. Facial recognition.

Facial detection is the process of identifying a human face within a scanned image. Feature extraction involves obtaining relevant facial patterns — facial regions (such as eyes spacing), variations, angles and ratios — to determine whether the object is human. Finally, the system tries to recognize the face and match it to a name stored in the database.

There are numerous approaches to facial recognition. The main difference between all of the algorithms is the calculation of features and the comparison of their data sets to each other. The approach we’ve chosen is a combination of principal component analysis and neural networks. Let’s see how these algorithms work.

### Principal Component Analysis

Principal component analysis (PCA) is one of the most popular and elaborate algorithms for facial recognition. The image is represented as a small-dimensional vector (main component), which is then compared with benchmark vectors from the database. The main purpose of PCA is to significantly reduce the dimensionality of the features that allows them to describe the “typical” features of different faces. Here’s how it works.

First, an inputted training set of faces is transformed into one common data matrix. 

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea7ce5bf-2a4b-49b6-95a3-f51ba397e009/training-set-to-data-matrix-opt.png" sizes="100vw" caption="Transformation of the training set of faces into a single matrix" alt="Training set of images is transformed into a data matrix" >}}

Using this matrix, the inputted image is decomposed into a set of linear coefficients, called principal components or eigenfaces. 

The principal components are calculated for each facial image, with the algorithm usually requiring from 5 to 300 eigenfaces. The remaining components identify the minor differences between faces and the background noise in the image. The recognition process involves, in fact, comparing the main components of an unknown image with the components of all the other images.

Principal component analysis is well proven. However, in cases of significant changes in brightness or facial expression, the effectiveness of the method is significantly reduced. The solution to this problem is to use Fisher's linear discriminant (aka Fisherface). Experiments show that under conditions of oblique lighting or shading of facial images, Fisherface still has 95% efficiency, compared to 53% for the eigenface method.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6bb92f9-bb6e-4880-8668-988f588dc495/examples-of-eigenfaces-opt.png" sizes="100vw" caption="An example of the eigenfaces obtained for a trained set of faces" alt="Eigenfaces from a trained set of faces" >}} 

## Artificial Neural Networks

Artificial neural networks are a popular method of facial recognition. They are used for feature extraction and decision-making. One of the most widely used options is a network built on a multi-layer perceptron, which allows classification of the input image in compliance with the pretrained network.

Neural networks are trained on a set of learning examples. During training, the neural network automatically extracts key features, determines their importance and builds relationships between them. It is assumed that the trained neural network will be able to apply the experience gained in the training process to unknown images, thanks to its abilities to generalize.

Convolutional neural networks show the best results in analyzing visual imagery, due to their ability to take into account the two-dimensional topology of the image, in contrast to the multi-layer perceptron. That is why a convolutional neural network is less affected by scale changes, biases, turns, angles and other distortions.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fde14571-693b-440a-8c40-99fb65c44e94/convolutional-neural-network-architecture-opt.png" sizes="100vw" caption="Schematic representation of the architecture of a convolutional neural network" alt="Architecture of a convolutional neural network" >}}

Being a relatively time- and energy-consuming process, however, trained neural networks show rather good results for facial recognition and decrease the error rate. The main problem is adding a new benchmark face to the database, which requires a complete retraining of the network across the entire database set.

In general, the combination of principal component analysis and neural networking works as follows. Faces are extracted from the images and described by a set of eigenfaces using PCA. Neural networks are then used to recognize the face through learning the right classification of the descriptors.

## Facial Recognition Project Implementation

### Project Overview

An application that requires the implementation of a facial recognition feature could be a simple note-taking app. It allows registered users to securely create, store and view confidential texting notes, using facial recognition as a secure way to access them.

When users run the app for the first time, they have to create a new account or log into an existing account. Creating an account is a simple and quick process that enables the user to capture a series of photos of their face through the device’s camera.

Once the app is launched, it starts the facial recognition engine. The app asks the user to look at the camera. The facial recognition engine evaluates the user’s facial data captured using the device’s camera. If the facial data matches the local data securely stored in the user’s profile, the text content is decrypted and displayed on the screen. The facial recognition engine continually evaluates the user’s face data every N seconds; if the captured facial data doesn’t match, the content is blurred. Here’s what it looks like.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05a12f1b-4341-4750-bef6-fcb0278e3c3d/face-recognition-feature-in-app-opt.png" sizes="100vw" caption="Scheme of facial recognition functionality in the app" alt="Facial recognition functionality in the app" >}}

### Facial Recognition With OpenCV

OpenCV is an open-source library initially aimed at implementing computer vision and machine learning in various apps. In general, OpenCV is an infrastructure for object detection that can be trained to detect any objects, including faces. Its toolkit contains thousands of optimized algorithms to serve various purposes. That’s why OpenCV seemed a perfect choice for our project.

Here are three ways to add OpenCV to your own iOS project:

1. Using CocoaPods: pod “OpenCV.”
2. Get and add an official iOS framework release to your project.
3. Using sources from [GitHub](https://github.com/Itseez/opencv), and follow the [instructions](https://docs.opencv.org/2.4/doc/tutorials/introduction/ios_install/ios_install.html#ios-installation) to build your own library.

OpenCV is good enough for the implementation of the two basic tasks of facial recognition: detection and recognition.

#### Facial Detection

The library has many ready-to-use settings for facial detection and facial features, even smiles. Detection is carried out through training. During the training process, the decision tree is usually optimized using positive images (ones with faces) and false images (those without faces).

The process of training is aimed at determining the cascade of correct features and their scales and weights. These parameters are loaded to initialize a classifier. During detection, the trained classifier is moved across all of the pixels in the input image at different scales, to be able to detect faces of different sizes.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3371eb92-68a6-4144-b12e-248e8572c412/eigenfaces-in-opencv-opt.png" sizes="100vw" caption="Eigenfaces in OpenCV" alt="Examples of eigenfaces obtained with OpenCV" >}}

Some things affect the training of the system:

1. One is the quality of the images used for training and how you crop them. In order to unify the input images, we’ve added a rectangular area to the registration screen that shows the desired position and distance of the user’s face relative to the camera.
2. The number of images you need for accurate training is also a factor. For our system, we consider nine images to be enough.
3. You might also consider the possibility of asking users to take profile pictures of their face (i.e. turned to the side) for better recognition.

#### Facial Recognition

There are three basic algorithms for facial recognition in OpenCv: eigenfaces, Fisherfaces, and local binary patterns histograms (LBPH). You can learn more about them in the OpenCV [documentation](https://docs.opencv.org/modules/contrib/doc/facerec/facerec_tutorial.html#local-binary-patterns-histograms). In our project, we were using the LBPH algorithm, because the user input can be updated without requiring a total retraining of the system.

**Why OpenCV Is Not The Best Choice For Our Project**  

Having tried to implement the project using the potential of OpenCV, we came to the conclusion that the platform was not the right tool for our project, for one critical reason. The OpenCV neural network is not cut out for real-time recognition. It is pretty good at recognizing faces in images and, therefore, will best suit social network apps. However, with the changing conditions of real-time recognition, such as changes in lighting or the user’s hair style, the system doesn't work properly.

That is the main reason why we switched to another facial recognition platform.

### Step-By-Step Facial Recognition With Kairos

The market has a great variety of facial recognition providers to meet all of your needs. Kairo is among the best of them, and we decided to give it a try. We had to make a choice: either use a Kairos SDK for iOS apps or opt for the [Kairos API](https://www.kairos.com/docs/api/#face-recognition) and implement the facial recognition functionality ourselves. We chose the Kairos API for our project, because it was a much cheaper solution. 

The principles of facial detection and recognition are virtually identical to those of OpenCV. So, there is no need to repeat the basics. Here’s how they work together with Kairos.

1. During registration, the app accesses the device’s camera to obtain images of the user. We require nine images to store in the database. 
2. The image-enroll functionality in Kairos stores the images in a created gallery. The images require an ID (i.e. the name of the user). The gallery also requires a name for its identification. Parameters used:
`image`: a publicly accessible URL, an uploaded file or a base64-encoded photo
`subject_id`: identifier for the face
`gallery_name`: identifier for the gallery.
3. **Recognition**  
The library uses neural networks to learn the features of the face and create a face template. Each time authorization is required, it compares a template of the image with the stored templates. The library may or may accept that the person is the same as the one in the submitted images.
4. **Interpretation of results**  
In cases where the inputted image and the stored template matches, the app displays the subject’s ID and grants access to the app. The program returns the result with two parameters: name and probability (or the level of confidence). The threshold of recognition is 80% confidence by default. This means that if the confidence level is below 80%, the API will not consider it a match. Optionally, you can change this parameter to be higher or lower. However, the threshold of 80% is optimal, because if you set it higher, you run the risk of false rejects.
5. **Response to rejection**  
If the inputted image doesn’t match the data stored in the database, the images and text in the app are blurred.

**Problems And Solutions**

The main problem we faced had to do with memory allocation. Because of the constant access to the device’s RAM for image processing, the device overheated. The solution was to connect an OpenGL library that handles images and multithreading and that gives access to the CPU directly.

We have yet to solve the problem with image recognition of when the user tries to take a photo when bright sunlight is behind them, which “blinds” the device’s camera.

## What We Learned From The Project

Choosing the wrong provider of facial recognition functionality can cause problems during development. Experience shows that when you choose a tool for implementing a facial recognition feature, you should clearly understand the objectives of your product and analyze the market. Some engines are good at detecting faces in images, while others are a perfect fit for real-time facial recognition.

### Option 1: Open-Source Libraries

You can opt for one of the free tools. The OpenCV library, for instance, allows for implementation of facial recognition projects for free. However, keep in mind that OpenCV works well for facial detection, rather than for real-time facial recognition, and you will have to adapt it for facial recognition purposes. All you will need is a team of experienced developers and a great deal of time. In this case, the resulting product will be able to recognize faces that are well lit and that are against a plain background.

### Option 2: Facial Recognition Software

Numerous services offer an API and SDK for facial recognition. We chose Kairos’ API due to its cost and simplicity. The engine gives developers all of the means required for learning and recognition. So, you don’t have to maintain an army of developers. Under certain conditions, it’s reasonable to opt for an SDK instead of an API. For instance, if your app has to recognize faces in offline mode or if you care about speed, then an SDK is a better choice. Luckily, most platform providers have both and supply clear documentation to help you make a sound decision. 

## Conclusion

Despite all of the limitations of facial recognition, such as variations in posing, lighting and image quality, the technology is gaining in popularity and eventually will become a part of users’ everyday lives. The platforms that provide simple implementation of facial recognition technology use different algorithms and, therefore, can be used in various types of apps.

We’ve tried to show the experience we gained in our particular project. As you can see, the really simple idea of using facial recognition functionality was not that simple to implement. We faced some problems and tried to find solutions to make it work more efficiently. We hope our experience will be useful for you.

{{< signature "da, ra, al, il" >}}

