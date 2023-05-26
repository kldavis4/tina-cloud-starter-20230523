---
title: 'Infinite Scroll: Let’s Get To The Bottom Of This'
slug: infinite-scrolling-lets-get-to-the-bottom-of-this
image: null
date: 2013-05-03T08:56:39.000Z
author: yogev-ahuvia
description: >-
  Infinite scroll promised to provide users with a better experience. However, the good is often accompanied by the bad and the ugly. Once we understand the strengths and weaknesses of infinite scrolling, we can begin to use it to empower our interfaces.
categories:
  - UX
  - Trends
  - Web Design
  - Navigation
  - UX
---
Human nature demands hierarchy and structures that are easy to navigate. But infinite scrolling sometimes leaves users feeling disoriented as they travel down a page that never ends.</p>

<div class="c-felix-the-cat">
<h4 class="h3">Infinite Scrolling, Pagination Or “Load More” Buttons?</h4>
<p>What is the best UX pattern to display products on an e-commerce website? We tested three different design patterns for loading products. <a href="https://www.smashingmagazine.com/2016/03/pagination-infinite-scrolling-load-more-buttons/" class="btn btn--medium btn--blue">Read a related article →</a></p>
</div>

{{% feature-panel %}}

<figure><img loading="lazy" decoding="async"  class="alignnone wp-image-115759" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd0ddec3-aca8-42ed-9d0d-3e09cd1fcf81/neverendingstory1-1024x684.jpg" alt="infinite scroll" width="500" height="334" /></figure>

## The Good

Long lists are not new, but the way in which we scroll these lists has fundamentally changed since the arrival of mobile interfaces. Due to the narrowness of mobile screens, list items are arranged vertically, requiring frequent scrolling.

Infinite scrolling is <a href="https://www.google.com/trends/explore#q=Infinite%20Scroll">highly trending</a> as an interaction behavior on pages and lists. The basic functionality is that, as the user scrolls through content, more content is loaded automatically. With the popularity of social media, massive amounts of data are being consumed; infinite scrolling offers an <strong>efficient way to browse that ocean of information</strong>, without having to wait for pages to preload. Rather, the user enjoys a truly responsive experience, whatever device they’re using.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10c26bc0-6dd8-4397-923c-e840e98cf6a1/infinite-scroll-vs-pagination.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="151618" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10c26bc0-6dd8-4397-923c-e840e98cf6a1/infinite-scroll-vs-pagination.png" alt="Pagination vs. Infinite Scroll" width="500" height="figure32" /></a><figcaption>Pagination versus infinite scrolling (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10c26bc0-6dd8-4397-923c-e840e98cf6a1/infinite-scroll-vs-pagination.png">Large version</a>)</figcaption></figure>

Websites with lots of user-generated content today are using infinite scrolling to handle content that is being generated every second. By unspoken agreement, users are aware that they won’t get to see <em>everything</em> on these websites, because the content is updated too frequently. With infinite scrolling, social websites are doing their best to expose as much information as possible to the user.</p>

<a href="https://www.twitter.com/estellevw">Twitter</a> integrates infinite scrolling effectively. Its feed fits the criteria: a large amount of data (tweets) and a real-time platform. From the perspective of the user, all tweets are equally relevant, meaning that they have the same potential to be interesting or uninteresting; so, users will often scroll through all of the tweets in their feed. Being a real-time platform, Twitter is constantly being updated, even if the user leaves their feed unattended. Infinite scrolling seems to have been created especially for websites like Twitter, which successfully employs the technology.

Infinite scrolling appears to have found its niche on the Web. However, there are also drawbacks that must be considered before assessing its value.</p>

## The Bad And The Ugly

With so much data to browse, users must stay focused on the information they are searching for. (Remember about being goal-oriented?) Do users always want <strong>a never-ending stream of data?</strong> Analytics show that when users search for information on Google, <a href="https://www.quora.com/What-is-the-distribution-of-traffic-between-Google-organic-search-results-e-g-1-vs-2-in-rankings-first-page-vs-second-page">only 6%</a> advance to the second page. So, 94% of users are satisfied with receiving only 10 results, which suggests that users find Google’s ranking of results to be relevant.</p>

### To Click or Not to Click

