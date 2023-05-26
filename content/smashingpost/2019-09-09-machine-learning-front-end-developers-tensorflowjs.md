---
title: 'Machine Learning For Front-End Developers With Tensorflow.js'
slug: machine-learning-front-end-developers-tensorflowjs
author: charlie-gerard
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd7f6338-3ee4-4d23-a76a-79222e1ed8f8/machine-learning-front-end-developers-tensorflowjs.png
date: 2019-09-09T14:00:59+02:00
summary: >-
  Using JavaScript and frameworks like Tensorflow.js is a great way to get started and learn more about machine learning. In this article, Charlie Gerard covers the three main features currently available using Tensorflow.js and sheds light onto the limits of using machine learning in the frontend.
description: >-
  Using JavaScript and frameworks like Tensorflow.js is a great way to get started and learn more about machine learning. In this article, Charlie Gerard covers the three main features currently available using Tensorflow.js and sheds light onto the limits of using machine learning in the frontend.
categories:
  - JavaScript
  - Machine Learning
  - UX
---
Machine learning often feels like it belongs to the realm of data scientists and Python developers. However, over the past couple of years, open-source frameworks have been created to make it more accessible in different programming languages, including JavaScript. In this article, we will use Tensorflow.js to explore the different possibilities of using machine learning in the browser through a few example projects.

## What Is Machine Learning?

Before we start diving into some code, let’s talk briefly about what machine learning is as well as some core concepts and terminology.

### Definition

A common definition is that it is the ability for computers to learn from data without being explicitly programmed.

If we compare it to traditional programming, it means that we let computers identify patterns in data and generate predictions without us having to tell it exactly what to look for.

Let’s take the example of fraud detection. There is no set criteria to know what makes a transaction fraudulent or not; frauds can be executed in any country, on any account, targeting any customer, at any time, and so on. It would be pretty much impossible to track all of this manually.

However, using previous data around fraudulent expenses gathered over the years, we can train a machine-learning algorithm to understand patterns in this data to generate a model that can be given any new transaction and predict the probability of it being fraud or not, without telling it exactly what to look for.

{{% feature-panel %}}

### Core Concepts

To understand the following code samples, we need to cover a few common terms first.

#### Model

When you train a machine-learning algorithm with a dataset, the model is the output of this training process. It’s a bit like a function that takes new data as input and produces a prediction as output.

#### Labels And Features

Labels and features relate to the data that you feed an algorithm in the training process.

A label represents how you would classify each entry in your dataset and how you would label it. For example, if our dataset was a CSV file describing different animals, our labels could be words like "cat", "dog" or "snake" (depending on what each animal represents).

Features on the other hand, are the characteristics of each entry in your data set. For our animals example, it could be things like "whiskers, meows", "playful, barks", "reptile, rampant", and so on.

Using this, a machine-learning algorithm will be able to find some correlation between features and their label that it will use for future predictions.

#### Neural Networks

Neural networks are a set of machine-learning algorithms that try to mimic the way the brain works by using layers of artificial neurons.

We don’t need to go in-depth about how they work in this article, but if you want to learn more, here’s a really good video:

<figure class="video-container break-out"><iframe loading="lazy" src="https://www.youtube.com/embed/aircAruvnKk" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

Now that we’ve defined a few terms commonly used in machine learning, let’s talk about what can be done using JavaScript and the Tensorflow.js framework.

### Features

Three features are currently available:

<ol>
  <li><a href="#pre-trained-model">Using a pre-trained model</a>,</li>
  <li><a href="#transfer-learning">Transfer learning</a>,</li>
  <li><a href="#defining-running-using-own-model">Defining, running, and using your own model</a>.</li>
</ol>

Let’s start with the simplest one.

#### 1. Using A Pre-Trained Model

Depending on the problem you are trying to solve, there might be a model already trained with a specific data set and for a specific purpose which you can leverage and import in your code.

For example, let’s say we are building a website to predict if an image is a picture of a cat. A popular image classification model is called *MobileNet* and is available as a pre-trained model with Tensorflow.js.

The code for this would look something like this:

<div class="break-out">

