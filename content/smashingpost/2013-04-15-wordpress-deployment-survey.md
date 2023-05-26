---
title: How To Improve The Deployment Of WordPress Websites
slug: wordpress-deployment-survey
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/586dcd8f-1ab0-451a-90ec-e55efa828926/wp-11.jpg
date: 2013-04-15T10:09:52.000Z
author: kieran-masterton
description: >-
  As WordPress matures into a full-fledged CMS and more and more large online
  publishers come to rely on the platform, the practice of developing and
  deploying websites becomes increasingly important.
categories:
  - WordPress
  - Techniques (WP)
---
As WordPress matures into a full-fledged CMS and more and more <strong>large online publishers come to rely on the platform</strong>, the practice of developing and deploying websites becomes increasingly important. High-profile members of the WordPress community, such as core developer Mark Jaquith and Cristi Burca, have <a href="https://wordpress.tv/2011/08/20/mark-jaquith-scaling-servers-and-deploys-oh-my/">spoken on the topic</a> and built tools such as <a href="https://github.com/wp-cli/wp-cli">WP-CLI</a> and <a href="https://github.com/markjaquith/WP-Stack">WP Stack</a> to improve the professionalism of our administration and deployment.

But what I’m really interested in is the current state of WordPress deployment: how an average developer manages the deployment of their websites, and how can we improve as a community?

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Get The Most Out Of A Premium WordPress Theme](https://www.smashingmagazine.com/2013/02/get-the-best-out-of-premium-wordpress-theme/)
*   [Powerful WordPress Tips And Tricks](https://www.smashingmagazine.com/2013/09/powerful-wordpress-tips-and-tricks/)
*   [WordPress Functions To Make Blogging Easier](https://www.smashingmagazine.com/2013/06/five-wordpress-functions-blogging-easier/)
*   <span>[How To Improve And Refine Your WordPress Theme Development Process](https://www.smashingmagazine.com/2013/02/wp-theme-development-process/)</span>

In late July 2012, <strong>I conducted a short survey to help me answer these questions</strong>. The survey was open for three months and drew a modest but not insignificant 327 respondents. This article documents the results of the survey and draws some conclusions about where education is needed and how we can help each other become more professional when deploying our WordPress websites.

{{% feature-panel %}}

## The Demographic

In my survey, I asked a few questions to establish the demographic that’s working with WordPress; this was obviously already done in far greater detail with the <a href="#">WordPress user and developer survey</a>, but I felt that getting a sense of who was responding to this survey was important. Of the 327 respondents, 43% self-identified as developers, 10% as designers, 40% as both designers and developers and 7% other.

The vast majority were located in the North America (50%) and Europe (38%), with the following continents also registering: Asia (6%), Australia (4%), Africa (3%) and South America (1%). I also asked respondents <strong>how they would categorize the businesses they work for</strong>. Here’s how they responded:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26128ee0-d757-4d98-8ca6-257468946ff1/biz-type.jpg" alt="biz-type" width="500" height="330" /></figure>

The <strong>results were overwhelmingly in favor of freelancing (46%)</strong>, with small businesses (19%) and small agencies (17%) taking a close second and third place, respectively. These figures back up accepted knowledge that WordPress is largely used by small internal Web teams, regional Web agencies and freelancers. Finally, as with the WordPress user and developer survey, I asked respondents whether they made their living from WordPress. This was relatively evenly split, with a small majority of 59% saying yes.

That said, of those who identified themselves as developers, 67% said they earn their living from WordPress, which suggests that WordPress developers are generally more inclined to stick with one platform than designers, who are perhaps more agonistic.</p>

## Deployment Practices

Now we get to the meat of the survey, how respondents actually deploy their WordPress websites. Combined, the 327 respondents maintain 6,378.5 WordPress websites — yes, someone maintains half a WordPress website. The majority of respondents manage a fairly small number of websites, with 46% looking after fewer than 10. That said, an impressive 8% manage between 30 and 40 websites, and, incredibly, one person is responsible for 700. Below is a breakdown of the numbers.</p>

### Websites Maintained by Survey Respondents

<table class="table-overview"><br>
<tbody>
<tr>
<th><strong>Number of websites</strong></th>
<th><strong>Number of respondents</strong></th>
</tr>
<tr>
<td>Fewer than 10</td>
<td>149</td>
</tr>
<tr>
<td>10 - 20</td>
<td>109</td>
</tr>
<tr>
<td>20 - 30</td>
<td>26</td>
</tr>
<tr>
<td>50 - 100</td>
<td>7</td>
</tr>
<tr>
<td>100 - 200</td>
<td>4</td>
</tr>
<tr>
<td>200 - 500</td>
<td>1</td>
</tr>
<tr>
<td>500 - 1000</td>
<td>1</td>
</tr>
</tbody>
</table>

### Version Control

I asked all respondents whether they use version control and, if so, which software they favor. Astonishingly (at least to me), 45% of respondents said they do not use version-control software at all as part of their workflow. Of the remaining 55%, <strong>Git was by far the most popular</strong>, taking 41% of the vote, and Subversion surprisingly accounted for only 9%. Drilling down a little deeper, 28% of those who identify themselves as a developer stated that they do not use version control, and 48% of those who are both developers and designers said the same. Here’s a breakdown of overall responses on version-control software:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f89a4376-97db-4ed1-a49a-1c65a694a796/version-control.jpg" alt="version-control" width="500" height="330" /></figure>

Next, I asked respondents what method of deploying websites they favor. These I broke down into FTP, SFTP, SCP, SSH + version control, SSH + version control + Capistrano, and other. Again, <strong>somewhat shocking for me was to find that FTP took 49% of the vote</strong>, followed by SFTP (20%) and SSH + version control (17%). My preferred method, SSH + version control + Capistrano, got only 3% of the vote; but even with so low a number, I was pretty encouraged to hear that people out there take the time to work in this manner.</p>

### Environments

I asked respondents whether they maintain different environments for their WordPress websites — that is, whether they set up local, test, staging and live environments. Answering yes didn’t require that they run all of these environments, but simply that they differentiate between the website they develop on, the website on which they show changes to a client and the live website. The vast majority of respondents (75%) indeed do this, which is great news.

An important facet and constant pain point of running multiple environments is the need to alter URLs in the WordPress database when migrating the database from one environment to another. I asked respondents how they typically deal with this problem and gave them an open field to type their answer. Here are some answers that came up repeatedly. These aren’t actual responses, but rather my representation of groups of similar replies.
<blockquote>"I don’t migrate between staging and live databases."</blockquote>

<blockquote>"I don’t touch the database. I just export and import posts out of and into WordPress."</blockquote>

<blockquote>"I use Dave Coveney’s PHP script for finding and replacing URLs in the database, including those in serialized data."</blockquote>

<blockquote>"I do a find-and-replace on the SQL dump and the website’s files."</blockquote>

<blockquote>"It’s a massive pain in the arse, and I steer clear of it."</blockquote>

<blockquote>"I dunno. What is the best practice on this?"</blockquote>

### Cowboy Coding

Finally, to gauge how strictly people adhere to general best practices, I asked respondents whether they ever cheekily edit code on the live server. Let’s be honest: this question is only ever going to yield one outcome. As expected, a whopping 76% owned up to having tweaked some WordPress production code in their time.</p>

## What We’ve Learned

In reviewing the lessons learned, it’s important to say up front that I am not criticizing the development and deployment practices of the survey’s respondents. The goal was to identify the areas where we, as a community, can become more professional and to draw some conclusions on how we might achieve that. You’ll find no finger-wagging or hyper-critical feedback for developers — just broad conclusions drawn from the responses.</p>

### Version Control

First, clearly not enough of us are using version control in our everyday workflow. This is a fundamental tool for any developer, and for 61% of those who self-identify as a developer or as both a designer and developer to say that they don’t use version control indicates that effort is needed in the WordPress community to educate developers on the importance of source-control management.

Still, while not enough WordPress developers use version control, that so many who do use Git is very positive. I prefer the decentralized approach of Git, and while WordPress’ core team still uses (and will likely continue to use) Subversion, <strong>Git brings many benefits</strong>. Suppose a few teams are working on a project. Each team could write to its own repository, and then a senior member of the quality-assurance team or an administrator could merge changes from all of those repositories into a protected repository before deploying the website. This approach makes a lot of sense if the website you’re working on is large and members of your team are dispersed, and it’s why I favor Git.</p>

### Environments

While a lot has been done to grapple with the issues arising from WordPress storing URLs in the database, the problem goes beyond WordPress’ core and extends to plugins and even to the pesky URLs ending up in serialized data. This is a pain in the arse at best, and a complete time-suck at worst. There are many options for overcoming this, but the most common choice is either not to migrate data from environment to environment at all <strong>or to use Dave Coveney’s PHP script</strong>. Both have their problems. For me, the first just isn’t viable, and the second, while perfectly acceptable, isn’t automated enough and is pretty time-consuming. There has to be a better option.

Free and premium tools and plugins offer solutions to this problem. One that came up a lot in the survey’s results was BackupBuddy and its migration feature. I’ve played around with its functionality, and, while it works perfectly well, it does not (as yet) work with Multisite, and I actually found the process more arduous than using a find-and-replace script. One project of mine that has emerged from this survey is to automate the find-and-replace process with a tool for Capistrano.</p>

## Conclusion

The survey’s results have shown the need for more education on professional deployment practices. Mark Jaquith’s talk “<a href="https://wordpress.tv/2011/08/20/mark-jaquith-scaling-servers-and-deploys-oh-my/">Scaling, Servers, and Deploys, Oh My!</a>” is a must-watch for anyone deploying WordPress websites. And the <a href="https://github.com/markjaquith/WP-Stack">WP Stack</a> project on Github and <a href="https://github.com/wp-cli/wp-cli">WP-CLI</a> are also worth checking out if you’re interested in breaking free of the browser and speeding up your administration of WordPress websites.

For my part, I plan to start blogging more about professional WordPress deployment practices and to release more Capistrano tools on Github. Finally, I would love to hear in the comments section about the kinds of issues that you’d like to see covered in future posts and of any other projects that are moving this issue forward.

{{< signature "al" >}}