Google has implemented infinite scrolling for image search results but has <a href="https://thenextweb.com/google/2011/08/17/google-testing-infinite-scrolling-in-search-results/">yet to implement</a> it for its general results. Doing so would eliminate the need for users to click to reach the second page. Google will probably maintain pagination because this pattern is quite symbolic for its brand. If it does switch to infinite scrolling, when would users typically stop scrolling? After 20 results? 50? When does an easy browsing experience become more complicated?

Looking for the best search result could take a second or an hour, depending on your research. But when you decide to stop searching in Google’s current format, you know the exact number of search results. You can make an informed decision about where to stop or how many results to peruse because you know where the end is. <a href="https://videolectures.net/chi08_kieras_phc/">According to studies</a> conducted in the field of human-computer interaction, <strong>reaching an end point provides a sense of control</strong>; you know that you have received all relevant results, and you know whether the one you are looking for is there or not. Knowing the number of results available provides a sense of control and helps the user make a more informed decision, rather than be left to scour an infinitely scrolling list.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4109abfa-31a6-4e2e-a877-9982b9f7a71c/pagination-close-up.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="151618" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4109abfa-31a6-4e2e-a877-9982b9f7a71c/pagination-close-up.png" alt="Pagination: The Click Barrier" width="500" height="132" /></a><figcaption>Pagination is a barrier of clicks. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4109abfa-31a6-4e2e-a877-9982b9f7a71c/pagination-close-up.png">Large version</a>)</figcaption></figure>

When items are distributed across Web pages, they are framed and indexed and have a start and end point. The information is presented clearly and orderly. If we select an item from a paginated list and are taken from that page, we know that clicking “Back” will return us to that page (probably to the same scroll position). Our Web search will continue right where it left off.

If you scroll the same list of results with infinite scrolling, you are left without that sense of control because you are scrolling through a list that is conceptually infinite. Let’s say you count yourself among the 94% who stop reading after the first page (i.e. 10 results) of a Google search. When the list scrolls infinitely, there is essentially no end to the first page. Rather than look for the end of the page, which doesn’t exist anyway, you decide to stop scrolling at the 10th item. This poses a problem with infinite scrolling, because the 11th item is directly in sight. With a paginated list, on which you wouldn’t see the 11th result, deciding not to continue browsing is easier. However, when the next results <a href="https://www.youtube.com/watch?v=j9UfY_94sKU">are already there</a>, <strong>you’d probably just keep on scrolling and scrolling</strong>.

As Dmitry Fadeyev points out:
<blockquote>"People will want to go back to the list of search results to check out the items they’ve just seen, comparing them to what else they’ve discovered somewhere else down the list. Having a paginated interface lets the user keep a <strong>mental location</strong> of the item. They may not necessarily know the exact page number, but they will remember roughly what it was, and the paginated links will let them get there easier.

Not only does the infinite scroll break this dynamic, it also makes it difficult to move up and down the list, especially when you return to the page at another time and find yourself back at the top, being forced to scroll down the list once again and wait for the results to load. In this way the infinite scroll interface is actually slower than the paginated one."

— Dmitry Fadeyev, <a href="https://www.usabilitypost.com/2013/01/07/when-infinite-scroll-doesnt-work/">When Infinite Scroll Doesn't Work</a></blockquote>

## When Infinite Scrolling Fails

The best companies are constantly <a href="https://www.businessinsider.com/marissa-mayer-google-9-2010-11">testing</a> and <a href="https://readwrite.com/2010/08/26/revolt_angry_digg_users_want_their_baby_back">studying</a> new interactions with their users. Increasing numbers of these studies are showing that infinite scrolling <a title="the pros" href="https://econsultancy.com/il/blog/61703-infinite-scrolling-pros-and-cons">does not resonate</a> with users if it does not support their goal on the website.</p>

### Temptation

When you’re looking for that perfect search result and are tempted to continue scrolling into a wasteland of irrelevant results, time is wasted. Chances are that the best result will appear in the first 10 items. Therefore, infinite scrolling merely <a href="https://techcrunch.com/2012/08/18/infinite-scroll-the-webs-slot-machine/">tempts you</a> to continue reading, wasting time and decreasing productivity in the process.</p>

### Optimism