<pre><code class="language-html">&lt;html lang="en"&gt;
  &lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
    &lt;meta http-equiv="X-UA-Compatible" content="ie=edge"&gt;
    &lt;title&gt;Cat detection&lt;/title&gt;
    &lt;script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@1.0.1"&gt; &lt;/script&gt;
    &lt;script src="https://cdn.jsdelivr.net/npm/@tensorflow-models/mobilenet@1.0.0"&gt; &lt;/script&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;img id="image" alt="cat laying down" src="cat.jpeg"/&gt;

    &lt;script&gt;
      const img = document.getElementById('image');

      const predictImage = async () => {
        console.log("Model loading...");
        const model = await mobilenet.load();
        console.log("Model is loaded!")

        const predictions = await model.classify(img);
        console.log('Predictions: ', predictions);
      }
      predictImage();
    &lt;/script&gt;
  &lt;/body&gt;
&lt;/html&gt;</code></pre>
</div>

We start by importing Tensorflow.js and the MobileNet model in the head of our HTML:

<div class="break-out">

<pre><code class="language-html">&lt;script src="https://cdnjs.cloudflare.com/ajax/libs/tensorflow/1.0.1/tf.js"&gt; &lt;/script&gt;
&lt;script src="https://cdn.jsdelivr.net/npm/@tensorflow-models/mobilenet@1.0.0"&gt; &lt;/script&gt;</code></pre>
</div>

Then, inside the body, we have an image element that will be used for predictions:

<pre><code class="language-html">&lt;img id="image" alt="cat laying down" src="cat.jpeg"/&gt;</code></pre>

And finally, inside the `script` tag, we have the JavaScript code that loads the pre-trained MobileNet model and classifies the image found in the `image` tag. It returns an array of 3 predictions which are ordered by probability score (the first element being the best prediction).

<pre><code class="language-javascript">const predictImage = async () => {
  console.log("Model loading...");
  const model = await mobilenet.load();
  console.log("Model is loaded!")
  const predictions = await model.classify(img);
  console.log('Predictions: ', predictions);
}

predictImage();</code></pre>

And that’s it! This is the way you can use a pre-trained model in the browser with Tensorflow.js!

