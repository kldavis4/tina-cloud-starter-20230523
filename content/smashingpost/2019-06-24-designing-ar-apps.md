---
title: 'What I Learned From Designing AR Apps'
slug: designing-ar-apps-guide
author: gleb-kuznetsov
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86cfc4e6-eaef-4f66-b271-70dc838a697a/3-ifly-a380-app.png
date: 2019-06-24T12:00:59+02:00
summary: >-
  We are still at the beginning stages of the new technological revolution &mdash; the exciting time when technologies like AR will be an expected part of our daily routines &mdash; and it’s our opportunity to create a solid foundation for the future generation of designers. In this article, Gleb shares his personal experience and advice on how to create and design AR apps.
description: >-
  We are still at the beginning stages of the new technological revolution &mdash; the exciting time when technologies like AR will be an expected part of our daily routines &mdash; and it’s our opportunity to create a solid foundation for the future generation of designers.
categories:
  - Apps
  - Augmented Reality
  - Interaction Design
---
<p>The digital and technological landscape is constantly changing &mdash; new products and technologies are popping up every day. Designers have to keep track of what is trending and where creative opportunities are. A great designer has the vision to analyze new technology, identify its potential, and use it to design better products or services.</p>

<p>Among the various technologies that we have today, there’s one that gets a lot of attention: Augmented Reality. Companies like Apple and Google realize the potential of AR and invest significant amounts of resources into this technology. But when it comes to creating an AR experience, many designers find themselves in unfamiliar territory. Does AR require a different kind of UX and design process?</p>

<p>As for me, I’m a big fan of learning-by-doing, and I was lucky enough to work on the Airbus mobile app as well as the Rokid AR glasses OS product design. I’ve established a few practical rules that will help designers to get started creating compelling AR experiences. The rules work both for mobile augmented reality (MAR) and AR glasses experiences.</p>

{{< vimeo id="344048679" caption="Rokid Glasses motion design exploration by <a href='https://dribbble.com/glebich'>Gleb Kuznetsov</a>" >}}

## Glossary

<p>Let’s quickly define the key terms that we will use in the article:</p>

<ul>
  <li>Mobile Augmented Reality (MAR) is delivering augmented reality experienced on mobile devices (smartphones and tablets);</li>
  <li>AR Glasses are a wearable smart display with a see-through viewing an augmented reality experience.</li>
</ul>

## 1. Get Buy-In From Stakeholders

<p>Similar to any other project you work for, it is vital that you get support from stakeholders as early in the process as is possible. Despite being buzzed about for years, many stakeholders have never used AR products. As a result, they can question the technology just because they don’t understand the value it delivers. Our objective is to get an agreement from them.</p>

<p>“Why do we want to use AR? What problem does it solve?” are questions that stakeholders ask when they evaluate the design. It’s vital to connect your design decisions to the goals and objectives of the business. Before reaching stakeholders, you need to evaluate your product for AR potential. Here are three areas where AR can bring a lot of value:</p>

<ul>
  <li><strong>Business Goals</strong><br />Understand the business goals you're trying to solve for using AR. Stakeholders always appreciate connecting design solutions to the goals of the business. A lot of time business will respond to quantifiable numbers. Thus, be ready to provide an explanation off how your design is intended to help the company make more money or save more money.</li>
  <li><strong>Helpfulness For Users</strong><br />AR will provide a better user experience and make the user journey a lot easier. Stakeholders appreciate technologies that improve the main use of the app. Think about the specific value that AR brings to users.</li>
  <li><strong>Creativity</strong><br />AR is excellent when it comes to creating a more memorable experience and improving the design language of a product. Businesses often have a specific image they are trying to portrait, and product design has to reflect this.</li>
</ul>

<p>Only when you have a clear answer to the question “Why is this better with AR?”, you will need to share your thoughts with stakeholders. Invest your time in preparing a presentation. Seeing is believing, and you’ll have better chances of buy-in from management when you show a demo for them. The demo should make it clear what are you proposing.</p>

{{% feature-panel %}}

## 2. Discovery And Ideation

### Explore And Use Solutions From Other Fields