Even more annoying is that scroll bars do not reflect the actual amount of data available. You’ll scroll down happily assuming you are close to the bottom, which by itself tempts you to scroll that little bit more, only to find that the results have just doubled by the time you get there.</p>

### Exhaustion

Infinite scrolling overwhelms users with stimuli. Like playing a game that you can never win, no matter how far you scroll, you feel like you’ll never get to the end. The combination of temptation and optimism play a big role in exhausting the user.</p>

### Pogosticking

Infinite scrolling often causes your position on the page to get lost. “Pogosticking” happens when you click away from an infinitely scrolling list and, when you return by clicking “Back,” are brought to the top of the previous page, instead of to the point where you left off. This happens because the scroll position is lost when you navigate away from an infinitely scrolling page, forcing you to scroll back down each time.</p>

### Loss of Control

Infinite scrolling leaves you with the feeling that you might be missing out on information. You continue scrolling because the results are right there, but you feel overwhelmed because you’re losing control over the amount of data being shown. There is something nice about defined pages on which the amount of content is quantified, where you can comfortably choose whether to click to view more or to stop. With infinite scrolling, you don’t have control over the amount of data on the page, which becomes overwhelming.</p>

### Distracting

Etsy, an e-commerce marketplace, implemented infinite scrolling, only to find that it <a href="https://www.slideshare.net/danmckinley/design-for-continuous-experimentation">led to fewer clicks</a> from its users. Infinite scrolling was unsuccessful because users felt lost in the data and had difficulty sorting between relevant and irrelevant information. While infinite scrolling provided faster and more results, users were <a href="https://danwin.com/2013/01/infinite-scroll-fail-etsy/">less willing</a> to click on them, defeating its very purpose.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d66f836a-7cb9-470b-8b58-a97d68421f68/etsy-home-page.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="151618" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d66f836a-7cb9-470b-8b58-a97d68421f68/etsy-home-page.jpg" alt="Etsy's Home Page" width="500" height="132" /></a><figcaption>Etsy’s home page (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d66f836a-7cb9-470b-8b58-a97d68421f68/etsy-home-page.jpg">Large version</a>)</figcaption></figure>

### Unreachable

Have you tried reaching the footer of Facebook lately? The footer block exists below the news feed, but because the feed scrolls infinitely, more data gets loaded as soon as you reach the bottom, pushing the footer out of view every time. Footers exist for a reason: they contain content that the user sometimes needs. In Facebook’s case, the user can’t reach it. The links are repeated elsewhere but are harder to find. Infinite scrolling impedes the user by making important information inaccessible.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1c917a5-6828-490d-ae2e-15b49a5e8c05/facebook-loading-footer.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="151618" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1c917a5-6828-490d-ae2e-15b49a5e8c05/facebook-loading-footer.png" alt="Facebook auto-loading News Feed and the unreachable footer" width="500" height="132" /></a><figcaption>Facebook’s auto-loading news feed makes the footer unreachable. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1c917a5-6828-490d-ae2e-15b49a5e8c05/facebook-loading-footer.png">Large version</a>)</figcaption></figure>

Footers serve as a last resort. If users can’t find something or they have questions or want more information or explanation, they often go there. If they don’t find it there, they might leave the website altogether. Companies that implement infinite scrolling should either make the footer accessible by <a href="https://struck.com/">making it sticky</a> or relocate the links to a sidebar.</p>

### Not Exclusive

<a href="https://de.pinterest.com/smashingmag/">Pinterest</a> does not have a footer at all, which makes sense given the problem we just saw with Facebook. Through infinite scrolling, Pinterest emphasizes its profusion of data, an endless sea of inspiration taken from all over the Web.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40c9ff26-aa94-440b-8273-50c250da56c2/pinterestocean.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40c9ff26-aa94-440b-8273-50c250da56c2/pinterestocean.jpg" alt="Pinterest Ocean of Pins" width="500" height="132" /></a><figcaption>Pinterest’s ocean of pins (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40c9ff26-aa94-440b-8273-50c250da56c2/pinterestocean.jpg">Large version</a>)</figcaption></figure>

Images are faster and easier to scroll than text, so Pinterest and Google Images succeed with infinite scrolling to an extent. However, <a href="https://techcrunch.com/2013/01/17/facebook-photos-record/">billions of images</a> are on the Web, and users would prefer to see only the best of them. There is something to be said for exclusivity, which seems to be lacking in Pinterest’s layout.