**Note**: *If you want to have a look at what else the MobileNet model can classify, you can find [a list of the different classes](https://github.com/tensorflow/tfjs-examples/blob/master/mobilenet/imagenet_classes.js) available on Github.*

An important thing to know is that loading a pre-trained model in the browser can take some time (sometimes up to 10s) so you will probably want to preload or adapt your interface so that users are not impacted.

If you prefer using Tensorflow.js as a NPM module, you can do so by importing the module this way:

<pre><code class="language-javascript">import * as mobilenet from '@tensorflow-models/mobilenet';</code></pre>

Feel free to play around with this example on [CodeSandbox](https://codesandbox.io/s/snowy-cherry-3i0z8?fontsize=14).

Now that we’ve seen how to use a pre-trained model, let’s look at the second feature available: transfer learning.

{{% ad-panel-leaderboard %}}

#### 2. Transfer Learning

Transfer learning is the ability to combine a pre-trained model with custom training data. What this means is that you can leverage the functionality of a model and add your own samples without having to create everything from scratch.

For example, an algorithm has been trained with thousands of images to create an image classification model, and instead of creating your own, transfer learning allows you to combine new custom image samples with the pre-trained model to create a new image classifier. This feature makes it really fast and easy to have a more customized classifier.

To provide an example of what this would look like in code, let’s repurpose our previous example and modify it so we can classify new images.

**Note**: *The end result is the experiment below that you can [try live here](https://zvs9k.sse.codesandbox.io/).*

<figure class="break-out"><a href="https://zvs9k.sse.codesandbox.io/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d31959f-5aae-4e76-bd52-12e91bd6032e/tfjs-transfer-800w.gif" width="800" height="" alt="" /></a><figcaption>(<a href='https://zvs9k.sse.codesandbox.io'>Live demo</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5285241-369b-4994-9737-f743b3ff871f/tfjs-transfer.gif">Large preview</a>)</figcaption></figure>

Below are a few code samples of the most important part of this setup, but if you need to have a look at the whole code, you can find it on this [CodeSandbox](https://codesandbox.io/s/tfjstransferlearning-zvs9k).

We still need to start by importing Tensorflow.js and MobileNet, but this time we also need to add a KNN (k-nearest neighbor) classifier:

<div class="break-out">

<pre><code class="language-html">&lt;!-- Load TensorFlow.js --&gt;
&lt;script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs"&gt;&lt;/script&gt;
&lt;!-- Load MobileNet --&gt;
&lt;script src="https://cdn.jsdelivr.net/npm/@tensorflow-models/mobilenet"&gt;&lt;/script&gt;
&lt;!-- Load KNN Classifier --&gt;
&lt;script src="https://cdn.jsdelivr.net/npm/@tensorflow-models/knn-classifier"&gt;&lt;/script&gt;</code></pre>
</div>

The reason why we need a classifier is because (instead of only using the MobileNet module) we’re adding custom samples it has never seen before, so the KNN classifier will allow us to combine everything together and run predictions on the data combined.

Then, we can replace the image of the cat with a `video` tag to use images from the camera feed.

<pre><code class="language-html">&lt;video autoplay id="webcam" width="227" height="227"&gt;&lt;/video&gt;</code></pre>

Finally, we’ll need to add a few buttons on the page that we will use as labels to record some video samples and start the predictions.

<pre><code class="language-html">&lt;section&gt;
  &lt;button class="button"&gt;Left&lt;/button&gt;

  &lt;button class="button"&gt;Right&lt;/button&gt;

  &lt;button class="test-predictions"&gt;Test&lt;/button&gt;
&lt;/section&gt;</code></pre>

Now, let’s move to the JavaScript file where we’re going to start by setting up a few important variables:

<pre><code class="language-javascript">// Number of classes to classify
const NUM_CLASSES = 2;
// Labels for our classes
const classes = ["Left", "Right"];
// Webcam Image size. Must be 227.
const IMAGE_SIZE = 227;
// K value for KNN
const TOPK = 10;

const video = document.getElementById("webcam");</code></pre>

In this particular example, we want to be able to classify the webcam input between our head tilting to the left or the right, so we need two classes labeled `left` and `right`.

<p class="c-pre-sidenote--left">The image size set to 227 is the size of the video element in pixels. Based on the Tensorflow.js examples, this value needs to be set to 227 to match the format of the data the MobileNet model was trained with. For it to be able to classify our new data, the latter needs to fit the same format.</p><p class="c-sidenote c-sidenote--right">If you really need it to be larger, it is possible but you will have to transform and resize the data before feeding it to the KNN classifier.</p>

Then, we’re setting the value of K to 10. The K value in the KNN algorithm is important because it represents the number of instances that we take into account when determining the class of our new input.

In this case, the value of 10 means that, when predicting the label for some new data, we will look at the 10 nearest neighbors from the training data to determine how to classify our new input.

Finally, we’re getting the `video` element. For the logic, let’s start by loading the model and classifier:

<pre><code class="language-javascript">async load() {
    const knn = knnClassifier.create();
    const mobilenetModule = await mobilenet.load();
    console.log("model loaded");
}</code></pre>

Then, let’s access the video feed:

<pre><code class="language-javascript">navigator.mediaDevices
  .getUserMedia({ video: true, audio: false })
  .then(stream => {
    video.srcObject = stream;
    video.width = IMAGE_SIZE;
    video.height = IMAGE_SIZE;
  });</code></pre>

Following that, let’s set up some button events to record our sample data:

<pre><code class="language-javascript">setupButtonEvents() {
    for (let i = 0; i < NUM_CLASSES; i++) {
      let button = document.getElementsByClassName("button")[i];

      button.onmousedown = () => {
        this.training = i;
        this.recordSamples = true;
      };
      button.onmouseup = () => (this.training = -1);
    }
  }</code></pre>

Let’s write our function that will take the webcam images samples, reformat them and combine them with the MobileNet module:

<div class="break-out">

<pre><code class="language-javascript">// Get image data from video element
const image = tf.browser.fromPixels(video);

let logits;
// 'conv_preds' is the logits activation of MobileNet.
const infer = () => this.mobilenetModule.infer(image, "conv_preds");

// Train class if one of the buttons is held down
if (this.training != -1) {
  logits = infer();

  // Add current image to classifier
  this.knn.addExample(logits, this.training);
}</code></pre>
</div>

And finally, once we gathered some webcam images, we can test our predictions with the following code:

<pre><code class="language-javascript">logits = infer();
const res = await this.knn.predictClass(logits, TOPK);
const prediction = classes[res.classIndex];</code></pre>

And finally, you can dispose of the webcam data as we don’t need it anymore:

<pre><code class="language-javascript">// Dispose image when done
image.dispose();
if (logits != null) {
  logits.dispose();
}</code></pre>

Once again, if you want to have a look at the full code, you can find it in the [CodeSandbox](https://codesandbox.io/s/tfjstransferlearning-zvs9k) mentioned earlier.

#### 3. Training A Model In The Browser

The last feature is to define, train and run a model entirely in the browser. To illustrate this, we’re going to build the classic example of recognizing Irises.

For this, we’ll create a neural network that can classify Irises in three categories: Setosa, Virginica, and Versicolor, based on an open-source dataset.

Before we start, here’s a link to the [live demo](https://ktncm.codesandbox.io/) and here’s the [CodeSandbox](https://codesandbox.io/s/tfjsall-ktncm) if you want to play around with the full code.

<iframe loading="lazy" src="https://codesandbox.io/embed/tfjsall-ktncm?fontsize=14" title="tfjs-all" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media; usb" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

At the core of every machine learning project is a dataset. One of the first step we need to undertake is to split this dataset into a training set and a test set.

The reason for this is that we’re going to use our training set to train our algorithm and our test set to check the accuracy of our predictions, to validate if our model is ready to be used or needs to be tweaked.

**Note**: *To make it easier, I already split the training set and test set into two JSON files you can find in the [CodeSanbox](https://codesandbox.io/s/tfjsall-ktncm).*

The training set contains 130 items and the test set 14. If you have a look at what this data looks like you’ll see something like this:

<pre><code class="language-javascript">{
  "sepal_length": 5.1,
  "sepal_width": 3.5,
  "petal_length": 1.4,
  "petal_width": 0.2,
  "species": "setosa"
}</code></pre>

What we can see is four different features for the length and width of the sepal and petal, as well as a label for the species.

To be able to use this with Tensorflow.js, we need to shape this data into a format that the framework will understand, in this case, for the training data, it will be `[130, 4]` for 130 samples with four features per iris.

<pre><code class="language-javascript">import * as trainingSet from "training.json";
import * as testSet from "testing.json";

const trainingData = tf.tensor2d(
  trainingSet.map(item => [
    item.sepal_length,
    item.sepal_width,
    item.petal_length,
    item.petal_width
  ]),
  [130, 4]
);

const testData = tf.tensor2d(
  testSet.map(item => [
    item.sepal_length,
    item.sepal_width,
    item.petal_length,
    item.petal_width
  ]),
  [14, 4]
);</code></pre>

Next, we need to shape our output data as well:

<pre><code class="language-javascript">const output = tf.tensor2d(trainingSet.map(item => [
    item.species === 'setosa' ? 1 : 0,
    item.species === 'virginica' ? 1 : 0,
    item.species === 'versicolor' ? 1 : 0

]), [130,3])</code></pre>

Then, once our data is ready, we can move on to creating the model:

<pre><code class="language-javascript">const model = tf.sequential();

model.add(tf.layers.dense(
    {
        inputShape: 4,
        activation: 'sigmoid',
        units: 10
    }
));

model.add(tf.layers.dense(
    {
        inputShape: 10,
        units: 3,
        activation: 'softmax'
    }
));</code></pre>

In the code sample above, we start by instantiating a sequential model, add an input and output layer.

The parameters you can see used inside (`inputShape`, `activation`, and `units`) are out of the scope of this post as they can vary depending on the model you are creating, the type of data used, and so on.

Once our model is ready, we can train it with our data:

<div class="break-out">

<pre><code class="language-javascript">async function train_data(){
    for(let i=0;i<15;i++){
      const res = await model.fit(trainingData, outputData,{epochs: 40});
    }
}

async function main() {
  await train_data();
  model.predict(testSet).print();
}</code></pre>
</div>

If this works well, you can start replacing the test data with custom user inputs.

Once we call our main function, the output of the prediction will look like one of these three options:

<pre><code class="language-javascript">[1,0,0] // Setosa
[0,1,0] // Virginica
[0,0,1] // Versicolor</code></pre>

The prediction returns an array of three numbers representing the probability of the data belonging to one of the three classes. The number closest to 1 is the highest prediction.

For example, if the output of the classification is `[0.0002, 0.9494, 0.0503]`, the second element of the array is the highest, so the model predicted that the new input is likely to be a Virginica.

And that’s it for a simple neural network in Tensorflow.js!

We only talked about a small dataset of Irises but if you want to move on to larger datasets or working with images, the steps will be the same:

- Gathering the data;
- Splitting between training and testing set;
- Reformatting the data so Tensorflow.js can understand it;
- Picking your algorithm;
- Fitting the data;
- Predicting.

If you want to save the model created to be able to load it in another application and predict new data, you can do so with the following line:

<pre><code class="language-javascript">await model.save('file:///path/to/my-model'); // in Node.js</code></pre>

**Note**: *For more options on how to save a model, have a look at [this resource](https://www.tensorflow.org/js/guide/save_load).*

{{% ad-panel-leaderboard %}}

### Limits

That’s it! We’ve just covered the three main features currently available using Tensorflow.js!

Before we finish, I think it is important to briefly mention some of the limits of using machine learning in the frontend.

#### 1. Performance

Importing a pre-trained model from an external source can have a performance impact on your application. Some objects detection model, for example, are more than 10MB, which is significantly going to slow down your website. Make sure to think about your user experience and optimize the loading of your assets to improve your perceived performance.

#### 2. Quality Of The Input Data

If you build a model from scratch, you’re going to have to gather your own data or find some open-source dataset.

Before doing any kind of data processing or trying different algorithms, make sure to check the quality of your input data. For example, if you are trying to build a sentiment analysis model to recognize emotions in pieces of text, make sure that the data you are using to train your model is accurate and diverse. If the quality of the data used is low, the output of your training will be useless.

#### 3. Liability

Using an open-source pre-trained model can be very fast and effortless. However, it also means that you don’t always know how it was generated, what the dataset was made of, or even which algorithm was used. Some models are called “black boxes”, meaning that you don’t really know how they predicted a certain output.

Depending on what you are trying to build, this can be a problem. For example, if you are using a machine-learning model to help detect the probability of someone having cancer based on scan images, in case of false negative (the model predicted that a person didn’t have cancer when they actually did), there could be some real legal liability and you would have to be able to explain why the model made a certain prediction.

## Summary

In conclusion, using JavaScript and frameworks like Tensorflow.js is a great way to get started and learn more about machine learning. Even though a production-ready application should probably be built in a language like Python, JavaScript makes it really accessible for developers to play around with the different features and get a better understanding of the fundamental concepts before eventually moving on and investing time into learning another language.

In this tutorial, we’ve only covered what was possible using Tensorflow.js, however, the ecosystem of other libraries and tools is growing. More specified frameworks are also available, allowing you to explore using machine learning with other domains such as music with [Magenta.js](https://github.com/tensorflow/magenta-js), or predicting user navigation on a website using [guess.js](https://github.com/guess-js/guess)!

As tools get more performant, the possibilities of building machine learning-enabled applications in JavaScript are likely to be more and more exciting, and now is a good time to learn more about it, as the community is putting effort into making it accessible.

## Further Resources

If you are interested in learning more, here are a few resources:

### Other Frameworks And Tools

- [ml5.js](https://github.com/ml5js/ml5-library)
- [ml.js](https://github.com/mljs)
- [brain.js](https://github.com/BrainJS/brain.js)
- [Keras.js](https://github.com/transcranial/keras-js)
- [PoseNet](https://github.com/tensorflow/tfjs-models/tree/master/posenet)
- [Tensorflow playground](https://playground.tensorflow.org/)

### Examples, Models And Datasets

- [Tensorflow.js models](https://github.com/tensorflow/tfjs-models)
- [Tensorflow.js examples](https://github.com/tensorflow/tfjs-examples/blob/master/mobilenet/imagenet_classes.js)
- [Datasets](https://github.com/tensorflow/datasets/blob/master/docs/datasets.md)

### Inspiration

- [Teachable machine](https://github.com/googlecreativelab/teachable-machine)
- [AI experiments](https://experiments.withgoogle.com/collection/ai)
- [AIJS.rocks](https://aijs.rocks/)
- [Creatability](https://experiments.withgoogle.com/collection/creatability)

Thanks for reading!

{{< signature "rb, dm, yk, il" >}}