<p>No matter what product you design, you have to spend enough time researching the subject. When it comes to designing for AR, look for innovations and successful examples with similar solutions from other industries. For example, when my team was designing audio output for AR glasses, we learned a lot from headphones and speakers on mobile phones.</p>

### Design User Journey Using “As A User I Want” Technique

<p>One of the fundamental things you should remember when designing AR experiences is that AR exists outside of the phone or glasses. AR technology is just a medium that people use to receive information. The tasks that users want to accomplish using this technology are what is really important.</p>

<p>“How to define a key feature set and be sure it will be valuable for our users?” is a crucial question you need to answer before designing your product. Since the core idea of user-centered design is to keep the user in the center, your design must be based on the understanding of users, their goals and contexts of use. In other words, we need to embrace the user journey.</p>

<p>When I work on a new project, I use a simple technique “<em>As a [type of user], I want [goal] because [reason].</em>” I put myself in the user's shoes and think about what will be valuable for them. This technique is handy during brainstorming sessions. Used together with storyboarding, it allows you to explore various scenarios of interaction.</p>

<p>In the article “<a href="https://uxplanet.org/designing-tomorrow-today-the-airbus-iflya380-app-b63eb0633484"><em>Designing Tomorrow Today: the Airbus iflyA380 App</em></a>,” I’ve described in detail the process that my team followed when we created the app. The critical element of the design process was getting into the passenger’s mind, looking for insights into what the best user experience would be before, during and after their flight.</p>

<p>To understand what travelers like and dislike about the travel experience, we held a lot of brainstorming sessions together with Airbus. Those sessions revealed a lot of valuable insights. For example, we found that visiting the cabin (from home) before flying on the A380 was one of the common things users want to do. The app uses augmented reality so people can explore the cabin and virtually visit the upper deck, the cockpit, the lounges &mdash; wherever they want to go &mdash; even before boarding the plane.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fd9170e-b48f-474f-97ba-a4b13f301cc2/2-ifly-a380-ios-app-design.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fd9170e-b48f-474f-97ba-a4b13f301cc2/2-ifly-a380-ios-app-design.gif" width="800" height="" alt="IFLY A380 iOS app design by Gleb Kuznetsov" /></a><figcaption>IFLY A380 iOS app design by <a href="https://dribbble.com/glebich">Gleb Kuznetsov</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fd9170e-b48f-474f-97ba-a4b13f301cc2/2-ifly-a380-ios-app-design.gif">Large preview</a>)</figcaption></figure>

<p>App also accompanies passengers from the beginning to the end of their journey &mdash; basically, everything a traveler wants to do with the trip is wrapped up in a single app. Finding your seat is one of the features we implemented. This feature uses AR to show your seat in a plane. As a frequent traveler, I love that feature; you don’t need to search for the place at the time when you enter the cabin, you can do it beforehand &mdash; from the comfort of your couch. Users can access this feature right from the boarding pass &mdash; by tapping on ‘glass’ icon.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86cfc4e6-eaef-4f66-b271-70dc838a697a/3-ifly-a380-app.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86cfc4e6-eaef-4f66-b271-70dc838a697a/3-ifly-a380-app.png" sizes="100vw" caption="IFLY A380 app users can access the AR feature by tapping on the ‘glass’ icon. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86cfc4e6-eaef-4f66-b271-70dc838a697a/3-ifly-a380-app.png'>Large preview</a>)" alt="IFLY A380 app users can access the AR feature by tapping on the ‘glass’ icon" >}}

### Narrow Down Use Cases

<p>It might be tempting to use AR to solve a few different problems for users. But in many cases, it’s better to resist this temptation. Why? Because by adding too many features in your product, you make it not only more complex but also more expensive. This rule is even more critical for AR experience that generally requires more effort. It’s always better to start with simple but well-designed AR experience rather than multiple complex but loose designed AR experiences.</p>

<p>Here are two simple rules to follow:</p>

<ul>
  <li>Prioritize the problems and focus on the critical ones.</li>
  <li>Use storyboarding to understand exactly how users will interact with your app.</li>
<li>Remember to be realistic. Being realistic means that you need to strike a balance between creativity and technical capabilities.</li>
</ul>

### Use Prototypes To Assess Ideas

<p>When we design traditional apps, we often use static sketches to assess ideas. But this approach won’t work for AR apps.</p>