Limiting the number of images on Pinterest’s home page, with an “Editor’s picks” or “Most popular” list, might make the website more appealing. How exclusive can a pin be when a ton of other similar pins are next to it?

Pinterest’s tactic of using infinite scrolling for its plethora of data suffers because it overwhelms users. The collection looks bottomless, but its immensity is somewhat daunting, and browsing it might seem a waste of time. Ultimately, Pinterest is trying to expose users to infinite inspiration, but that actually undermines the <a href="https://www.youtube.com/watch?v=6ELAkV2fC-I">human need for control</a>. The amount of data becomes intimidating, and users are left with mixed feelings.</p>

## When Usability Wins

As mentioned earlier, Twitter integrates infinite scrolling effectively. The user sees an infinitely growing list of tweets and can comfortably click on a tweet to expand it in place, preventing the page from refreshing and, as a result, maintaining their scroll position.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4a2f2d9-7cb2-44a5-990f-cdc496808ee7/twittertornfeed.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4a2f2d9-7cb2-44a5-990f-cdc496808ee7/twittertornfeed.png" alt="Twitter's torn feed" width="500" /></a><figcaption>Twitter’s torn feed (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4a2f2d9-7cb2-44a5-990f-cdc496808ee7/twittertornfeed.png">Large version</a>)</figcaption></figure>

On its mobile version, Twitter even adds a “torn paper” marker, indicating to the user where to resume reading. This subtle and simple solution enables the user <strong>to scroll up and down the list, while having a recognizable point</strong> to return to. Psychologically, that marker reassures the reader by dividing read and unread content. Such markers give the user a sense of control and a better perception of the content’s depth and how far they’ve gotten into it.

Twitter is not the only one. <a title="Discourse" href="https://www.discourse.org/">Discourse</a>, an emerging discussion platform, also has infinite scrolling that empowers the user. The company considered the importance of infinite scrolling to its user experience and implemented an intriguing and unique progress indicator. The indicator appears when needed and remains in view (without interfering) while the user reads the content. The indicator numbers the item currently being viewed out of the total number of items. This is a great way to make the user feel in control, even with a lot of data.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6eca245-ff5e-465a-a05f-5a3669886eba/discourse-infinite-scroll1.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="116660" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6eca245-ff5e-465a-a05f-5a3669886eba/discourse-infinite-scroll1.png" alt="Smart progress indicator on Discourse.com" width="500" /></a><figcaption>The smart progress indicator on Discourse (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6eca245-ff5e-465a-a05f-5a3669886eba/discourse-infinite-scroll1.png">Large version</a>)</figcaption></figure>

### Go Hybrid

A hybrid of infinite scrolling and pagination is also a good option in many cases. With this solution, you would show a “load more” button at the end of a preloaded list, which, when clicked, loads another batch of items onto the list. The same behavior that infinite scroll does automatically, this button does <strong>on demand</strong>. The interface gains some of the advantages of infinite scrolling, without some of its drawbacks.

Because infinite scrolling requires the website to fetch so much content, the hybrid solution is used at times to control the data load. In Facebook’s news feed and Google’s image search, the infinite scrolling is automatic at first but becomes on-demand once a certain number of items have loaded. This maintains the interface while limiting the load on the server.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/605a6cd6-aae8-46f4-ba7b-04cd44b42a71/hybrid-infinite-pagination.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="151618" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/605a6cd6-aae8-46f4-ba7b-04cd44b42a71/hybrid-infinite-pagination.png" alt="Hybrid Infinite Pagination on Google Images" width="figure00" height="132" /></a><figcaption>Hybrid infinite pagination on Google Images (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/605a6cd6-aae8-46f4-ba7b-04cd44b42a71/hybrid-infinite-pagination.png">Large version</a>)</figcaption></figure>

## Infinite Pages

<a href="https://www.usabilitypost.com/2012/10/29/the-return-of-the-scroll/">Infinite pages</a> take the concept of infinite scrolling to a new level. Websites that employ this concept are “one-pagers.” To remove the barrier of clicking to the next page, the designer turns the entire website into one long scrollable page. Examples are <a href="https://unfold.no/">Unfold</a> and <a href="https://lostworldsfairs.com/atlantis/">Lost World’s Fairs</a>.

