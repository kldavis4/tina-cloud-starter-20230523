---
title: 'State Of GDPR In 2021: Cookie Consent For Designers And Developers'
slug: state-gdpr-2021-cookie-consent-designers-developers
author: danny-bluestone
image: >-
  https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/075a850f-3306-42ca-8991-ff8acc2d335e/gdpr-update-new-cookie-banner.png
date: 2021-03-01T14:30:00.000Z
summary: >-
  As digital practitioners, GDPR has impacted every facet of our professional and personal lives. Whether you’re addicted to Instagram, message your family on WhatsApp, buy products from Etsy or Google information, no one has escaped the rules that were introduced in 2018.
description: >-
  As digital practitioners, GDPR has impacted every facet of our professional and personal lives. Whether you’re addicted to Instagram, message your family on WhatsApp, buy products from Etsy or Google information, no one has escaped the rules that were introduced in 2018.
categories:
  - GDPR
  - Privacy
---

[Last week](https://www.smashingmagazine.com/2021/02/state-gdpr-2021-key-updates/), I gave you an update on everything that’s happened with GDPR since 2018. (TL;DR: A lot has changed.) In this article, we’ll look at cookie consent: specifically, the paradox where marketers are heavily reliant on Google Analytics cookie data but need to **comply with regulations**.

We’ll take a look at two developments that have impacted cookies, plus a third on the horizon. Then I’ll walk you through the risk-based approach that we’ve taken &mdash; for the moment, at least. And come back next time for a deep dive into first-party ad tracking as we start to see moves away from third-party cookies.

- [Part 1: GDPR, Key Updates And What They Mean](https://www.smashingmagazine.com/2021/02/state-gdpr-2021-key-updates/)
- **Part 2: GDPR, Cookie Consent And 3rd Parties**

### Big Development #1: Cookie Consent

In May 2020, the EU [updated its GDPR guidance](https://edpb.europa.eu/sites/edpb/files/files/file1/edpb_guidelines_202005_consent_en.pdf) to clarify several points, including two key points for cookie consent:

- **Cookie walls** do not offer users a genuine choice, because if you reject cookies you’re blocked from accessing content. It confirms that cookie walls should not be used.
- **Scrolling or swiping** through web content does not equate to implied consent. The EU reiterates that consent must be explicit.

What does this mean for our industry?

Well, the EU is tightening up on cookie consent &mdash; perhaps the most noticeable (and annoying!) aspect of GDPR. Critics say that cookie notices are **a cumbersome block for users**, and don’t do anything to protect user privacy. The EU is trying to change this, by promoting simple, meaningful, equitable options for cookie consent.

But that restricts what we can do with cookies, and it hints ahead to when the Privacy and Electronic Communications Regulation (PECR) may come into force. More on that shortly.

### Big Development #2: Google and Apple crack down on third-party tracking; get hit by anti-trust complaints

As the big digital players figure out [how to comply with GDPR](https://www.cyber-duck.co.uk/what-we-do/digital-optimisation/gdpr-compliance) &mdash; and how to turn privacy legislation to their advantage &mdash; some have already come under fire.

Google is being investigated by the UK’s competition watchdog, the Competition and Markets Authority (CMA), for its ‘[Privacy Sandbox](https://www.reuters.com/article/us-google-britain-idUSKBN29D18Q)’ initiative, following complaints from adtech companies and publishers.

The Internet giant, which is also facing an **antitrust investigation** in Italy for [display advertising](https://www.reuters.com/article/us-italy-google-antitrust/italian-watchdog-investigates-google-over-alleged-advertising-market-abuse-idUKKBN27D0MM?edition-redirect=uk), and in the US for its [search advertising services](https://techcrunch.com/2020/10/20/justice-department-will-reportedly-file-its-antitrust-lawsuit-against-google-today/), is looking to remove third-party cookies from Chrome. (Firefox and Safari already block these cookies by default.)

The complainants say that this change will further concentrate advertising revenue in Google’s hands. Google’s response? The advertising industry needs to make ‘[major changes](https://www.reuters.com/article/us-google-britain-idUSKBN29D18Q)’ as it shifts to a ‘web without third-party cookies’.

Google’s not alone. In October 2020, four French digital advertising lobbies filed an [antitrust suit](https://www.reuters.com/article/apple-advertisting-france-idUSL1N2HJ237) against Apple’s forthcoming iOS privacy change, a feature it’s called **App Tracking Transparency** (ATT).

ATT, coming in an early-spring 2021 release of iOS 14, shifts app users from an opt-out to an opt-in ad-tracking model. With ATT, every app must get your permission to share your Identifier for Advertisers (IDFA), which enables third-party ad tracking across multiple sites and channels.

The complainants say that by restricting apps’ ad revenue, developers may have to boost app subscriptions and in-app purchases or switch to Apple’s targeted ad platform &mdash; all of which will funnel ad spend away from them and towards Cupertino.

Critics including Facebook have [slammed the change](https://techcrunch.com/2021/01/27/apple-app-tracking-transparency/), saying it’ll hit small businesses who rely on **microtargeted ads**. Apple has defended the move and praised the EU’s defence of citizens’ data privacy.

To sum up:

- Implied consent doesn’t equal consent under GDPR, according to the EU.
- We should also avoid cookie walls
- Google and Apple are moving against third-party cookies &mdash; which some say exploits their dominant market position.

So what does that mean for us, as designers and developers? First, let’s take a look at why this is important.

{{% feature-panel %}}

## Here’s What Designers Should Know About Cookies

- **GDPR is critical for you** because you’ll design the points at which cookies are placed, what data is collected, and how it’s processed.
- A **functionality audit** means you can map your cookie activity in the data and compliance layers on your service blueprint.
- It can help to do a cookie audit and gap analysis, i.e. is the existing cookie pattern compliant? What content does it need around it?
- Follow *Privacy by Design* best practices. Don’t try to reinvent the wheel &mdash; if you’ve created a compliant cookie banner, use your proven design pattern.
- Work with your compliance and development teams to **ensure designs meet GDPR** and can be implemented. Only ask for the data you need.
- If you need to compromise, take a risk-based approach. There’s a walk-through of one that we did further down.
- Be aware that your content team may need to **update your privacy policy** as GDPR and your use of cookies evolve.

## Here’s What Developers Should Know About Cookies

- Make sure you’re involved upfront about cookie consent and tracking, so what’s decided can be implemented.
- If you’re doing a product or website redesign, a cookie audit using Chrome Dev Tools can show you what **tracking cookies** are being used. Tools like [Ghostery](https://www.ghostery.com/) or [Cookiebot](https://www.cookiebot.com/en/) give you more detail. 
- You should implement the standard cookie opt in/out **as per GDPR guidance**. (Note that while GDPR is standard, the enforcement of it varies across EU countries. There’s more on this further down.) You may stand to lose Google Analytics data. You might also come under pressure to implement things that could be considered as dark patterns. There’s more on this later, with a walk-through of what we did and a look at the risk.

So that’s where we are today. Oh, and there’s one more thing to be aware of: a piece of **further legislation** that might be coming our way. I like to call it *Schrodinger’s Law*.

## Schrodinger’s Law: The ePrivacy Regulation

You may have heard of GDPR’s twin sister, the ePrivacy Regulation, who’s lurking on the legislative horizon. If you haven’t, here’s an introduction.

As I said above, cookie consent &mdash; the notice that pops up when you visit a website &mdash; is regulated by the GDPR. However, cookies themselves fall under a different piece of legislation, the **ePrivacy Directive of 2002**, commonly known as the Cookie Law. Like GDPR, it aims to protect customer privacy. 

The ePrivacy Directive is due to be replaced by more stringent legislation, the ePrivacy Regulation. (If you’re interested in the difference between EU directives and regulations, EU directives set out the goals for legislation but delegate the implementation of those goals to member states’ legislatures. EU regulations mandate both the goals and the implementation at an EU-wide level.)

{{% pull-quote %}}
 The draft ePrivacy Regulation goes beyond cookies and ad tracking. It applies to all electronic communications, including messaging apps, spam mail, IoT data transfer and more.
{{% /pull-quote %}}

The draft ePrivacy Regulation was first presented by the EU in 2017. However, it has to be agreed by both the European Parliament and the Council of the European Union. (The Council consists of government representatives of each EU member state.)

This is where it gets messy. Since 2017, the European Parliament and the Council haven’t been able to agree on the scope and detail of the ePrivacy Regulation.

That’s because some countries &mdash; widely thought to include the Nordic states of Finland and Denmark &mdash; want to strengthen the current ePrivacy Directive. They want users, for example, to be able to **set acceptance and rejection of tracking cookies** in their browsers, not on every site they visit.

But other countries, notably Austria and believed also to include those with sizeable digital marketing and advertising sectors, say this is bad for business. It’s thought the 27 EU member states are split down the middle on this issue &mdash; and they’re all being heavily lobbied by the tech industry.

So the draft regulation has been ricocheting back and forth between the European Commission and its Working Party on Telecommunications and Information Society as they try to agree its scope. In November 2020, the Working Party [rejected](https://data.consilium.europa.eu/doc/document/ST-12891-2020-INIT/en/pdf) the redrafted legislation once again.

What happens next? There are two possibilities. **Either a compromise will be reached**, in which case the legislation will be agreed. Because it takes time for legislation to be implemented, the soonest the ePrivacy Regulation could become law is 2025.

Alternatively, **the legislation cannot be agreed and is withdrawn** by the European Commission. But the EU has staked so much on it. It will be extremely reluctant to take that step.

That’s why I call it Schrodinger’s Law. It’s hard for us to know how to plan for any cookie-related developments because we simply don’t know what’s happening.

{{% ad-panel-leaderboard %}}

## So what should I do about cookies right now?

Different EU countries are currently implementing the ePrivacy Directive differently. Over in the UK, the ICO (the UK’s data protection authority) is taking a tough stance. It’s requiring [strict consent for analytics cookies](https://ico.org.uk/for-organisations/guide-to-pecr/guidance-on-the-use-of-cookies-and-similar-technologies/how-do-we-comply-with-the-cookie-rules/#comply15), for example, and has spoken out against cookie walls.

Until &mdash; and if &mdash; we get consistency from a new ePrivacy Regulation, if you’re based in an EU country, start by following the advice from your national Data Protection Authority. Then watch this space for developments around the ePrivacy Regulation.

{{% pull-quote %}}
 If you’re based outside the EU, make sure you’re giving EU citizens the options required under the GDPR and the ePrivacy Directive.
{{% /pull-quote %}}

However, when it comes down to the detail, there are times when I recommend taking a risk-based approach. That’s what we’ve done at Cyber-Duck &mdash; and here’s why.

Here’s **our original cookie notice**. You see these everywhere. They’re pretty meaningless &mdash; users just hit accept and continue on their way.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5015a98f-d1c6-4520-bbb9-4aa35c4a1a44/gdpr-update-original-cookie-banner.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5015a98f-d1c6-4520-bbb9-4aa35c4a1a44/gdpr-update-original-cookie-banner.png" width="800" height="" sizes="100vw" caption="It didn’t matter if the user had accepted cookies or not &mdash; Google Tag Manager (GTM) fired when they landed as cookies were enabled by default, meaning we would get our analytics data. (Image source: <a href='https://www.cyber-duck.co.uk/'>Cyber-Duck</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5015a98f-d1c6-4520-bbb9-4aa35c4a1a44/gdpr-update-original-cookie-banner.png'>Large preview</a>)" alt="Screengrab of cookie consent banner. It says ‘Learn how we use cookies to manage your experience and change your settings.’" >}}

But we wanted to be compliant, so we replaced it with this notice. You’ll see that tracking cookies are turned off by default &mdash; **in line with ICO guidance**. We knew there was a risk we would lose analytics data as GTM would no longer fire on first load.

Let’s see what happened.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/075a850f-3306-42ca-8991-ff8acc2d335e/gdpr-update-new-cookie-banner.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/075a850f-3306-42ca-8991-ff8acc2d335e/gdpr-update-new-cookie-banner.png" width="800" height="" sizes="100vw" caption="Our new cookie banner followed ICO guidelines, but... (Image source: <a href='https://www.cyber-duck.co.uk/'>Cyber-Duck</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/075a850f-3306-42ca-8991-ff8acc2d335e/gdpr-update-new-cookie-banner.png'>Large preview</a>)" alt="Screengrab of new cookie consent notice showing marketing and analytics cookies turned off by default" >}}

Problem solved? Actually, no. It just created another problem. The impact was far more significant than we expected:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6681c065-7e13-4aad-86d3-61d47fa952a3/gdpr-update-new-cookie-traffic.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6681c065-7e13-4aad-86d3-61d47fa952a3/gdpr-update-new-cookie-traffic.png" width="800" height="" sizes="100vw" caption="The new cookie consent caused our tracked traffic to collapse. (Image credits: <a href='https://www.cyber-duck.co.uk/'>Cyber-Duck</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6681c065-7e13-4aad-86d3-61d47fa952a3/gdpr-update-new-cookie-traffic.png'>Large preview</a>)" alt="Google Analytics screengrab showing tracked traffic fall when the new cookie consent was implemented" >}}

Look at the collapse in the blue line when we implemented the new cookie notice. We released the new cookie consent on 17 December and went straight from plenty of tracked traffic to almost zero. (The orange line shows the previous year’s traffic, for comparison.)

In both the before-and-after scenarios, the default option was by far the most popular. Most users just naturally click on “accept” or “confirm”. That’s tricky, because we now **know so little about the people visiting our site** that we can’t give them the best information tailored to their needs.

We needed a solution. Analytics and marketing data ultimately drive business decisions. I’m sure we all know how important data is. In this case, it was like putting money in a bank account and not knowing how much we’d spent or saved!

Some of the solutions that were posed include **design alternatives** (would removing the toggle, or having two buttons with a visual nudge towards the “accept” help?) Or would we enable analytics cookies by default?

For now, we’ve implemented a compromise position. Marketing and analytics cookies are on by default, with one clear switch to toggle them off:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81667310-5d1e-4715-9d6e-5bf12f1ab0db/gdpr-update-2nd-iteration-banner.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81667310-5d1e-4715-9d6e-5bf12f1ab0db/gdpr-update-2nd-iteration-banner.png" width="800" height="" sizes="100vw" caption="Then we iterated again. (Image credits: <a href='https://www.cyber-duck.co.uk/'>Cyber-Duck</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81667310-5d1e-4715-9d6e-5bf12f1ab0db/gdpr-update-2nd-iteration-banner.png'>Large preview</a>)" alt="Screengrab showing iterated cookie notice with marketing and analytics cookies switched on by default" >}}

And here’s what that’s done to our stats:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23ddeffe-cee5-436f-a91e-6551c596c15d/gdpr-update-2nd-iteration-traffic.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23ddeffe-cee5-436f-a91e-6551c596c15d/gdpr-update-2nd-iteration-traffic.png" width="800" height="" sizes="100vw" caption="This iteration brought back a chunk of attributable traffic. (Image credits: <a href='https://www.cyber-duck.co.uk/'>Cyber-Duck</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23ddeffe-cee5-436f-a91e-6551c596c15d/gdpr-update-2nd-iteration-traffic.png'>Large preview</a>)" alt="Google Analytics screengrab showing tracked traffic partially recover from 15 January" >}}

The new cookie banner was relaunched on 15 January. You can see our website traffic starts to pick back up again. However, we’re not getting the full data we were getting before as Google Tag Manager doesn’t fire unless a user chooses cookies.

The good news is, we are getting some data back again! But the story doesn’t end here. After we had **turned cookie tracking back on by default**, the attribution model got messed up. It wasn’t attributing to the correct channel in Google Analytics.

Here’s what we mean:

### Scenario 1: (Correct Attribution)

1. User lands on our website via a paid ad (PPC) or from the search result (organic)
2. User accepts cookies straight away.
3. The channel source is attributed correctly, e.g. to PPC.

### Scenario 2: (Incorrect Attribution)

1. User lands on our website via a paid ad (PPC) or from the search result (organic)
2. User visits a few other pages on our website without responding to the cookie banner prompt (banner appears on every page until it gets a response)
3. User finally accepts cookie banner after browsing a few pages.
4. Attribution comes through as direct &mdash; although they originally came from a search engine.

How does that work? When a user browses other pages on the site, **nothing is tracked until they respond to the cookie prompt**. Tracking only kicks in at that point. So to Google, it looks as though the user has just landed on that page &mdash; and they are attributed to Direct traffic.

Back to the drawing board.

**Note**: *I’m sure by now you’re starting to see a pattern here. This entire experience is new for us and there’s not a lot of documentation around, so it’s been a real learning curve.*

{{% ad-panel-leaderboard %}}

Now, how could we solve this attribution issue and stop users from navigating around the site until they’ve selected their cookie preference?

A **cookie wall** is one option we considered, but that would potentially push us further away from being compliant, according to the ICO. (Though you might like to try browsing their site incognito and see if they stick to their own guidance...)

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d657d06c-374e-4c0c-9ec0-0737366dd7da/gdpr-update-cookie-compromise.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d657d06c-374e-4c0c-9ec0-0737366dd7da/gdpr-update-cookie-compromise.png" width="800" height="" sizes="100vw" caption="In the end, we had to settle on a compromise. (Image credits: <a href='https://www.cyber-duck.co.uk/'>Cyber-Duck</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d657d06c-374e-4c0c-9ec0-0737366dd7da/gdpr-update-cookie-compromise.png'>Large preview</a>)" alt="Screengrab showing compromise cookie consent notice with tracking switched on by default" >}} 

But that’s what we’ve chosen to go with. The journey ends here for now, as we’re still gathering data. In the future, we want to **explore other tools** and the potential impact of moving away from Google Analytics.

So what’s everyone else doing?

Well, McDonald’s UK offers straightforward on/off buttons:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3138de66-b868-43c0-8735-2489f228e723/gdpr-update-mcdonalds.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3138de66-b868-43c0-8735-2489f228e723/gdpr-update-mcdonalds.png" width="800" height="" sizes="100vw" caption="McDonald’s UK gives straightforward cookie choices. (Image credits: <a href='https://www.mcdonalds.com/gb/en-gb.html'>McDonald’s UK</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3138de66-b868-43c0-8735-2489f228e723/gdpr-update-mcdonalds.png'>Large preview</a>)" alt="Screengrab of McDonald’s cookie consent offering three options: reject all, accept cookies and cookie settings" >}}

Coca Cola’s British site nudges you to accept by making the ‘reject’ option harder to find:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0488bcc-c323-43fb-be95-588cbface3ee/gdpr-update-coca-cola.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0488bcc-c323-43fb-be95-588cbface3ee/gdpr-update-coca-cola.png" width="800" height="" sizes="100vw" caption="Coca-Cola’s UK site nudges you to accept cookies. (Image credits: <a href='https://www.coca-cola.co.uk/'>Coca Cola UK</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0488bcc-c323-43fb-be95-588cbface3ee/gdpr-update-coca-cola.png'>Large preview</a>)" alt="Screengrab of Coca-Cola’s cookie consent notice with ‘accept all cookies’ highlighted" >}}

Whereas Sanrio just has an option to agree to ad tracking:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/328b6fc2-ace4-40ea-a069-d7956e8eb391/gdpr-update-sanrio.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/328b6fc2-ace4-40ea-a069-d7956e8eb391/gdpr-update-sanrio.png" width="800" height="" sizes="100vw" caption="Sanrio just gives the option to agree to cookies. (Image credit: <a href='https://www.sanrio.com/'>Sanrio.com</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/328b6fc2-ace4-40ea-a069-d7956e8eb391/gdpr-update-sanrio.png'>Large preview</a>)" alt="Screengrab of Sanrio’s cookie consent showing ‘Ok’ confirmation button" >}}

Hello Kitty, hello cookies.

Die Zeit offers free access if you accept tracking cookies &mdash; but for an untracked, ad-free experience you’ll have to pay:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5fc212a-3eff-4120-8883-661f8202670e/gdpr-update-zeit.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5fc212a-3eff-4120-8883-661f8202670e/gdpr-update-zeit.png" width="800" height="" sizes="100vw" caption="Die Zeit offers free access with cookies &mdash; but for an untracked experience, you have to subscribe. (Image credit: <a href='https://www.zeit.de/'>Die Zeit</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5fc212a-3eff-4120-8883-661f8202670e/gdpr-update-zeit.png'>Large preview</a>)" alt="Screengrab of Zeit’s cookie consent" >}}

And here’s one of my favourite dark patterns. This restaurant site only has the ‘Necessary’ cookies selected. But it nudges you to the ‘Allow all cookies’ big red button &mdash; and when you click that, the analytical and ad cookie boxes are automatically checked and set. [Give it a go here!](https://www.pinchos.se/)

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a7a173b-1844-4ae6-ae2d-d2063c71f360/gdpr-update-pinchos.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a7a173b-1844-4ae6-ae2d-d2063c71f360/gdpr-update-pinchos.png" width="800" height="" sizes="100vw" caption="Pinchos’ cookie consent is a good example of a dark pattern. (Imagae credit: <a href='https://www.pinchos.se/'>Pinchos.se</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a7a173b-1844-4ae6-ae2d-d2063c71f360/gdpr-update-pinchos.png'>Large preview</a>)" alt="Screengrab of Pinchos cookie consent" >}}

Even the EU isn’t consistent on its own sites.

The European Parliament’s cookie consent offers two clear options:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed83771d-3ab9-4d29-b3f5-5d34218dd527/gdpr-update-euro-parliament.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed83771d-3ab9-4d29-b3f5-5d34218dd527/gdpr-update-euro-parliament.png" width="800" height="" sizes="100vw" caption="The European Parliament’s cookie notice gives two clear options. (Image credit: <a href='https://www.europarl.europa.eu/portal/en'>European Parliament</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed83771d-3ab9-4d29-b3f5-5d34218dd527/gdpr-update-euro-parliament.png'>Large preview</a>)" alt="Screengrab of the European Parliament’s cookie consent" >}} 

The CJEU’s site isn’t so clear:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b16022cb-8280-491f-bdf3-537bd4a71ab6/gdpr-update-cjeu.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b16022cb-8280-491f-bdf3-537bd4a71ab6/gdpr-update-cjeu.png" width="800" height="" sizes="100vw" caption="The CJEU’s cookie consent offers three choices: necessary cookies, accept all and more information. (Image credit: <a href='https://curia.europa.eu/jcms/jcms/j_6/en/'>EU Court of Justice</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b16022cb-8280-491f-bdf3-537bd4a71ab6/gdpr-update-cjeu.png'>Large preview</a>)" alt="Screengrab of the CJEU’s cookie consent" >}}

While Europol’s site comes with two pre-checked boxes:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/359fdf24-ed49-458b-b2bb-b79473595601/gdpr-update-europol.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/359fdf24-ed49-458b-b2bb-b79473595601/gdpr-update-europol.png" width="800" height="" sizes="100vw" caption="Europol’s cookie consent has analytics cookies automatically checked. (Image credit: <a href='https://www.europol.europa.eu/'>Europol</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/359fdf24-ed49-458b-b2bb-b79473595601/gdpr-update-europol.png'>Large preview</a>)" alt="Screengrab of Europol’s cookie consent showing mandatory and tracking cookies checked" >}}

And if you look at the sites for the [German presidency of the Council of the European Union](https://www.eu2020.de/eu2020-en) (July&ndash;December 2020), at first it seems as if there’s no cookies at all:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa8c4e88-79f1-4f33-8943-45a738a1ddbb/gdpr-update-eu2020.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa8c4e88-79f1-4f33-8943-45a738a1ddbb/gdpr-update-eu2020.png" width="800" height="" sizes="100vw" caption="Cookies? What cookies? (Image credit: <a href='https://www.eu2020.de/eu2020-en'>eu2020.de</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa8c4e88-79f1-4f33-8943-45a738a1ddbb/gdpr-update-eu2020.png'>Large preview</a>)" alt="Screengrab of Germany’s EU2020 site showing no cookies and no cookie consent notice" >}}

When you land on the site, there are no cookie banners or prompts. A closer look, with cookie extension tools, shows that no cookies are being placed either.

So are they capturing any analytics data? The answer is yes.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e07adc6-6f25-4f5e-bf9e-52d0a039eab1/gdpr-update-piwik.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e07adc6-6f25-4f5e-bf9e-52d0a039eab1/gdpr-update-piwik.png" width="800" height="" sizes="100vw" caption="The eu2020.de site tracks users using Piwik, now Matomo. No cookies here! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e07adc6-6f25-4f5e-bf9e-52d0a039eab1/gdpr-update-piwik.png'>Large preview</a>)" alt="Screengrab of Matomo code from eu2020.de" >}}

We found this little snippet in their code, which shows they are using ‘Piwik’. Piwik is now known as [Matomo](https://matomo.org/), one of a clutch of new tools that help with cookie compliance along with [Fathom](https://usefathom.com/) (server-side tracking) and [HelloConsent](https://helloconsent.com/) (cookie management).

So **alternatives and solutions are emerging**. We’ll take a closer look at that next time &mdash; with new alternatives to third-party cookies that will help you take control of your data and get the insight you need to deliver optimum experiences to your customers. Stay tuned!

### Further Reading

- [Data protection](https://ec.europa.eu/info/law/law-topic/data-protection_en) (the EU’s site)
- UK ICO’s [Guidance On Cookies](https://ico.org.uk/for-organisations/guide-to-pecr/guidance-on-the-use-of-cookies-and-similar-technologies/how-do-we-comply-with-the-cookie-rules/#comply15)
- [GDPR Enforcement Tracker](https://www.enforcementtracker.com/), logs fines applied under GDPR
- [GDPR Checklist](https://www.cyber-duck.co.uk/insights/resources/gdpr-checklist), by Cyber-Duck &mdash; a great place to start
- Overview of [Data Protection Law in the United States](https://iclg.com/practice-areas/data-protection-laws-and-regulations/usa), by ICLG
- [GDPR &amp; CCPA Comparison Guide](https://fpf.org/wp-content/uploads/2018/11/GDPR_CCPA_Comparison-Guide.pdf), by DataGuidance and the Future of Privacy Forum
- [CCPA vs CPRA](https://iapp.org/news/a/cpra-analysis-the-good-and-bad-news-for-ccpa-regulated-businesses/), from IAPP
- [Security By Design](https://aws.amazon.com/compliance/security-by-design/) (Amazon)
- [How To Protect Your Users With The Privacy By Design Framework](https://www.smashingmagazine.com/2017/07/privacy-by-design-framework/), Heather Burns, Smashing Magazine

{{< signature "vf, il" >}}
