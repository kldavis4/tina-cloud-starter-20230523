---
title: 'Powerful Image Analysis With Google Cloud Vision And Python'
slug: powerful-image-analysis-google-cloud-vision-python
author: bartosz-biskupski
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2bd806f-bd5d-49be-a3ab-12c7f57440cf/sharing-card-bartosz.png
date: 2019-01-09T13:45:32+01:00
summary: >-
  The scope of possibilities to apply Google Cloud Vision service is practically endless. With Python Library available, it can certainly help you bring out deeper interest in Machine Learning technologies.
description: >-
  The scope of possibilities to apply Google Cloud Vision is endless. With Python Library available, it can help you bring out deeper interest in Machine Learning technologies.
categories:
  - Experience Design
  - Machine Learning
  - API
  - Apps
---
Quite recently, I’ve built a web app to manage user’s personal expenses. Its main features are to scan shopping receipts and extract data for further processing. Google Vision API turned out to be a great tool to get a text from a photo. In this article, I will guide you through the development process with Python in a sample project. 

If you’re a novice, don’t worry. You will only need a very basic knowledge of this programming language &mdash; with no other skills required.

Let’s get started, shall we?

## Never Heard Of Google Cloud Vision?

It’s an API that allows developers to analyze the content of an image through extracted data. For this purpose, Google utilizes machine learning models trained on a large dataset of images. All of that is available with a single API request. The engine behind the API classifies images, detects objects, people’s faces, and recognizes printed words within images. 

