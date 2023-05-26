---
title: A Definitive Guide To The Android Carousel Design Pattern
slug: android-carousel-design-pattern
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8381af4-ed28-437e-9cd6-7b7c39dd5616/ecomm-3.jpg
date: 2013-02-01T15:07:15.000Z
author: greg-nudelman
description: >-
  One of the best patterns for browsing a small collection of featured products
  is the carousel. Unfortunately, many mobile app implementations do not offer
  an engaging or satisfying carousel experience and are not effective at driving
  conversions.
categories:
  - Mobile
  - Android
  - Design Patterns
---
One of the best patterns for browsing a small collection of featured products is the carousel. Unfortunately, many mobile app implementations do not offer an engaging or satisfying carousel experience and are not effective at driving conversions.

In this article, we’ll use the analogy of a real-world amusement park carousel to explain what makes for an authentically mobile user experience, and we’ll give you the <strong>design, the complete source code and a downloadable mini-app</strong>, which you can use today to add an enjoyable and effective carousel to your own app on phones and tablets.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">C-Swipe: A Solution To Navigation Fragmentation On Android</span>](https://www.smashingmagazine.com/2013/03/c-swipe-navigation-on-android/)
*   [An Exploration Of Carousel Usage On Mobile E-Commerce Websites](https://www.smashingmagazine.com/2015/02/carousel-usage-exploration-on-mobile-e-commerce-websites/)
*   [Dropbox’s Carousel Design Deconstructed](https://www.smashingmagazine.com/2014/08/dropbox-carousel-design-deconstructed-part-1/)
*   [How To Design For Android Tablets](https://www.smashingmagazine.com/2011/08/designing-for-android-tablets/)

## How It Works

The carousel is fairly simple. The customer is able to view several images of products across a row, and they can swipe horizontally across the row to navigate to the next set of products. An arrow indicating the direction of the carousel’s movement is usually provided as a clue to how to interact with it. Optionally, the next set of products in the queue may be partially hidden, creating what we call the “teaser,” indicating that more content will be visible by swiping.

{{% feature-panel %}}

## Example

One excellent example of this pattern is the Amazon app’s home screen.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d78c2e0-1060-4bf5-876d-058ee9bbc611/figure1.png"><img loading="lazy" decoding="async" class="134168" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01c4f3c4-1d4d-4c71-a08e-ea1b2fda7e1d/mobile-figure1-cut.png" alt="Mobile figure 1." width="500" height="432" /></a><br>
<em>The carousel on the home screen of Amazon’s app is excellent. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d78c2e0-1060-4bf5-876d-058ee9bbc611/figure1.png">Larger preview</a>.</em>

This implementation of the carousel uses the teaser method to hint at the required interaction, showing only a small tantalizing glimpse of the naked CAT5E Ethernet cable, which is (and I have this from most reliable sources) completely irresistible to Amazon’s more impressionable customers, who can’t help but swipe across to see more of the naked cable and get to more of the content.</p>

## When And Where To Use It

The carousel is a fantastic pattern to show off featured items and relevant new arrivals. For example, new items matching the customer’s last search in their local area would be a sure winner.

In fact, consider using a carousel any time you have a small set of products (8 to 20 items) that are easily recognizable from just their picture. Augmenting the mostly visual content with a small amount of overlaid text is also sometimes effective. For example, in the screenshot below of the Pulse app on a 7-inch Android tablet, the carousel’s visual content is augmented with a semi-transparent dark-gray overlay, which provides the date and name of the comic. Without this overlay, the thumbnails of the carousel, especially in the first row, could be easily misinterpreted as belonging to a single comic.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69f82968-2d63-4c02-8111-00c87eb539e2/figure2.png"><img loading="lazy" decoding="async" class="134132" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/186a5870-ae7d-4ac1-aa53-76325e3296a8/mobile-figure2.png" alt="mobile_figure2" width="500" height="293" /></a><br>
<em>The visual carousel content with semi-transparent overlay helps with comprehension in the Pulse app. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69f82968-2d63-4c02-8111-00c87eb539e2/figure2.png">Larger preview</a>.</em>

I am a huge fan of semi-transparent layers in mobile design. This example is particularly effective because the overlay on the thumbnails is semi-transparent and thus does not interfere with viewing the thumbnails, all the while augmenting the carousel experience in a way that is both visually appealing and informative. (Well, it does interfere just a bit, but it keeps interference down to a minimum while making best use of the small screen space.) The example also demonstrates that a carousel is an exceptionally great pattern for the large swiping gestures that small and large tablets invite.</p>

## Why Use It?

The carousel is an attractive and still fairly underused control for presenting visual information. It takes full advantage of the multi-touch gesture of swiping available on a mobile device. The carousel is easy and intuitive to operate and takes full advantage of the compressed real estate on mobile devices, where few words are needed to support the content.</p>

## Other Applications

One of the best features of a carousel is that it works well for a wide variety of device sizes and screen resolutions. This includes the ever-tricky horizontal orientation, for which the carousel works even better than in the vertical orientation.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7d20668-db98-494f-a044-73b81d152c23/figure3.png"><img loading="lazy" decoding="async" class="134135" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/500fbc5e-71d5-4c5c-ac37-48a9c54ba1a7/mobile-figure3.png" alt="mobile_figure3" width="500" height="281" /></a><br>
<em>The carousel adjusts to various screen sizes, and it works even better in a horizontal orientation. Pictured here is Amazon’s app. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7d20668-db98-494f-a044-73b81d152c23/figure3.png">Larger preview</a>.</em>

Whereas the usefulness of traditional search results is severely hindered by the lack of vertical space, a well-designed carousel shines by showing off even more inventory.

Also noteworthy is the presence of the “See all” link, which points to the featured products.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25b0f9d8-5e05-47a9-b521-0c0c2c34a97c/figure4.png"><img loading="lazy" decoding="async" class="134139" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0bbb4f8-920a-4a89-b853-1e445c1f9c2d/mobile-figure4.png" alt="mobile_figure4" width="500" height="441" /></a><br>
<em>The “More like this” link in this carousel navigates to a list of search results. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25b0f9d8-5e05-47a9-b521-0c0c2c34a97c/figure4.png">Larger preview</a>.</em>

A “More” link is an excellent idea if your carousel has a small subset of items (8 to 20) that fails to meet the customer’s desires but piques their interest. In this case, the entire carousel control serves as advertising of sorts, enticing the customer to explore the relevant area of Amazon’s massive inventory.</p>

## Caution

As with any pattern, many implementations of the carousel do not feel quite right. One instance is NewEgg’s “Shell shocker” carousel:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dfef941-7859-4e49-ac70-21a9fc96f2d7/figure5.png"><img loading="lazy" decoding="async" class="134142" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8feb3960-a484-4156-ad5a-0dff67df55b6/mobile-figure5.png" alt="mobile_figure5" width="500" height="418" /></a><br>
<em>NewEgg’s carousel has a few issues. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dfef941-7859-4e49-ac70-21a9fc96f2d7/figure5.png">Larger preview</a>.</em>

Some recommendations based on the UX problems in NewEgg’s implementation might help.</p>

### Make the Scrolling Smooth

To begin with, NewEgg’s carousel is structured more like the iTunes cover flow feature on iOS, with a large central element and two partial elements on the periphery of either side.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9fee147-aec6-47e7-b75a-833154b14866/coverflow.png"><img loading="lazy" decoding="async" class="134145" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a1228cb-e050-44e8-9fc5-4fdcc319778d/mobile-coverflow.png" alt="mobile_coverflow" width="500" height="333" /></a><br>
<em>The cover flow screen in iTunes on iOS emphasizes the central element. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9fee147-aec6-47e7-b75a-833154b14866/coverflow.png">Larger preview</a>.</em>

Like Amazon’s carousel, NewEgg’s can be swiped faster to advance more quickly through the list of products. However, NewEgg’s carousel moves very jerkily because of the structure of the central element, making it hard to see the intermediate states while scrolling — a major disadvantage. Seeing the two peripheral elements change is particularly hard — things hop all over the place, instead of smoothly swimming by the way they do in Amazon’s app. Higher-end and traditional carousels accelerate and decelerate smoothly and provide a pleasant, mellow, smooth ride. A carousel should be a high-end visual viewing experience that induces calm in the user, not stress. All parts of the control, including transitions, should behave accordingly and work together smoothly.</p>

### Indicate the Scrolling Direction

NewEgg’s carousel appears to be scrollable in both the left and right directions, causing a confusion: Is this carousel meant to represent a circle? Have I seen everything already, or do I need to keep scrolling? Amazon uses Android 4.0’s standard “blue parallax” visual treatment to signal the end of the line, a much better approach.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6494a411-67ea-44f8-845a-2eab4ad00026/amazon-paralax-treatment.png"><img loading="lazy" decoding="async" class="134172" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cc52979-4cc3-47f9-85e5-eb17c2e1ce06/mobile-amazon-paralax-treatment.png" alt="mobile_amazon_paralax_treatment" width="500" height="351" /></a><br>
<em>Amazon uses Android 4.0’s standard “blue parallax” to signal the boundaries of the carousel ride. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6494a411-67ea-44f8-845a-2eab4ad00026/amazon-paralax-treatment.png">Larger preview</a>.</em>

Just as a real carousel has papier-mâché horses that point you unambiguously in the right direction (you wouldn’t sit backwards on a horse now, would you?), so must your own carousel show which way the ride goes.</p>

### End the Ride Quickly

Good carousel implementations indicate the end of the list with the same parallax treatment seen at the beginning, and they present only 8 to 20 items, after which the ride is over and the customer can get off the carousel. Most importantly, the customer needs to exit the ride with the feeling of still wanting more. By contrast, NewEgg’s carousel seems to go on forever, so the customer does not get off until they feel bored (or, more likely given the jerky transitions, weak in the stomach). A much better approach would be to accompany the last element in the carousel with an obvious built-in “More like this” link, as shown below.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47f285da-3f3d-476f-93f3-fd126f723b4f/figure6.png"><img loading="lazy" decoding="async" class="134147" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ceab24aa-4d97-4b10-90ed-fcb4489fe211/mobile-figure6.png" alt="mobile_figure6" width="500" height="200" /></a><br>
<em>Show a “More like this” tile at the end of the carousel. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47f285da-3f3d-476f-93f3-fd126f723b4f/figure6.png">Larger preview</a>.</em>

A “More like this” link can be used to jump into search results, which are more efficient for scanning large quantities of data and which are more likely to be relevant because of the sheer volume of items. Think of the “More” link as a premium combo ticket that grants admission to all of the remaining delights at the amusement park, conveniently presented after the cheap introductory carousel ride is over. Kind of puts a different spin on the entire carousel pattern, doesn’t it?

### Make Sure Your Horses Look Amazing

No matter how smooth the ride is or how far or how fast the carousel goes, the best carousels have the best-looking horses, period. Make sure your horses (i.e. thumbnails) tell the story you want your audience to be told. For example, Amazon’s thumbnails are much better looking than NewEgg’s, although sometimes even the e-commerce giant screws up the ride, dropping thumbnails entirely:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/920d24a6-c12a-407e-80ba-88ebe4e64ffd/figure7.png"><img loading="lazy" decoding="async" class="134175" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b51fe05-fe77-4825-a6bf-d0ed60213625/mobile-figure7.png" alt="mobile_figure7" width="500" height="386" /></a><br>
<em>Amazon’s carousel sometimes misses thumbnails. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/920d24a6-c12a-407e-80ba-88ebe4e64ffd/figure7.png">Large preview</a>.</em>

It goes without saying that ghost horses make for a terrible ride, even on Halloween (unless you’re the Headless Horseman). Which brings up my next point: some products are just not that visual, making them poor candidates for inclusion in a carousel. A classic example from my first book, <em>Designing Search: UX Strategies for Ecommerce Success</em> (Wiley 2011), is coffee — Peet’s Coffee to be exact. Even though Berkeley, California-based Peet’s makes some of the world’s most divine premium coffee, all of the thumbnails are identical pictures of a generic coffee bag and some spilled beans.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8182cfac-143d-4076-b994-ade4e1990a4a/figure8.png"><img loading="lazy" decoding="async" class="134177" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6463378a-5d38-4d8c-a4db-e9523062a6c0/mobile-figure8.png" alt="mobile_figure8" width="500" height="430" /></a><br>
<em>Some thumbnails, like these coffee bags from Peet’s, are not good candidates for the carousel pattern. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8182cfac-143d-4076-b994-ade4e1990a4a/figure8.png">Large preview</a>.</em>

Carousels are way more fun when the horses are all different; likewise, these generic bean-bag thumbnails are not good candidates for inclusion in a carousel pattern. A much more interesting horse would have been a close-up photo of a bean variety, or a map of a coffee-growing region, or a Tufte-style diagram of coffee taste attributes such as acidity, earthiness and body.

Even for products that have good thumbnails, presenting enough information can be a challenge. Including the right text in the individual tile is especially important for information scent; this could include key specifications such as processor speed, hard drive capacity and so on for the kind of technical gadgets sold by NewEgg. Picking an image resolution that can handle the amount of detail you are trying to show is also key. For example, can you tell what the item below is by looking at the small thumbnail and truncated description?

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ef32636-f60f-4912-8d2c-6defcf83d2bf/figure9.png"><img loading="lazy" decoding="async" class="134179" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a864474d-b668-488a-a018-85b4a0ee1c9d/mobile-figure9.png" alt="mobile_figure9" width="500" height="402" /></a><br>
<em>A small thumbnail and overly short description lead to “pogo-sticking.” <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ef32636-f60f-4912-8d2c-6defcf83d2bf/figure9.png">Large preview</a>.</em>

Only by drilling down into the item do we see that it’s actually a screwdriver set. A larger thumbnail and better description would have helped a great deal and reduced the “pogo-sticking” (i.e. the frustrating navigation back and forth between carousel control and details page), which ruins the entire ride.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56f79cf7-c52a-48ad-bab7-358a1d28192c/figure10.png"><img loading="lazy" decoding="async" class="134181" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65189d51-d4ea-45c5-92cb-b14d734c2788/mobile-figure10.png" alt="mobile_figure10" width="500" height="470" /></a><br>
<em>Having to pogo-stick between the carousel and details page ruins the ride. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56f79cf7-c52a-48ad-bab7-358a1d28192c/figure10.png">Large preview</a>.</em>

If the picture tells only half the story and you have to include a great deal of text, then you might find yourself having to increase the size of the individual element to the point that the carousel is no longer the best choice of presentation. For such items, think twice about whether you even really need a carousel, and whether a simple vertical list (more akin to a themed roller coaster) would make for a better experience.</p>

## Code

Carousel code can be fairly straightforward. One way to implement an ultra-simple demo using Java is shown below. Plugging cute pictures of puppies into the carousel, you should end up with a mini-app that looks something like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/563096d7-e521-404c-9716-a68488091150/figure11.png"><img loading="lazy" decoding="async" class="134183" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9992b73-c0fe-4cf3-a0c3-818afb23ff0c/mobile-figure11.png" alt="mobile_figure11" width="500" height="300" /></a><br>
<em>Mini-app with a puppy carousel. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/563096d7-e521-404c-9716-a68488091150/figure11.png">Large preview</a>.</em>

First, we define how many items to show, and compute the width of the carousel item based on the screen’s width. (You may need to use more sophisticated code that computes a dynamic <code>INTIAL_ITEMS_COUNT</code> if you’d like to accommodate longer carousels for tablet devices.)

<pre><code class="language-javascript">/**
* Define the number of items visible when the carousel is first shown.
*/
private static final float INITIAL_ITEMS_COUNT = 3.5F;

// Compute the width of a carousel item based on the screen width and number of initial items.
final DisplayMetrics displayMetrics = new DisplayMetrics();
getWindowManager().getDefaultDisplay().getMetrics(displayMetrics);
final int imageWidth = (int) (displayMetrics.widthPixels / INITIAL_ITEMS_COUNT);</code></pre>

Next, for the purposes of this demo, we will create a static array of pictures. In a real app, this list would come from a database, of course.

<pre><code class="language-javascript">// Get the array of puppy resources
final TypedArray puppyResourcesTypedArray = getResources().obtainTypedArray(R.array.puppies_array);</code></pre>

Then, we simply populate the carousel with items in the array and display it by overriding the <code>onPostCreate()</code> function. While <code>onPostCreate()</code> is mostly intended for framework use (according to the documentation), we can use it for this simple demo to simplify things a bit.

<pre><code class="language-javascript">// Populate the carousel with items
ImageView imageItem;
for (int i = 0 ; i &lt; puppyResourcesTypedArray.length() ; ++i) {
// Create new ImageView
imageItem = new ImageView(this);

// Set the shadow background
imageItem.setBackgroundResource(R.drawable.shadow);

// Set the image view resource
imageItem.setImageResource(puppyResourcesTypedArray.getResourceId(i, -1));

// Set the size of the image view to the previously computed value
imageItem.setLayoutParams(new LinearLayout.LayoutParams(imageWidth, imageWidth));

/// Add image view to the carousel container
mCarouselContainer.addView(imageItem);
}</code></pre>

This code is provided free of charge and distributed under the <a href="https://www.gnu.org/licenses/gpl.html">GNU General Public License v3</a>. See the <code>README_LICENSE</code> file for details. Download the <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/009e7187-2663-4875-b553-58023e643e5c/carouseldemo.zip">complete source code for the app</a>.</p>

## Try It Out

If you want to see how the carousel app runs, the completed puppy carousel mini-app is available for you to download and try out. To install it, I recommend using an app installer (I use the one made by FunTrigger, which you can get free from the Play market).

Here’s how it works. Connect your Android device to your computer. You should see the Android file-transfer window open automatically. Download the APK source file (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/009e7187-2663-4875-b553-58023e643e5c/carouseldemo.zip">download the entire package</a>), and place it in the “App Installer” directory (you may have to create it).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81ac0849-4a07-4da6-a34b-fcd58c7b9bbb/figure12.png"><img loading="lazy" decoding="async" class="134153" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22da0f26-2f11-4442-8278-d404bd09c9c9/mobile-figure12.png" alt="mobile_figure12" width="500" height="394" /></a><br>
<em>Place the APK file in Android’s file-transfer window. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81ac0849-4a07-4da6-a34b-fcd58c7b9bbb/figure12.png">Large preview</a>.</em>

Now you will be able to launch the app installer on your device, navigate to the right directory, and tap the icon for the APK file that you want to install.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4804714b-e2f0-47ce-bd26-a69290be853f/figure13.png"><img loading="lazy" decoding="async" class="134154" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9dd6d7d-e8ea-495b-ae35-bd7c774ca369/mobile-figure13.png" alt="mobile_figure13" width="500" height="441" /></a><br>
<em>Use the app launcher to install the app. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4804714b-e2f0-47ce-bd26-a69290be853f/figure13.png">Large preview</a>.</em>

After a few customary Android disclaimers, the app will be installed in the normal apps area on your device, and you can launch it from there.</p>

## Conclusion

The carousel pattern is a microcosm of mobile design: deceptively simple. It is also a somewhat new Android pattern, and pitfalls abound. Nevertheless, if you take the time to get it right, the carousel is a fantastic pattern for showing off featured items and relevant new arrivals, as well any items that are highly visual. It dovetails perfectly with the local context by showing new items that match the customer’s last search in their local area. Finally, with the right implementation of the carousel, you will be supporting touch gestures on today’s Android devices to the fullest extent, fitting more products on the screen and making them accessible with a natural swiping gesture.

When designing your carousel control, think of it as you would its real-world namesake, the carnival ride. Make sure your horses look amazing; indicate the scrolling direction; make the scrolling smooth; and end the ride quickly, providing an exit to more of your inventory. We’ve provided you with the Java code and a demo implementation of the carousel pattern, so now you have no excuse not to try it!

{{< signature "al" >}}