{{% pull-quote %}}
Understanding whether a particular idea is good or bad cannot be captured from a static sketch; quite often the ideas that look great on paper don’t work in a real-life context.
{{% /pull-quote %}}

<p>Thus, we need to interact with a prototype to get this understanding. That’s why it’s essential to get to prototyping state as soon as possible.</p>

<p>It’s important to mention that when I say ‘prototyping state’ I don’t mean a state when you create a polished high-fidelity prototype of your product that looks and work as a real product. What I mean is using a technique of rapid prototyping and building a prototype that helps you experience the interaction. You need to make prototypes really fast &mdash; remember that the goal of rapid prototyping is in evaluating your ideas, not in demonstrating your skills as a visual designer.</p>

{{% ad-panel-leaderboard %}}

## 3. Design

<p>Similar to any other product you design, when you work on AR product, your ultimate goal is to create intuitive, engaging, and clean interface. But it can be challenging since the interface in AR apps accounts both for input and output.</p>

### Physical Environment

<p>AR is inherently an environmental medium. That’s why the first step in designing AR experience is defining where the user will be using your app. It’s vital to select the environment up front. And when I say ‘environment’, I mean a physical environment where the user will experience the app &mdash; it could be indoors or outdoors.</p>

<p>Here are three crucial moments that you should consider:</p>

<ol>
<li>How much space users need to experience AR? Users should have a clear understanding of the amount of space they’ll need for your app. Help users understand the ideal conditions for using the app before they start the experience.</li>
<li>Anticipate that people will use your app in environments that aren’t optimal for AR. Most physical environments can have limitations. For example, your app is AR table tennis game but your users might not have a large horizontal surface. In this case, you might want to use a virtual table generated based on your device orientation.</li>
<li>Light estimation is essential. Your app should analyze the environment automatically and provide contextual guidance if the environment is not good enough. If the environment is too dark or too bright for your app, tell the user that they should find a better place to use your app. ARCore and ARKit have a built-in system for light estimation.</li>
</ol>

<p>When my team designed Airbus i380 mobile AR experience, we took the available physical space into account. Also, we’ve considered the other aspects of interaction, such as the speed at which the user should make decisions. For instance, the user who wants to find her seat during the boarding won’t have too much time.</p>

<p>We sketched the environment (in our case, it was a plane inside and outside) and put AR objects in our sketch. By making our ideas tangible, we got an understanding of how the user will want to interact with our app and how our app will adapt to the constraints of the environment.</p>

### AR Realism And AR Objects Aesthetics

<p>After you define the environment and required properties, you will need to design AR objects. One of the goals behind creating AR experience is to blend virtual with real. The objects you design should fit into the environment &mdash; people should believe that AR objects are real. That’s why it’s important to render digital content in context with the highest levels of realism.</p>

<p>Here are a few rules to follow:</p>

<ul>
<li>Focus on the level of details and design 3D assets with lifelike textures. I recommend using multi-layer texture model such as PBR (Physically Based Rendering model). Most AR development tools support it, and this is the most cost-effective solution to achieve an advanced degree of detail for your AR objects.</li>
<li>Get the lighting right. Lighting is a very crucial factor for creating realism &mdash; the wrong light instantly breaks the immersion. Use dynamic lighting, reflect environmental lighting conditions on virtual objects, cast object shadows, and reflections on real-world surfaces to create more realistic objects. Also, your app should <a href="https://designguidelines.withgoogle.com/ar-design/content/realism.html#realism-normal-maps">react to real-world changing of lighting</a>.</li>
<li>Minimize the size of textures. Mobile devices are generally less powerful than desktops. Thus, to let your scene load faster, don’t make textures too large. Strive to use 2k resolution at most.</li>
<li>Add visual noise to AR textures. Flat-colored surfaces will look fake to the user's eye. Textures will appear more lifelike when you introduce rips, pattern disruptions, and other forms of visual noise.</li>
<li>Prevent flickering. Update the scene 60 times per second to prevent flickering of AR objects.</li>
</ul>

{{% ad-panel-leaderboard %}}

### Design For Safety And Comfort

