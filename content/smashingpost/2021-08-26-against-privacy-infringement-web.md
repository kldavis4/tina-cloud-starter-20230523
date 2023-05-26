---
title: 'Pushing Back Against Privacy Infringement On The Web'
slug: against-privacy-infringement-web
author: robin-berjon
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbab17a6-483b-4e8e-b9f1-9ab583202df1/against-privacy-infringement-web.jpg
date: 2021-08-26T08:00:00.000Z
summary: >-
  The Web is still wrestling with issues we take for granted offline, privacy chief among them. These are steps The New York Times took to protect users’ data, and how you can too.
description: >-
  The Web is still wrestling with issues we take for granted offline, privacy chief among them. These are steps The New York Times took to protect users’ data, and how you can too.
categories:
  - Privacy
  - Security
  - Ethics
---

At the ripe old age of 25, [nytimes.com](https://nytimes.com) is now older than some of the people who work building it. Wikipedia turned 20 this year, and the first browser shipped 30 years ago. The Web has over 4 billion internet users and is nearing 2 billion websites. By this point, it’s reasonable to expect to have answers to most of the big, basic questions of how people and digital technology work with one another.

As you no doubt know, however, we don’t. We really don’t. If anything, questions of technology and society seem to be **piling up faster than we can address them**. I started working for The Times four years ago. Before that, I had done a range of tech work: developing sites at small web shops, product work with startups, consulting for household name tech companies, and heavy involvement in a range of [W3C](https://www.w3.org/) work. One of the things that drew me to The New York Times was the opportunity to work on some of those big unanswered questions in collaboration with excellent teams and with a strong ethical mandate.

Of these issues, perhaps the most surprising to find still unsolved is **privacy**. Outside of the digital realm, we make multiple privacy decisions a day and typically find them obvious enough that we barely notice they’re there. Is it okay to read that stranger’s DMs over their shoulder? Can I recount that intimate detail that a friend shared with me? Will my doctor repeat what I tell them of my symptoms to my boss? 

Weighing up whether we &mdash; or someone we speak with &mdash; may take personal information from one context and share it in another is something we do almost instinctively. If we required expert opinion for every such decision, ethicist would be a high-income profession. So why can’t we seem to put this one to rest online as well?

## The Digital Context

Several factors stand against us. The first is that [privacy is contextual](https://bookshop.org/books/10948192/9780804752374). We understand what may be shared to whom and how by using different frames for work, home, the subway, a doctor’s office, or the local neighborhood dive. But in our digital lives, everything is a slight variation on a glossy slab of plastic. We chat with friends on the same gadget we work on, speak in public through, and look up symptoms with. It is hard to develop cues for what counts as appropriate amidst such homogeneity.

A second factor is the **usefulness of third parties**. The modern development of complex digital products often requires relying on third parties one way or another. This is not necessarily bad. A company specializing in a clear service might have better data protection than a home-grown equivalent, and not all third parties are privacy-invasive. Some third parties work only for the first-party site and will not reuse user data elsewhere. For privacy purposes, they are indistinguishable from whatever the first party does. One example of this might be Fathom: it’s third-party analytics, but they have [openly published the method they use to ensure user privacy](https://usefathom.com/blog/anonymization). 

Conversely, other third parties insist on being **controllers of the data** they take from the users of your site and reuse it independently for entirely different purposes. The latter are clear violations of privacy, but Web technology gives no way for browsers &mdash; and therefore users &mdash; to tell them apart. Cracking open your ad blocker extension and counting the "trackers" might be easy but it tells you little about how privacy-invasive a site really is. It is hard to automate protection at the browser level without the ability to tell third parties apart.

A final factor we shan’t be coy about is that there’s **money to be made from this confusion**. Many of the biggest names in tech (and a host of smaller ones too) operate with business models that do nothing other than **convert privacy violations into money**. They often muddy the waters with widely-read positions that extoll a confounding picture of privacy often confused with security, transparency, complex privacy settings and check-ups, or with consent. It can be hard to progress on informed improvements to privacy when so much of the conversation on the topic comes from a place of confusion.

This might feel like a lot to fix at once, but not to worry: we can all make the Web better one website at a time. It’s easy to become paralyzed thinking that all data collection is a privacy issue. That’s not the case. You can **walk this path gradually**. The way I approach privacy for a given site is to first try to find a familiar everyday context that I believe is close to it. Reasoning from known everyday contexts makes it possible to tap into established norms for which we tend to have good intuitions. Because the digital world works differently, there is rarely a perfect one-to-one match, but starting with a concrete situation can help structure your thinking.

## Enter My Bookshop

Let us look at a bookshop and at how we can **incrementally change its privacy properties** by adding more details that render it increasingly like a modern commercial website. Hopefully, there is a point at which you will want to draw a line &mdash; and that point should tell you something about what is appropriate in a comparable context on the Web.

{{% feature-panel %}}

A bookshop makes for a decent **real-world comparison point** for an online publication. You go there looking for things to read. The people who work there can see you enter, and they might even recognize you from previous visits. If you’ve identified yourself, they may know your name, or at least have some moniker for you.

As you browse the shop, the staff can get a sense of what you’re looking at. They might not spy on it in great detail, but they’ll know which section you’re in and could easily notice which book you just pulled out. They can use that and ask you questions to offer recommendations.

It’s a **commercial environment**, and if you buy something there, depending on how you pay they might learn a little bit more about you, and share some of that data with a payment processing company of some sort.

At closer inspection, you notice that the shop has a few **video surveillance cameras** running. This makes you a little uncomfortable, but after a quick chat with the owner they reassure you that these are running on a local closed circuit such that the video never leaves the shop, is automatically kept for a maximum of 24 hours, and is only ever watched for the sole purpose of identifying theft. These properties &mdash; highly restricted access, short retention, clear and limited purpose &mdash; offer strong guarantees (assuming you trust the business) and limit how invasive the process is.

But, paying more attention, you notice a number of other smaller, more discrete cameras. They are dispersed throughout the store in a way that allows them to analyze which books you are looking at, which you pull out to read the blurb on, which you decide to buy.

The conversation with the bookshop owner is a bit more fraught this time. Those **video feeds** go to a number of companies in exchange for which they help pay a little of the shop’s costs or list the shop on neighborhood maps. You agreed to this by pushing the door open and stepping inside.

The owner is adamant that it’s safe, that the process is entirely “anonymous,” that these monitoring companies “only” use a hash of your facial biometrics to recognize you from shop to shop. What do you have to hide anyway? It’s an important part of making sure that the books stay cheap. Without that, only rich people would have books. Anything else would be bad for small businesses and poor people.

Flipping through the list of companies taking video feeds from this shop, you can’t find a name you recognize. Except for those two that seem to be taking video feeds from every single other shop as well.

Pushing the bookshop owner a little more, you come to realize they’re not very happy with those companies. They use the data they collect in the shop both to **compete with the bookshop** by selling books directly and to recommend other bookshops. They’re also using their position, informed by that data, to push for a model in which they run the infrastructure for all stores &mdash; why would a bookshop owner care about walls, shelves, lighting, is their value not just in the book selection? &mdash; and an increasing number of other shops have switched over to this worldwide strip mall model. The owner isn’t too sanguine about any of that. "But when you don’t comply they drop you off the map and send people to your competitors," they say.

As promised, finding an exact non-digital equivalent to the state of privacy on the Web is imperfect and has some slightly contrived corners. Yet the above is very close to what it’s like to operate a commercial publisher or an online store on the Web today.

In reading the above, **different people will draw the line at different places**. Some are entirely bought into the death of privacy and look forward to the promised bright future of big tech bureaucracy. At the other end of the spectrum, others will prefer a staff-less bookshop where they can pick their next read with nary a human ever seeing what it may be.

If you’re like me, you’ll draw the line somewhere around the addition of the CCTV system. I’m not excited about it, but if its data processing is properly limited and if it helps my favorite source of books to stay alive, I can live with it. I am not inclined, however, to accept the pervasive surveillance of my behavior &mdash; the primary effect of which is for a handful of large corporations to either absorb small shops or drive them out of existence.

None of these positions is inherently right or wrong, but we help our users if we agree on a *default* and set expectations to match it. I believe that a good starting point for a default that works for most sites that perform a relatively small set of related services is the *Vegas Rule*: **what happens on the site stays on the site**. (Including the parties that work for the site, and only for the site.)

{{% ad-panel-leaderboard %}}

## How Can We Build For Privacy?

What does this mean for those of us who build places on the Web that others visit? There is no one-size-fits-all answer to that. Last year, I wrote about how [*The Times* sees it](https://open.nytimes.com/how-the-new-york-times-thinks-about-your-privacy-bc07d2171531), but how you approach your own situation will depend on the specifics that you are dealing with.

I recommend **working on privacy iteratively**, with a plan to improve in gradual steps over time. In most cases, it’s unlikely that you’ll be able to deploy a catch-all Big Bang cleanup.

The first step towards making a site more trustworthy in its privacy is to **understand what is going on and why**. If you work on the tech or product side, you might have grown used to grumbling in dismay as the marketing team adds yet another tracker, which they refer to under harmless, cutesy euphemisms like “pixel,” that will slow down your site. But you might only have a limited understanding of why they do that in the first place. 

These overlaps are great opportunities to **build actual relationships** with other teams. They are trying to achieve something, and that something is probably covering at least some of your pay-check. But they also sometimes struggle to tell honest vendors from hoaxes and they can benefit from a greater understanding of the technology that underlies what they buy &mdash; which you can likely help with. If you’re on their side instead of complaining about them, you might not be able to remove all the trackers, but you’ll be in a position to make progress.

Once you have that relationship (or if you’re the person making those decisions), the next step is to make sure that each third party is held accountable. The reality of online business today is such that you might have to keep some trackers, but those that stay should be **provably effective**. By working closely with our marketing team, we were able to reduce the amount of data *The Times* shared with third-party data controllers by over 90 percent. Not only did that improve privacy, but it also improved performance. The second step is to develop a habit of healthy skepticism.

{{% pull-quote %}}
 Read the fine print so that your users don’t have to — it’s part and parcel of building a site that won’t betray your users’ trust.
{{% /pull-quote %}}

That free widget to make it easy to share pages on social media? It’s probably a data broker. That comments system you can drop at the bottom of your blog? [You might want to check that it’s not selling your users’ data](https://twitter.com/martingund/status/1207327648093003777). It’s not uncommon for a third party to strike deals with other third parties so that when you add one to your site it will inject the others as well, a practice known as [piggybacking](https://themarkup.org/blacklight/2020/09/22/blacklight-tracking-advertisers-digital-privacy-sensitive-websites). It’s a good idea to run your site through a tool like [Blacklight](https://themarkup.org/blacklight) now and then to make sure that nothing surprising is going on (though if you run ads there will only be so much you can do, sadly).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6e675d6-e150-417a-9ab7-5ab7608e5af0/1-against-privacy-infringement-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6e675d6-e150-417a-9ab7-5ab7608e5af0/1-against-privacy-infringement-web.png" width="800" height="574" sizes="100vw" caption="Just because your site visitors won’t read the fine print doesn’t mean you shouldn’t either." alt="Google note asking for key points of Google’s Privacy Policy to be reviewed" >}}

Finally, you of course want to be thinking about your users, but you should also be thinking about yourself! The business implications of sending your audience data to third parties are often poorly understood and are too rarely taken into account. Understanding your users, your readers, your customers is a key business asset. When you share your audience data with third parties, they benefit from that too &mdash; and they can use that data to compete with you.

If you run a shoe store and let a social network track your users so you can target ads to them there later, know that that data, which reveals who is interested in shoes, will also be used to show them shoe ads for your competitors.

If you host your e-commerce pages on a virtual strip mall owned by a company that also runs its own online shopping business, how long will it be before they use what they learn from your customers to outcompete you?

{{% pull-quote %}}
 Privacy isn’t just about ethics and earning the trust of your readers: it’s also a sound business strategy when, willingly or not, you participate in the data economy.
{{% /pull-quote %}}

## And How About We Fixed The Web, Too?

As a community, we can each work to improve our own little corners of the Web. But, collectively, we can do better. We can improve the Web and make it a better platform for privacy.

Perhaps the most important property of the Web is **trust**. You can browse around freely from site to site because you can trust that your browser will protect your security and that, even as those sites run code on your computer, they won’t endanger it. That is a strong promise, much stronger than what you can expect from native platforms, but when it comes to privacy it’s a promise that we have broken. As you browse freely from site to site, your privacy is not in trustworthy hands.

Still, things are looking up. Most browsers have delivered excellent work towards preventing tracking on the Web, and the biggest holdout, Chrome, has promised change in 2023. Projects like the [Global Privacy Control](https://globalprivacycontrol.org/) are [making headway](https://globalprivacycontrol.org/press). As **third-party cookies slowly become extinct**, industry stakeholders are working together to propose privacy-preserving standards that enable businesses to function on the Web without infringing on people’s privacy. 

Detailing all the proposals on the table would require a whole other article, but Apple’s [Private Click Measurement](https://privacycg.github.io/private-click-measurement/), Google’s [FLEDGE](https://github.com/WICG/turtledove/blob/main/FLEDGE.md), Microsoft’s [PARAKEET](https://github.com/WICG/privacy-preserving-ads/blob/main/Parakeet.md), or, if you’ll allow me this shameless plug, The New York Times’s [Garuda](https://darobin.github.io/garuda/) are all worth looking at, as is the work taking place in the [Privacy CG](https://www.w3.org/community/privacycg/). Some of the proposals discussed there, like Federated Learning of Cohorts (FLoC), have [run into trouble](https://www.theregister.com/2021/07/08/google_floc_changes/), but that only underscores the value in building a solid understanding of privacy in the Web community in order to develop these novel solutions.

As much as we’d all love to engineer our way out of these complex problems, that’s rarely possible. Solutions will require **cooperation between technologists and policymakers**. As technologists, there are several ways in which we can help. We can act as citizens and take part in policy debates. We can describe our systems in understandable terms, and explain what is riding on them. (You’d be surprised at how many bad descriptions of cookies there can be.) We can use our understanding of technology to [try to explore how what we build can create problems when deployed at large scales](https://berjon.com/stewardship/). 

Most importantly, when technology fails society we can make it our responsibility to imagine other ways in which it could work &mdash; even if they seem out of immediate reach. Technology is often presented as inevitable as if its current design were the only rational option rather than the accumulation of arbitrary decisions that it is. We hold large, often untapped power in our ability simply to say that “it doesn’t have to be this way” and to show what other paths exist.

**We build for users**, not to milk them of their data. The Web has made it hard for them to stand for themselves &mdash; it’s on us to do it for them. Few of us who work on commercial sites will be able to produce perfect privacy outcomes immediately, but this should not stop us from doing better. The tide has turned and a privacy-friendly Web now seems possible. We might yet get to check one of those big, basic questions off the list.

{{% ad-panel-leaderboard %}}

### Further Reading

- A great book to read to understand how privacy works is Helen Nissenbaum’s [Privacy in Context](https://bookshop.org/books/10948192/9780804752374). A shorter overview is available in Matt Salganik’s [Bit by Bit](https://www.bitbybitbook.com/) which you can [read online](https://www.bitbybitbook.com/en/1st-ed/ethics/dilemmas/privacy/).
- [Privacy is Power](https://www.penguin.co.uk/books/1120394/privacy-is-power/9781787634046.html) by Carissa Véliz offers an effective and well-documented overview of why privacy matters.
- James C. Scott’s classic [Seeing Like A State](https://bookshop.org/books/seeing-like-a-state-how-certain-schemes-to-improve-the-human-condition-have-failed/9780300246759) presents a dire overview of how society-level engineering can fail, often in catastrophic ways, which includes an extensive description of the problems brought about by “legibility”, which is what collective infringement of privacy leads to.
- Maria Farrell’s [This Is Your Phone On Feminism](https://conversationalist.org/2019/09/13/feminism-explains-our-toxic-relationships-with-our-smartphones/) is an outstanding description of how we love our devices but don’t trust them, and of how love without trust is the definition of an abusive relationship.
- The W3C’s Technical Architecture Group (TAG) is working on a set of privacy definitions to help support discussions in the Web community. The output from that isn’t baked yet, but it is being built based on a blend of the [Principles of User Privacy (PUP)](https://darobin.github.io/pup/) and the [Target Privacy Threat Model](https://w3cping.github.io/privacy-threat-model/).
- In this article, I could only cover some of the basics, but one important concern in privacy is how data collection affects us at the collective instead of the individual level that we too often fixate on. Salomé Viljoen’s [Democratic Data](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3727562) covers that issue very well.
- Woodrow Hartzog and Neil Richards have written so many excellent articles on privacy that it’s hard to pick a favorite, but I would suggest [Taking Trust Seriously In Privacy Law](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2655719) as a great place to start. Don’t be daunted by the “law” part, it’s really about trust.
- Looking at a broader issue, [Re-Engineering Humanity](https://bookshop.org/books/re-engineering-humanity-9781107147096/9781108707640), by Brett Frischmann and Evan Selinger, is a great description of how we can misuse technology to shape people against their interests.
- More on the advertising side, [Subprime Attention Crisis](https://bookshop.org/books/re-engineering-humanity-9781107147096/9781108707640) by Tim Hwang explains why we should worry about online advertising and the businesses it supports.

{{< signature "vf, il" >}}
