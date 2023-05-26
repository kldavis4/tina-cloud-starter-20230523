---
title: 'Flash vs. Silverlight: What Suits Your Needs Best?'
slug: flash-vs-silverlight-what-suits-your-needs-best
image: null
date: 2009-05-09T13:22:08.000Z
author: muhammad-usama-alam
description: >-
  With the release of Silverlight 1.0 and its subsequent versions, a debate started among designers and developers regarding choosing between Flash and Silverlight. Silverlight faces difficulties in capturing the market because of the maturity of Flash. However, Silverlight has managed to keep up by including certain features that designers and developers have always wanted to see in Flash, such as search engine optimization.
categories:
  - Design
  - Flash
---
In this article, we will discuss some of the <strong>technical differences between Flash and Silverlight</strong> to help you choose the technology that best suits your needs.

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3c231eb-13e4-4c93-803d-228ab70e9708/flash-silverlight.jpg)

{{% feature-panel %}}

## Animation

Flash uses the <strong>frame-based animation model</strong>. In frame-by-frame animation, we create an object for each frame to produce an animation sequence. For example, if you want to move something across the screen in 3 seconds, calculate how many frames 3 seconds will take, then calculate the matrices required for each frame along the way. Keep in mind that the player won’t actually maintain a frame rate unless you embed a blank audio track; otherwise, 3 seconds might turn out to be 2 or 6 or 5.