<p>AR usually accompanied by the word ‘immersive.’ Creating immersive experience is a great goal, but AR immersion can be dangerous &mdash; people can be so immersed in smartphones/glasses, so they forget what is happening around them, and this can cause problems. Users might not notice hazards around them and bump into objects. This phenomenon is known as cognitive tunneling. And it caused a lot of physical traumas.</p>

<ul>
<li>Avoid users from doing anything uncomfortable &mdash; for example, physically demanding actions or rapid/expansive motion.</li>
  <li>Keep the user safe. Avoid situations when users have to walk backward.</li>
<li>Avoid long play AR sessions. Users can get fatigued using AR for extended periods. Design stop points and in-app notifications that they should take a break. For instance, if you design an AR game, let users pause or save their progress.</li>
</ul>

### Placement For Virtual Objects

<p>There are two ways of placing virtual objects &mdash; on the screen or in the world. Depending on the needs of your project and device capabilities, you can follow either the first or second approach. Generally, virtual elements should be placed in world space if they suppose to act like real objects (e.g., a virtual statue in AR space), and should be placed as an on-screen overlay if they intended to be UI controls or information messages (e.g., notification).</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed32c74d-589c-4541-9106-45011d0ec1e5/4-rokid-glasses.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed32c74d-589c-4541-9106-45011d0ec1e5/4-rokid-glasses.png" sizes="100vw" caption="Rokid Glasses. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed32c74d-589c-4541-9106-45011d0ec1e5/4-rokid-glasses.png'>Large preview</a>)" alt="Rokid Glasses" >}}

<p>‘Should every object in AR space be 3D?’ is a common question among designers who work on AR experiences. The answer is no. Not everything in the AR space should be 3D. In fact, in some cases like in-app notifications, it's preferable to use flat 2D objects because they will be less visually distracting.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08a20a06-54d1-4f5f-8d73-b2925e810789/5-rokid-glasses-motion-design-exploration.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08a20a06-54d1-4f5f-8d73-b2925e810789/5-rokid-glasses-motion-design-exploration.gif" width="800" height="600" alt="Rokid Glasses motion design exploration by Gleb Kuznetsov" /></a><figcaption>Rokid Glasses motion design exploration by <a href="https://dribbble.com/glebich">Gleb Kuznetsov</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08a20a06-54d1-4f5f-8d73-b2925e810789/5-rokid-glasses-motion-design-exploration.gif">Large preview</a>)</figcaption></figure>

### Avoid Using Haptic Feedback

<p>Phone vibrations are frequently used to send feedback in mobile apps. But using the same approach in AR can cause a lot of problems &mdash; haptic feedback introduces extra noise and makes the experience less enjoyable (especially for AR Glasses users). In most cases, it’s better to use sound effect for feedback.</p>

### Make A Clear Transition Into AR

<p>Both for MAR and AR glass experiences, you should let users know they’re about to transition into AR. Design a transition state. For the ifly380 app, we used an animated transition &mdash; a simple animated effect that user sees when taps on the AR mode icon.</p>

<p>Trim all the fat.</p>

<p>Devote as much of the screen as possible to viewing the physical world and your app's virtual objects:</p>

<ul>
<li>Reduce the total number of interactable elements on the screen available for the user at one moment of time.</li>
<li>Avoid placing visible UI controls and text messages in your viewport unless they are necessary for the interaction. A visually clean UI lends itself seamlessly to the immersive experience you’re building.</li>
<li>Prevent distractions. Limit the number of times when objects appear on the user screen out of the blue. Anything that appears out of the blue instantly kills realism and make the user focus on the object.</li>
</ul>

{{< vimeo id="283909154" >}}

### AR Object Manipulation And Delineating Boundaries Between The ‘Augment’ And The ‘Reality’

<p>When it comes to designing a mechanism of interaction with virtual objects, favor direct manipulation for virtual objects &mdash; the user should be able to touch an object on the screen and interact with it using standard, familiar gestures, rather than interact with separate visible UI controls.</p>