On these one-page websites, the sections are spread vertically, one after another. This makes the whole website less comprehensible — hence, less accessible. These websites might not have infinite scrolling, but the user might still have that feeling of a never-ending page.

On infinite pages, the height of each section will vary according to its contents. Although the approach can make for some creative interactions, it can leave users disoriented and unsure where to scroll for the next piece of information. The scroll bar is hidden on many such pages, leaving users feeling lost as they unconsciously <a href="https://www.cxpartners.co.uk/cxblog/the_myth_of_the_page_fold_evidence_from_user_testing/">look for the scroll position</a> to track their progress. <strong>Hidden scroll bars deprive users of that chance for rescue.</strong> Users shouldn’t be left helpless; the interface should clearly show them how to navigate the page.</p>

<figure><img loading="lazy" decoding="async"  class="151618" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0c3dc9b-248c-4cb4-90aa-dda20a1f7000/infinite-page.png" alt="Infinite Page" width="400" /><br>
<em>Not knowing where they stand can leave the users disoriented.</em></figure>

UX engineers need to take extra care when designing infinite pages. They must take into account accessibility; tell users where they stand by showing the length of the page and how much they’ve viewed. Solutions could include a fixed menu, a <a href="https://larsjung.de/fracs/">map of the page</a> or a scroll progress bar.

Another trick is the <a href="https://en.wikipedia.org/wiki/Parallax_scrolling">parallax effect</a>, whereby different layers on the page move at different speeds according to the user’s scrolling, creating the illusion of depth (as seen on <a href="https://andrevv.com/">Andrew McCarthy’s website</a>). While it can help to create beautiful and <a href="https://www.shibui.me/web/scroll/index.html">innovative</a> experiences, it is sometimes <strong>heavily overused</strong>, and users can get confused by how much they need to scroll for more content. When the parallax effect is combined with animation, the user can get confused about whether the page is being scrolled by their movement or is moving autonomously. It's wise to use the technique to enhance content, not as the content itself.</p>

## Let’s Get To The Bottom Of This

Infinite scrolling can be an innovative feature that greatly improves an interface by exposing content and making performance more efficient. But it needs to be used correctly.

Avoid the following sinkholes to achieve a strong infinite scrolling experience:

*   **Users want immediate access to exclusive data.**.  Users don’t want to be left to explore all of a website’s data on their own. When implementing infinite scrolling, identify what data is exclusive to your website and elevate it to the top of the page, and filter less relevant information.
*   **Users want to feel in control.**.  Infinite scrolling sabotages that feeling of control. Add a smart progress indicator, a fixed menu or a map.
*   **Users often look for landmarks when scrolling.**.  When scrolling through long lists, users expect to be able to easily distinguish between new and viewed data. Add landmarks along the interface to keep users oriented.
*   **Consider conventional pagination or a hybrid solution.**.  Good old pagination is always an alternative to infinite scrolling. And if that doesn’t fit the context, then a hybrid solution, using a “load more” button, could greatly enhance the interface.
*   **Provide interesting content without an ambiguous interface.**.  Having to traverse a never-ending list is logical only if the user leaves feeling that it was worthwhile.
*   **Users often expect a footer.**.  If footer-type information is functional to the interface, then it should appear at the bottom of the page. A fixed footer is usually the way to go with infinite scrolling.
*   **An infinite list is still a list.**.  Infinite scrolling still needs to meet common interface standards. Whether users take their eyes off the screen for a moment or click a link and then click “Back,” they expect to return to the exact point where they left off. Whatever your interface, make sure it meets users’ expectations.
*   **Effects are nice to have but not a must.**.  Many infinitely scrolling interfaces have various effects to show more data (whether by sliding in new content or another method). Be mindful not to focus more on effects than on presenting data in the most effective way possible.</p>

### Use It Correctly

Users are goal-oriented and find satisfaction in reaching the end of their exploration. To be effective, infinite scrolling has to account for this. <strong>Nothing is really infinite</strong>, not even these infinitely scrolling lists we’ve looked at. Users should always know where they stand, even when the content has not finished loading. They should know what the total amount of data is and be able to easily navigate the list. Infinite scrolling has to be implemented in the best possible way so that users can always find their way.

{{< signature "al" >}}

