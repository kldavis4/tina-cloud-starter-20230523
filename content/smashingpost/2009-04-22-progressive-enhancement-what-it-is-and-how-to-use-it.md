---
title: 'Progressive Enhancement: What It Is, And How To Use It?'
slug: progressive-enhancement-what-it-is-and-how-to-use-it
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf00f006-310a-493b-a6c6-bd93a484ae3a/css.jpg
date: 2009-04-22T21:10:21.000Z
author: sam-dwyer
description: >-
  **Progressive Enhancement** is a powerful methodology that allows Web
  developers to concentrate on building the best possible websites while
  balancing the issues inherent in those websites being accessed by multiple
  unknown user-agents. Progressive Enhancement (PE) is the principle of starting
  with a rock-solid foundation and then adding enhancements to it if you know
  certain visiting user-agents can handle the improved experience.

  PE differs from Graceful Degradation (GD) in that GD is the journey from
  complexity to simplicity, whereas PE is the journey from simplicity to
  complexity. PE is considered a better methodology than GD because it tends to
  cover a greater range of potential issues as a baseline. PE is the whitelist
  to GD's blacklist.

  Part of the **appeal of PE is the strength of the end result**. PE forces you
  to initially plan out your project as a functional system using only the most
  basic of Web technologies. This means that you know you'll always have a
  strong foundation to fall back on as complexity is introduced to the project.
categories:
  - Coding
  - CSS
---
<strong>Progressive Enhancement</strong> is a powerful methodology that allows Web developers to concentrate on building the best possible websites while balancing the issues inherent in those websites being accessed by multiple unknown user-agents. Progressive Enhancement (PE) is the principle of starting with a rock-solid foundation and then adding enhancements to it if you know certain visiting user-agents can handle the improved experience.