<p>Also, users should have a clear understanding of what elements they can interact with and what elements are static. Make it easy for users to spot interactive objects and then interact with them by providing visual signifiers for interactive objects. Use glowing outlines or other visual highlights to let users know what’s interactive.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dbcf771-47a4-4aa9-af00-bb3e4535f7c5/6-scan-object-effect-for-outdoor-mar.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dbcf771-47a4-4aa9-af00-bb3e4535f7c5/6-scan-object-effect-for-outdoor-mar.gif" width="800" height="600" alt="Scan object effect for outdoor MAR by Gleb Kuznetsov" /></a><figcaption>Scan object effect for outdoor MAR by Gleb Kuznetsov. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dbcf771-47a4-4aa9-af00-bb3e4535f7c5/6-scan-object-effect-for-outdoor-mar.gif">Large preview</a>)</figcaption></figure>

<p>When the user interacts with an object, you need to communicate that the object is selected visually. Design a selection state &mdash; use either highlight the entire object or space underneath it to give the user a clear indication that it’s selected.</p>

<p>Last but not least, follows the rules of physics for objects. Just like real objects, AR objects should react to the real-world environment.</p>

### Design For Freedom Of Camera

<p>AR invites movement and motion from the user. One of the significant challenges when designing or AR is giving users the ability to control the camera. When you give users the ability to control the view, they will swing device around in an attempt to find the points of interest. And not all apps are designed to help the user to control the viewfinder.</p>

<p>Google identifies <a href="https://designguidelines.withgoogle.com/ar-design/user/movement.html#movement-encourage-movement">four different ways that a user can move in AR space</a>:</p>

<ol>
  <li>Seated, with hands fixed.</li>
  <li>Seated, with hands moving.</li>
  <li>Standing still, with hands fixed.</li>
  <li>Moving around in a real-world space.</li>
</ol>

<p>The first three ways are common for mobile AR while the last one is common for AR glasses.</p>

<p>In some cases, MAR users want to rotate the device for ease of use. Don’t interrupt the camera with rotation animation.</p>

### Consider Accessibility When Designing AR

<p>As with any other product we design, our goal is to make augmented reality technology accessible for people. Here are a few general recommendations on how to address real-world accessibility issues:</p>

<ul>
<li>Blind users. Visual information is not accessible to blind users. To make AR accessible for blind users, you might want to use audio or haptic feedback to deliver navigation instructions and other important information.</li>
<li>Deaf or hard-hearing users. For AR experience that requires voice interaction, you can use visual signals as an input method (also known as speechreading). The app can learn to analyze lip movement and translate this data in commands.</li>
</ul>

<p>If you're interested in learning more practical tips on how to create accessible AR apps, consider watching the video talk by Leah Findlater:</p>

<figure class="video-container"><iframe loading="lazy" src="https://www.youtube.com/embed/lBq-WjXmTDo" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

### Encourage Users To Move

<p>If your experience demands exploration, remind users they can move around. Many users have never experienced a 360-degree virtual environment before, and you need to motivate them to change the position of their device. You can use an interactive object to do that. For example, during I/0 2018, Google used an animated fox for Google Maps that guided users to the target destination.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fdc7339-8fee-43df-8ec3-efae02b9f152/7-ar-experience.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fdc7339-8fee-43df-8ec3-efae02b9f152/7-ar-experience.png" sizes="100vw" caption="This AR experience uses an animated bird to guide users. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fdc7339-8fee-43df-8ec3-efae02b9f152/7-ar-experience.png'>Large preview</a>)" alt="This AR experience uses an animated bird to guide users" >}}

### Remember That Animation Is A Designer’s Best Friend

<p>Animation can be multipurpose. First, you can use a combination of visual cues and animation to teach users. For example, the animation of a moving phone around will make it clear what users have to do to initialize the app.</p>

<p>Second, you can use animation to create emotions.</p>

{{% pull-quote %}}
One second of emotion can change the whole reality for people engaging with a product.
{{% /pull-quote %}}

<p>Well-designed animated effects help to create a connection between the user and the product &mdash; they make the object feel tangible. Even a simple object such as loading indicator can build a bridge of trust between users and the device.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18f99658-39c9-48d4-87f7-e24773f05f62/8-rokid-alien-motion-design.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18f99658-39c9-48d4-87f7-e24773f05f62/8-rokid-alien-motion-design.gif" width="800" height="600" alt="Rokid Alien motion design by Gleb Kuznetsov" /></a><figcaption>Rokid Alien motion design by <a href="https://dribbble.com/glebich">Gleb Kuznetsov</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18f99658-39c9-48d4-87f7-e24773f05f62/8-rokid-alien-motion-design.gif">Large preview</a>)</figcaption></figure>