To give you an example, let’s bring up the well-liked [Giphy](https://giphy.com). They’ve adopted the API to extract caption data from GIFs, what resulted in significant improvement in user experience. Another example is [realtor.com](https://Realtor.com), which uses the Vision API’s OCR to extract text from images of For Sale signs taken on a mobile app to provide more details on the property.

## Machine Learning At A Glance

Let’s start with answering the question many of you have probably heard before &mdash; what is the Machine Learning?

The broad idea is to develop a programmable model that finds patterns in the data its given. The higher quality data you deliver and the better the design of the model you use, the smarter outcome will be produced. With 'friendly machine learning' (as Google calls their Machine Learning through API services), you can easily incorporate a chunk of Artificial Intelligence into your applications.

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2018/09/getting-started-with-machine-learning/">Getting Started With Machine Learning</a></em></p>

{{% feature-panel %}}

## How To Get Started With Google Cloud

Let’s start with the registration to Google Cloud. Google requires authentication, but it’s simple and painless &mdash; you’ll only need to store a JSON file that’s including API key, which you can get directly from the [Google Cloud Platform](https://console.cloud.google.com/apis/credentials/serviceaccountkey). 

Download the file and add it’s path to environment variables:

<div class="break-out">

<pre><code class="language-python">export GOOGLE_APPLICATION_CREDENTIALS=/path/to/your/apikey.json
</code></pre></div>

Alternatively, in development, you can support yourself with the `from_serivce_account_json()` method, which I’ll describe further in this article. To learn more about authentication, check out [Cloud’s official documentation](https://googleapis.github.io/google-cloud-python/latest/core/auth.html). 

Google provides a Python package to deal with the API. Let’s add the latest version of **google-cloud-vision==0.33** to your app. Time to code!

### How To Combine Google Cloud Vision With Python

Firstly, let’s import classes from the library.

<pre><code class="language-python">from google.cloud import vision
from google.cloud.vision import types
</code></pre>

When that’s taken care of, now you’ll need an instance of a client. To do so, you’re going to use a text recognition feature.

<pre><code class="language-python">client = vision.ImageAnnotatorClient()
</code></pre>

If you won’t store your credentials in environment variables, at this stage you can add it directly to the client.

<div class="break-out">

<pre><code class="language-python">client = vision.ImageAnnotatorClient.from_service_account_file(
'/path/to/apikey.json'
)
</code></pre></div>

Assuming that you store images to be processed in a folder 'images' inside your project catalog, let’s open one of them.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7669b141-9ff9-47e6-b56b-2bb1ff6e0d72/receipt-example-processed-by-google-cloud-vision.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7669b141-9ff9-47e6-b56b-2bb1ff6e0d72/receipt-example-processed-by-google-cloud-vision.png" sizes="100vw" caption="An example of a simple receipt that could be processed by Google Cloud Vision. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7669b141-9ff9-47e6-b56b-2bb1ff6e0d72/receipt-example-processed-by-google-cloud-vision.png'>Large preview</a>)" alt="Image of receipt that could be processed by Google Cloud Vision" >}}

<pre><code class="language-python">image_to_open = 'images/receipt.jpg'

with open(image_to_open, 'rb') as image_file:
    content = image_file.read()
</code></pre>

Next step is to create a Vision object, which will allow you to send a request to proceed with text recognition.

<pre><code class="language-python">image = vision.types.Image(content=content)

text_response = client.text_detection(image=image)
</code></pre>

The response consists of detected words stored as description keys, their location on the image, and a language prediction. For example, let’s take a closer look at the first word:

<pre><code class="language-python">[
...
description: "SHOPPING"
bounding_poly {
  vertices {
    x: 1327
    y: 1513
  }
  vertices {
    x: 1789
    y: 1345
  }
  vertices {
    x: 1821
    y: 1432
  }
  vertices {
    x: 1359
    y: 1600
  }
}
...
]
</code></pre>

As you can see, to filter text only, you need to get a description "on all the elements". Luckily, with help comes Python’s powerful list comprehension. 

<div class="break-out">

<pre><code class="language-python">texts = [text.description for text in text_response.text_annotations]

['SHOPPING STORE\nREG 12-21\n03:22 PM\nCLERK 2\n618\n1 MISC\n1 STUFF\n$0.49\n$7.99\n$8.48\n$0.74\nSUBTOTAL\nTAX\nTOTAL\nCASH\n6\n$9. 22\n$10.00\nCHANGE\n$0.78\nNO REFUNDS\nNO EXCHANGES\nNO RETURNS\n', 'SHOPPING', 'STORE', 'REG', '12-21', '03:22', 'PM', 'CLERK', '2', '618', '1', 'MISC', '1', 'STUFF', '$0.49', '$7.99', '$8.48', '$0.74', 'SUBTOTAL', 'TAX', 'TOTAL', 'CASH', '6', '$9.', '22', '$10.00', 'CHANGE', '$0.78', 'NO', 'REFUNDS', 'NO', 'EXCHANGES', 'NO', 'RETURNS']
</code></pre></div>

If you look carefully, you can notice that the first element of the list contains all text detected in the image stored as a string, while the others are separated words. Let’s print it out.

<pre><code class="language-python">print(texts[0])

SHOPPING STORE
REG 12-21
03:22 PM
CLERK 2
618
1 MISC
1 STUFF
$0.49
$7.99
$8.48
$0.74
SUBTOTAL
TAX
TOTAL
CASH
6
$9. 22
$10.00
CHANGE
$0.78
NO REFUNDS
NO EXCHANGES
NO RETURNS
</code></pre>

Pretty accurate, right? And obviously quite useful, so let’s play more.

{{% ad-panel-leaderboard %}}

## What Can You Get From Google Cloud Vision?

As I’ve mentioned above, Google Cloud Vision it’s not only about recognizing text, but also it lets you discover faces, landmarks, image properties, and web connections. With that in mind, let's find out what it can tell you about web associations of the image.

<pre><code class="language-python">web_response = client.web_detection(image=image)
</code></pre>

Okay Google, do you actually know what is shown on the image you received?

<pre><code class="language-python">web_content = web_response.web_detection
web_content.best_guess_labels
>>> [label: "Receipt"]
</code></pre>

Good job, Google! It’s a receipt indeed. But let’s give you a bit more exercise &mdash; can you see anything else? How about more predictions expressed in percentage?

<div class="break-out">

<pre><code class="language-python">predictions = [
(entity.description, '{:.2%}'.format(entity.score))) for entity in web_content.web_entities
]

>>> [('Receipt', '70.26%'), ('Product design', '64.24%'), ('Money', '56.54%'), ('Shopping', '55.86%'), ('Design', '54.62%'), ('Brand', '54.01%'), ('Font', '53.20%'), ('Product', '51.55%'), ('Image', '38.82%')]
</code></pre></div>

Lots of valuable insights, well done, my almighty friend! Can you also find out where the image comes from and whether it has any copies?

<div class="break-out">

<pre><code class="language-python">web_content.full_matching_images
 >>> [
url: "https://www.rcapitalassociates.com/wp-content/uploads/2018/03/receipts.jpg", 
url:"https://media.istockphoto.com/photos/shopping-receipt-picture-id901964616?k=6&m=901964616&s=612x612&w=0&h=RmFpYy9uDazil1H9aXkkrAOlCb0lQ-bHaFpdpl76o9A=", 
url: "https://www.pakstat.com.au/site/assets/files/1172/shutterstock_573065707.500x500.jpg"
]
</code></pre></div>

I’m impressed. Thanks, Google! But one is not enough, can you please give me three examples of similar images? 

<div class="break-out">

<pre><code class="language-python">web_content.visually_similar_images[:3]
>>>[
url: "https://thumbs.dreamstime.com/z/shopping-receipt-paper-sales-isolated-white-background-85651861.jpg", 
url: "https://thumbs.dreamstime.com/b/grocery-receipt-23403878.jpg", 
url:"https://image.shutterstock.com/image-photo/closeup-grocery-shopping-receipt-260nw-95237158.jpg"
]
</code></pre></div>

Sweet! Well done.

## Is There Really An Artificial Intelligence In Google Cloud Vision?

As you can see in the image below, dealing with receipts can get a bit emotional.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1dd88e1-aa68-41f0-a879-f6a46d557bcf/example-stress-receipt.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1dd88e1-aa68-41f0-a879-f6a46d557bcf/example-stress-receipt.jpg" sizes="100vw" caption="An example of stress you can experience while getting a receipt. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1dd88e1-aa68-41f0-a879-f6a46d557bcf/example-stress-receipt.jpg'>Large preview</a>)" alt="Man screaming and looking stressed while holding a long receipt" >}}

Let’s have a look at what the Vision API can tell you about this photo.

<div class="break-out">

<pre><code class="language-python">image_to_open = 'images/face.jpg'

with open(image_to_open, 'rb') as image_file:
    content = image_file.read()
image = vision.types.Image(content=content)

face_response = client.face_detection(image=image)
face_content = face_response.face_annotations

face_content[0].detection_confidence
>>> 0.5153166651725769
</code></pre></div>

Not too bad, the algorithm is more than 50% sure that there is a face in the picture. But can you learn anything about the emotions behind it?

<pre><code class="language-python">face_content[0]
>>> [
...
joy_likelihood: VERY_UNLIKELY
sorrow_likelihood: VERY_UNLIKELY
anger_likelihood: UNLIKELY
surprise_likelihood: POSSIBLE
under_exposed_likelihood: VERY_UNLIKELY
blurred_likelihood: VERY_UNLIKELY
headwear_likelihood: VERY_UNLIKELY
...
]
</code></pre>

Surprisingly, with a simple command, you can check the likeliness of some basic emotions as well as headwear or photo properties. 

{{% ad-panel-leaderboard %}}

When it comes to the detection of faces, I need to direct your attention to some of the potential issues you may encounter. You need to remember that you’re handing a photo over to a machine and although Google’s API utilizes models trained on huge datasets, it’s possible that it will return some unexpected and misleading results. Online you can find photos showing how easily artificial intelligence can be tricked when it comes to image analysis. Some of them can be found funny, but there is a fine line between innocent and offensive mistakes, especially when a mistake concerns a human face. 

With no doubt, Google Cloud Vision is a robust tool. Moreover, it’s fun to work with. API’s REST architecture and the widely available Python package make it even more accessible for everyone, regardless of how advanced you are in Python development. Just imagine how significantly you can improve your app by utilizing its capabilities!

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2017/04/applications-machine-learning-designers/">Applications Of Machine Learning For Designers</a></em></p>

## How Can You Broaden Your Knowledge On Google Cloud Vision

The scope of possibilities to apply Google Cloud Vision service is practically endless. With Python Library available, you can utilize it in any project based on the language, whether it’s a web application or a scientific project. It can certainly help you bring out deeper interest in Machine Learning technologies.

[Google documentation](https://cloud.google.com/vision/overview/docs/) provides some great ideas on how to apply the Vision API features in practice as well as gives you the possibility to learn more about the Machine Learning. I especially recommend to check out the guide on [how to build an advanced image search app](https://cloud.google.com/solutions/image-search-app-with-cloud-vision). 

One could say that what you’ve seen in this article is like magic. After all, who would've thought that a simple and easily accessible API is backed by such a powerful, scientific tool? All that’s left to do is write a few lines of code, unwind your imagination, and experience the boundless potential of image analysis.

{{< signature "rb, ra, il" >}}