PE differs from Graceful Degradation (GD) in that GD is the journey from complexity to simplicity, whereas PE is the journey from simplicity to complexity. PE is considered a better methodology than GD because it tends to cover a greater range of potential issues as a baseline. PE is the whitelist to GD's blacklist.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Progressive Enhancement Is Faster](https://www.smashingmagazine.com/2013/09/progressive-enhancement-is-faster/)
*   [Progressive Enhancement And Standards Do Not Limit Web Design](https://www.smashingmagazine.com/2010/04/progressive-enhancement-and-standards-do-not-limit-web-design/)
*   [Reimagining Single-Page Applications With Progressive Enhancement](https://www.smashingmagazine.com/2015/12/reimagining-single-page-applications-progressive-enhancement/)
*   [Preload: What is it good for?](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/)

## That's All Well and Good, But Why Would I Want To Use It?

Part of the <strong>appeal of PE is the strength of the end result</strong>. PE forces you to initially plan out your project as a functional system using only the most basic of Web technologies. This means that you know you'll always have a strong foundation to fall back on as complexity is introduced to the project.

{{% feature-panel %}}

PE goes well with the principle of "Release early, release often." By starting with a strong foundation, you are able to release projects that work and then concentrate on adding the bells and whistles at a more appropriate time.

PE projects are easier to maintain. With this focus on "first principles," developers can concentrate on more complex sections of system interaction without worrying about the foundation.

PE is also good for your users. It gives them the security of knowing they can visit your website using any of the thousands of user-agents available to them and still interact with your content as that agent allows.</p>

## All Right, So How Do I Use It?

In practical terms, it's easiest to break the concept of PE into different layers, each one building on the previous to improve the experience of interacting with the website.</p>

### The Layers

The first layer is clean, semantic HTML. This allows text-based, speech-based, antiquated and robotic user-agents to navigate the content of your website properly.

The second layer is CSS. This allows visual-based user-agents to display or alter the visual representation of your website's content.

The third layer is JavaScript. This allows user-agents that are capable of using it to provide your users with enhanced usability.</p>

### A practical example

We'll create a Progressively Enhanced list of website navigation items whose order is saved by the user. Our ultimate goal is for users to have a drag-and-drop experience that saves the menu order via AJAX. But because we’ll be reaching that end goal through the principles of PE, all user-agents should be able to interact with our list in the way most appropriate to them.

<strong>The first layer</strong>

Here we have the semantic markup of the navigation. See <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72fe44ba-68d2-4af0-aebc-cf14e6e3e225/navigation-1.html">navigation-1.html</a>.

<pre><code class="language-markup tmp-xml">&lt;form action="save_order.php" method="post"&gt;
	    &lt;fieldset&gt;
	        &lt;legend&gt;Order of Navigation&lt;/legend&gt;
	        &lt;ol&gt;
	            &lt;li id="homepage-12"&gt;Homepage &lt;label for="menu-id-12"&gt;Change the order for Homepage&lt;/label&gt;&lt;input type="text" name="homepage-12" id="menu-id-12" value="1" /&gt;&lt;/li&gt;
	            &lt;li id="contact-23"&gt;Contact Us &lt;label for="menu-id-23"&gt;Change the order for Contact Us&lt;/label&gt;&lt;input type="text" name="contact-23"  id="menu-id-23" value="2" /&gt;&lt;/li&gt;
	            &lt;li id="about-16"&gt;About Us &lt;label for="menu-id-16"&gt;Change the order for About Us&lt;/label&gt;&lt;input type="text" name="about-16"  id="menu-id-16" value="3" /&gt;&lt;/li&gt;
	            &lt;li id="latest-14"&gt;Latest News &lt;label for="menu-id-14"&gt;Change the order for Latest News&lt;/label&gt;&lt;input type="text" name="latest-14"  id="menu-id-14" value="4" /&gt;&lt;/li&gt;
	        &lt;/ol&gt;
	    &lt;/fieldset&gt;
	    &lt;p&gt;&lt;input type="submit" value="Save new order" /&gt;&lt;/p&gt;
    &lt;/form&gt;</code></pre>

<img loading="lazy" decoding="async"  class="alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b06332d-a48a-4a05-a4d8-a66a47d8338b/navigation-1.png" alt="progressive enhancement - The first layer of the navigation form" />

The navigation is laid out as an ordered list within a form so that the user can alter the order using the input boxes provided. The individual list items are given an ID that correlates to the name of the input box (for reasons that will become apparent later -- for now, it does nothing but add a little weight to the markup). The labels for the input fields help the user figure out how to use the form.

Clicking "Save" will POST to the PHP page, which will determine the new order and print the results, but which could just as easily save to a database. The page is not very attractive to look at, but the important thing is that every element is in place to allow any user-agent, no matter how basic, to read and make sense of the form. Screen readers should be able to process this form easily, and keyboard navigation is functional and enabled by default.

Our <em>save_order.php</em> page is very simple and just echos the order of the menu items sent through in the POST.

<pre><code class="language-php">&lt;?php
	foreach($_POST as $menu_item=&gt;$order) {
	    echo "The order for $menu_item is $order";
	}
    ?&gt;</code></pre>

Obviously, this isn't a production script. It simply illustrates that the procedure for processing a form should be one of the first interactions in PE.

<strong>The second layer</strong>

Now, we’ll add a CSS layer to give the form a bit of visual elegance. See <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7421317-ab74-43ad-917c-7598f67079ab/navigation-2.html">navigation-2.html</a>.

<pre><code class="language-css">name="code"&gt;
    &lt;style type="text/css"&gt;
        form { width: 50%; margin: 0 auto;  }
        fieldset { background: #555555; padding: 1em; }
        legend { border: 1px #513939 solid; background: #FAFAFA;}
        label { position: absolute; margin-left: -999em; }
        ol { list-style: none; position: relative; }
        body { font: 100% serif; }
        ol li { border: 1px #FFF solid; background: #FAFAFA; padding: 0.7em; }
        ol li:hover { border: 1px #513939 solid; }
        input[type='text'] { width: 2em; text-align: center; position: absolute; left: 40%; }
    &lt;/style&gt;</code></pre>

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6ae8154-8848-43b2-b036-2dcf9aa68c61/navigation-2.png" alt="The second layer of the navigation form" />

We took the labels out of the document flow with <tt>position: absolute</tt> and then gave them an outrageous negative margin to remove them visually while leaving them in place for screen readers (which can still read them in the original order because we're not removing them with <tt>display: none</tt>).

We removed the numbers from the ordered list to avoid the potential confusion of having two sets of numbers for the list items.

We maintained the font size to initially be equal to whatever the user-agent has set as a preference and asked the user-agent to use its own default serif font.

We gave the individual list elements an outline and a bit of padding to see them more easily. To give the user a little more of a visual hint that the list items are movable, we also gave them a hover state that we know will be used by any user-agent that can handle it. Input boxes are neatened up a little, too, for browsers that can handle attribute selectors.

The form now looks a lot neater and is still just as functional as the first layer.

<strong>The third layer</strong>

Finally, we'll add the JavaScript layer, which allows the user to simply drag and drop the navigation items into the desired order. We'll use jQuery to make the process as painless as possible (both for us and our users). See <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2a5e95c-9c93-4caf-86be-30d4da42b7e5/navigation-3.html">navigation-3.html</a>.
<pre class="js">    &lt;script type="text/javascript"&gt;
        $(document).ready(function() {
            $('input').hide();
            $('ol').sortable({items: 'li',
                update: function(event, ui) {
                    var new_order = $('ol').sortable('toArray');
                    $.each(new_order, function(i, element) {
                        $('input[name='+element+']').attr('value', i+1);
                    });
                    $.post("save_order.php", {
                        'new_order': $('form').serialize()
                    })
                }
            }); 
        });
    &lt;/script&gt;
</pre>

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7c971e6-8df6-4646-8076-4ae635cb3f48/navigation-3.png" alt="The third layer of the navigation form" />

1.  Hide the input fields because we're providing users with a different usability experience.
2.  Make the ordered list sortable using the jQuery UI sortable plug-in.
3.  Update the new order each time the DOM changes. We'll use the options and utility functions in jQuery and the plug-in to get the new order for the list items and to set the value of each text field to match each list item's unique ID.
4.  Send the newly updated form to the server via POST.
5.  Parse the <tt>new_order</tt> variable that we sent via AJAX to match the values expected by the original PHP script.

Our server-level script in <em>save_order.php</em> needs to change very little to still work. We simply take the new AJAX posted value and parse it into the POST that the original form was looking for. This is another of the strengths of PE: by adding the basic form interactions in the first layer, it becomes much easier to add potentially complex interactions in later stages with minimal fuss.

<pre><code class="language-php">&lt;?php
		if(isset($_POST['new_order'])) {
		    parse_str($_POST['new_order'], $_POST);
		}
		foreach($_POST as $menu_item=&gt;$order) {
		    echo "The order for $menu_item is $order";
		}
	?&gt;</code></pre>

Now, here's the interesting thing about this last layer: while the drag-and-drop functionality makes menu ordering more <em>usable</em> for many users, it actually makes it less <em>accessible</em>, too. Our users now have to use the mouse to reorder menu items; those who prefer keyboard shortcuts will have a frustrating experience, and blind users would find it totally unusable (even if they could drag and drop the new menu elements, they have no way of updating the new values to their screen reader).

There are a few solutions to this problem, from as complex as rewriting the sortable jQuery plug-in to be keyboard-accessible and WAI-ARIA-compliant to as simple as providing a quick link at the top of the page that allows users to turn off JavaScript and use the more accessible version we had in layer 2.

## Okay, You've Convinced Me...

While this is a very basic example, it illustrates the power of using Progressive Enhancement in development. By clearly establishing how a system's interactive elements are supposed to function at the most basic level, you gain a clearer understanding of the project's requirements. Your clients will be happy with the rock-solid results, the more accurate time-frame estimates and the easier maintenance, and you will be happy knowing you've provided a better, stronger product that benefits more people.</p>

## Related Articles To P<span data-sheets-value="{&quot;1&quot;:2,&quot;2&quot;:&quot;progressive enhancement&quot;}" data-sheets-userformat="{&quot;2&quot;:513,&quot;3&quot;:{&quot;1&quot;:0},&quot;12&quot;:0}">rogressive Enhancement</span>

You may be interested in the following related articles:

*   Graceful degradation versus progressive enhancement
*   Delivering the right experience to the right device
*   Pragmatic progressive enhancement - why you should bother with it

{{< signature "al" >}}