[![Adobe Flash Animation](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/822d3446-105b-448f-9cb1-2db0372ea66a/flash-frame.jpg)](https://www.webdesigndev.com)

Silverlight is based on the <strong>WPF animation model</strong>, which is time-based instead of frame-based, so you define the start and end conditions, and it figures out how to do it. No need to deal with matrices like with Flash. Also, no need to calculate the positions of objects in various frames.

![Microsoft Silverlight Animation](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/995d8ad7-02ad-429e-8b00-ddd01c559dc7/silverlight-frame.jpg)

## File Size

Flash uses a <strong>compressed format</strong>, and text and images are embedded in the movie, hence the file size of a Flash component is relatively small.

[![Text representation in Adobe Flash](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ef1c466-3350-41a7-b0bc-59ea925072dd/flash-text.jpg)](https://wareseeker.com/)

Silverlight uses <strong>XAML</strong> for its description language, and it is non-compressed, so the size of a Silverlight component is usually larger.

[![Text representation in Microsoft Silverlight](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/433dbe2f-2dc2-4ec8-b444-99dcb6d23c11/silverlight-text.jpg)](https://www.microsoft.com)

## Scripting

<strong>ActionScript</strong> is used to program Flash objects. ActionScript is an object-oriented language with a full range of controls for designing user interfaces. And it can be integrated with back-end technologies that use other languages and frameworks, such as PHP, ASP and Ruby On Rails. It comes with a huge, powerful class library for developing online browser-hosted applications and stand-alone desktop applications.

![Action Script](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abec29fc-d6c5-4ccb-8890-74f0df9a760d/flash-actionscript.jpg)

For Silverlight scripting, you can choose from among a number of programming languages such as <strong>Visual C#.Net and Visual Basic.Net</strong>, including client-side scripting with JavaScript. C# and VB.NET can be used to write managed code that runs on and uses all of the enhancements and capabilities of Microsoft's .NET framework.

[![Visual Basic](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fa091ce-0ddc-4a0e-80dc-4ffe3a27180b/silverlight-script.jpg)](https://joymon.googlepages.com/)

## Video And Audio

Flash supports <strong>multiple video formats</strong>. The latest codec is very high quality, and the bandwidth usage is nice. There is one problem, though: if you create a tool that outputs Flash content, the formats it supports aren’t really used by anyone else. The original video codec, Sorenson’s proprietary H.263 implementation, is a mutant version of H.263. The compression follows the spec fairly closely, but a bunch of features were left out, and you can’t exactly just go find complete specs on how to build your own encoder.

[![Video Codec](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd64304a-2bce-4671-8103-8dd814bb72fc/video-codec.gif)](https://technet.microsoft.com)

Silverlight implements the industry-standard <strong>VC-1 codec</strong> for video, and supports <strong>WMV</strong> and <strong>WMA</strong>. Just about everyone already has Windows Movie Maker, but if someone doesn't, it’s not a big deal because Microsoft makes available a free SDK encoder for producing WMA and WMV. So, not only would you be using formats that people would more likely be able to encode themselves, but Microsoft provides your product with SDKs if you want to do the encoding yourself.</p>

## Sound Processing

ActionScript offers a set of sound classes that can be used to generate and control sound in a movie. You can add sounds from the library while the movie clip is playing and control those sounds. If you do not specify a target when you create a new sound object, there are methods to control sound for the whole movie.

[![Sound Processing](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c19f9587-0822-4127-b457-a6268d474b97/flash-sound.jpg)](https://www.prepresstraining.com/)

Silverlight doesn't have the low-level audio APIs you would need to write an audio application in the browser. It doesn't even support playback of WAV files because .NET has very little audio playback support.</p>

## Accessibility

Flash provides <strong>rich accessibility features</strong> for those who have hearing and vision problems or who rely on keyboard shortcuts. Providing captions for video solves accessibility challenges for people who are deaf and hard of hearing, but people who are blind or have low vision or other physical disabilities need the video playback controls to be keyboard-accessible and to function properly with assistive technologies such as screen readers and screen magnifiers. Users who rely on keyboard access can use a variety of familiar shortcuts to control video. Buttons such as "Play/Pause," "Stop," "Rewind," "Mute" and "Closed Captions" can be tabbed to and activated with the spacebar. Slider controls such as for volume and playhead position controls can be accessed via the arrow keys, and the "Home" and "End" keys can be used to skip directly to the beginning or end of a range. The volume slider also accepts numeric keys to set playback audio levels in one quick step.

[![Accessibility](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34fdf8f4-a473-442b-84a7-ea63a3e05464/silverlight-accessibility1.png)](https://lh5.ggpht.com/_D_LHhy5fi8o/SUQhlbxnK2I/AAAAAAAAADA/E34em8f43fw/WhistlerBlue_thumb.png)

[![Accessibility](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4617513e-0e56-40ed-ae24-27d75ec54923/silverlight-accessibility2.png)](https://lh5.ggpht.com/_D_LHhy5fi8o/SUQhlbxnK2I/AAAAAAAAADA/E34em8f43fw/WhistlerBlue_thumb.png)

[![Accessibility](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53876279-9add-438f-b390-d672bb606673/mac-os.png)](https://lh5.ggpht.com/_D_LHhy5fi8o/SUQhlbxnK2I/AAAAAAAAADA/E34em8f43fw/WhistlerBlue_thumb.png)

Silverlight 3 is the first browser plug-in to provide access to all system colors, allowing people with partial vision to use familiar operating system controls to make changes, such as switching to high-contrast color schemes for ease of readability. These features are far fewer than those provided by Flash.

## Platform Compatibility

Flash supports Windows Vista/XP/2000, Windows Server 2003/2008, Mac OS 10.1/10.5 (PowerPC), Mac OS 10.1/10.5 (Intel), Linux 5, openSUSE 11, Ubuntu 7.10 or later and Solaris 10.

Silverlight supports only Windows Vista/XP/2000, Windows Server 2003/2008, Windows Mobile 6, Mac OS 10.1/10.5 (PowerPC) and Mac OS 10.1/10.5 (Intel). Because Linux and Solaris support is missing, users of those operating systems won't be able to experience Silverlight on their machines.</p>

## Text Representation/SEO

Flash stores fonts using shape definitions and the player doesn't understand TTF, hence we cannot separate the text layer from the movie. Typically the text written on a flash component was not SEO friendly however Adobe has made the modifications to Flash so that it will be indexable, and the search engines have begun to index Flash.

Currently <strong>Google is the only search engine that is noticeably reading Flash files</strong>. They have worked closely with Adobe to develop the right toolset for the Googlebot in order to read the files for indexing. <strong>Yahoo is working on it</strong> and MSN is working with their own format, Silverlight, so they probably won’t be developing the toolset necessary to read Flash files.

To read more about how to make Flash SEO friendly, please read the following articles:

*   [How to SEO Flash](https://www.hochmanconsultants.com/articles/seo-friendly-flash.shtml)
*   [Google learns to crawl Flash](https://googleblog.blogspot.com/2008/06/google-learns-to-crawl-flash.html)

In Silverlight applications, user interfaces are declared in <strong>XAML</strong> and programmed using a subset of the .NET Framework. XAML can be used for marking up the vector graphics and animations. Text is deployed on web server as separate entity and can be read and accessed separately. Textual content created with <strong>Silverlight is searchable and indexable by search engines</strong> as it is not compiled, but represented as text (XAML).</p>

## Supported Image Formats

Flash supports almost <strong>all image formats</strong>.

Silverlight supports only <strong>PNG and JPEG file formats</strong>. Some other file formats are supported by Silverlight but in a limited way. A full list can be found here.</p>

## Socket Programming

The <strong>XMLSocket object implements client sockets</strong> that allow computers running the Flash player to communicate with a server computer identified by an IP address or domain name.

To use the XMLSocket object, the server computer must run a daemon that understands the protocol used by the XMLSocket object. The protocol is as follows:

*   XML messages are sent over a full-duplex TCP/IP stream socket connection.
*   Each XML message is a complete XML document, terminated by a zero byte.
*   An unlimited number of XML messages can be sent and received over a single XMLSocket connection.

<a href="https://www.adobe.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b6f7566-ca28-410b-a61d-337202d0bc01/flash-socket.jpg" alt="Socket Programming with Flash" width="500" /></a>

<del>Silverlight doesn't support socket programming.</del> Silverlight supports sockets programming through the System.Net.Sockets namespace. Silverlight supports asynchronously sending data back and forth across a socket over ports ranging from 4502 to 4534. Silverlight supports cross-domain socket communications between a Silverlight application and any server, provided that a special security policy file is in place on the server.</p>

## Webcam Support

Flash has <a href="https://youtube.com/watch?v=qYmYkMYGp5s">webcam</a> and microphone support for live video and audio transmission, and using them is really easy in Flash. It takes only a few lines of ActionScript code to invoke the camera object.
<table id="rounded-corner" border="0" summary="Webcam Support" width="500"><br>
<tbody>
<tr>
<td valign="top">Camera.get</td>
<td align="left" valign="top">Returns a default or specified camera object, or null if the camera is not available.</td>
</tr>
<tr>
<td valign="top">Camera.setMode</td>
<td align="left" valign="top">Sets aspects of the camera capture mode, including height, width and frames per second.</td>
</tr>
<tr>
<td valign="top">Camera.setMotionLevel</td>
<td align="left" valign="top">Specifies how much motion is required to invoke Camera.onActivity(true) and how much time should elapse without motion before Camera.onActivity(false) is invoked.</td>
</tr>
</tbody>
</table>

Silverlight doesn't support webcam or microphone.</p>

## Deployment

The Flash deployment package contains only a <strong>single Shockwave (SWF) file</strong>, and all images, text and animations are incorporated in this file. Because of the compressed nature of a Flash component, its images and text are not indexed by search engines, and thus not searchable.

The deployment process of Silverlight is far more complex; <strong>all individual components need to be deployed separately</strong>. The following components typically get sent to the client for each Web request of Silverlight:

*   XML files,
*   DLL files (if necessary),
*   Silverlight.js file,
*   Any other JavaScript file,
*   Resources (images, audio, video).

[![Silverlight Deployment](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca2f3f2f-a195-47f1-9417-785015a4cf1a/silverilght-deployment.png)](https://www.microsoft.com/)

<em>Read the full documentation on Silverlight deployment.</em>

## Windows Application

A Flash movie can be compiled into a Windows application and run as a <strong>standalone EXE</strong> file. It can also be played on a desktop that has an appropriate Flash player.

![Flash EXE Builder](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16ac6544-687a-45bc-bd55-95c8dc65ddd0/flash-exe.jpg)

Silverlight doesn't support playing the movie as a Windows application.</p>

## Media Streaming

Flash provides no such service to host the content and application with them. Thus, building a video website with Flash is not as cost-effective as building one with Silverlight.

<strong>Microsoft Silverlight Streaming</strong> by Windows Live is a companion service for Silverlight that makes it easy for developers and designers to deliver rich media as part of their Silverlight applications. The service allows Web designers and developers to host and stream cross-browser media and interactive applications that run on both Windows and Mac. This service can be combined with Microsoft Expression Studio and other third-party tools to create and develop interactive contents.

Silverlight Streaming by Windows Live is currently in beta testing and offers 10 GB of free hosting for rich-media applications.

[![Microsoft Silverlight Streaming](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90830afa-1fae-4832-bbc9-98b1f8a65aa7/silverlight-stream.gif)](https://msdn.microsoft.com)

## Conclusion

Selecting the right technology for rich Internet applications is often critical, and choosing between Flash and Silverlight depends entirely on your requirements. If you expect that some of your users will be on Linux or Solaris, then you should go with Flash. If you want your website to be indexed by search engines, then Silverlight may be better.

Besides, as Doug S. is points out in the comments, it's worth noticing that a minority of web users actually have a Silverlight plugin installed on their machine, while most users do have Flash-support. The Flash Player 9 and higher support streaming of the H.264 video codec which means anyone with a video program that can output an MP4 can stream to Flash. There are literally hundreds of free apps on Mac, PC and Linux that can do this. It's also important to mention that the latest version of Flash Player supports 3D rendering while Silverlight does not and that SWF, FLA, FLV, and AS are all open-standard formats, while Silverlight is 100% proprietary.

The following table summarizes the features discussed above. Rather than including arrows to indicate whether each platform has a particular feature, we've simply marked "better" to show the areas in which each technology beats out the other.
<table id="rounded-corner" border="0" summary="Flash vs. Silverlight">
<thead>
<tr>
<th class="rounded-company" scope="col" align="left">Features</th>
<th class="rounded-q1" scope="col" align="center">Flash</th>
<th class="rounded-q2" scope="col" align="center">Silverlight</th>
</tr>
</thead>
<tfoot></tfoot>
<tbody>
<tr>
<td>Animation</td>
<td align="center"></td>
<td align="center">better</td>
</tr>
<tr>
<td>File size</td>
<td align="center">better</td>
<td align="center"></td>
</tr>
<tr>
<td>Scripting</td>
<td align="center"></td>
<td align="center">better</td>
</tr>
<tr>
<td>Video/Audio</td>
<td align="center"></td>
<td align="center">better</td>
</tr>
<tr>
<td>Sound processing</td>
<td align="center">better</td>
<td align="center"></td>
</tr>
<tr>
<td>Accessibility</td>
<td align="center">better</td>
<td align="center"></td>
</tr>
<tr>
<td>Platform compatibility</td>
<td align="center">better</td>
<td align="center"></td>
</tr>
<tr>
<td>Text representation/SEO</td>
<td align="center"></td>
<td align="center">better</td>
</tr>
<tr>
<td>Supported image formats</td>
<td align="center">better</td>
<td align="center"></td>
</tr>
<tr>
<td>Socket programming</td>
<td align="center">better</td>
<td align="center"></td>
</tr>
<tr>
<td>Webcam support</td>
<td align="center">better</td>
<td align="center"></td>
</tr>
<tr>
<td>Deployment</td>
<td align="center">better</td>
<td align="center"></td>
</tr>
<tr>
<td>Windows application</td>
<td align="center">better</td>
<td align="center"></td>
</tr>
<tr>
<td>Media streaming</td>
<td align="center"></td>
<td align="center">better</td>
</tr>
</tbody>
</table>

## Further Resources

The following articles are suggested for further reading:

*   [The Gradual Disappearance Of Flash Websites](https://www.smashingmagazine.com/2010/04/the-gradual-disappearance-of-flash-websites/)
*   [The State Of Animation 2014](https://www.smashingmagazine.com/2014/11/the-state-of-animation-2014/)
*   [HTML5 And Flash: Why It’s Not A War, And Why Flash Won’t Die](https://www.smashingmagazine.com/2010/05/html5-and-flash-why-its-not-a-war-and-why-flash-wont-die/)

{{< signature "al" >}}