<p>A critical moment about animation &mdash; after discovering the elements of design and finding design solutions for the animation base, it’s essential to spend enough time on creating a proper animated effect. It took lots of iterations to finish a loading animation that you see above. You have to test every animation to be sure it works for your design and be ready to adjust color, positioning, etc. to give the best effect.</p>

<figure class="video-container"><iframe loading="lazy" src="https://www.youtube.com/embed/pybMYmJ2Kko" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

### Prototype On The Actual Device

<p>In the <a href="https://uxplanet.org/top-designers-you-need-to-know-an-interview-with-gleb-kuznetsov-and-jeshua-nanthakumar-5572dcae8df9">interview for Rokid team</a>, Jeshua Nanthakumar mentioned that the most effective AR prototypes are always physical. That’s because when you prototype on the actual device, from the beginning, you make design work well on hardware and software that people actually use. When it comes to unique displays like on the Rokid Glasses, this methodology is especially important. By doing that you’ll ensure your design is implementable.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d87034b-5600-462f-8671-822448ba66d8/9-motion-design-language-exploration.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d87034b-5600-462f-8671-822448ba66d8/9-motion-design-language-exploration.gif" width="800" height="600" alt="Motion design language exploration for AR Glasses Rokid by Gleb Kuznetsov" /></a><figcaption>Motion design language exploration for AR Glasses Rokid by Gleb Kuznetsov. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d87034b-5600-462f-8671-822448ba66d8/9-motion-design-language-exploration.gif">Large preview</a>)</figcaption></figure>

<p>My team was responsible for designing the AR motion design language and loading animation for AR glasses. We decided to use a 3D sphere that will be rotated during the loading and will have nice reflections on its edges. The design of the animated effect took two weeks of hard work of motion designers and it looked gorgeous on high-res monitors of our design team, but the final result wasn’t good enough because the animation caused motion sickness.</p>

{{< vimeo id="344054417" >}}

<p>Motion sickness often caused by the discrepancies between the motion perceived from the screen of AR Glasses and the actual movement of the user's head. But in our case, the root cause of the motion sickness was different &mdash; since we put a lot of attention in polishing details like shapes, reflections, etc.  unintentionally we made users focus on those details while the sphere was moving.</p>

<p>As a result, the motion happened in the periphery, and since humans are more sensitive to the moving objects in the periphery this caused motion sickness. We solved this problem by simplifying the animation. But it’s critical to mention that we won’t be able to find this problem without testing on the actual device.</p>

<p>If we compare the actual procedure of testing of AR apps with traditional GUI apps, it will be evident that testing AR apps require more manual interactions. A person who conducts testing should determine whether the app provides the correct output based on the current context.</p>

<p>Here are a few tips that I have for conducting efficient usability testing sessions:</p>

<ul>
<li>Prepare a physical environment to test in. Try to create real-world conditions for your app &mdash; test it with various physical objects, in different scenes with different lighting. But the environment might not be limited to scene and lighting.</li>
<li>Don’t try to test everything all at once. Use a technique of chunking. Breaking down a complex flow into smaller pieces and testing them separately is always beneficial.</li>
<li>Always record your testing session. Record everything that you see in the AR glass. A session record will be beneficial during discussions with your team.</li>
  <li>Testing for motion sickness.</li>
<li>Share your testing results with developers. Try to mitigate the gap between design and development. Make sure your engineering team knows what problem you face.</li>
</ul>

## Conclusion

<p>Similar to any other new technology, AR comes with many unknowns. Designers who work on AR projects have a role of explorers &mdash; they experiment and try various approaches in order to find the one that works best for their product and delivers the value for people who will use it.</p>

<p>Personally, I believe that it’s always great to explore new mediums and find new original ways of solving old problems. We are still at the beginning stages of the new technological revolution &mdash; the exciting time when technologies like AR will be an expected part of our daily routines &mdash; and it’s our opportunity to create a solid foundation for the future generation of designers.</p>

{{< signature "cc, yk, il" >}}
