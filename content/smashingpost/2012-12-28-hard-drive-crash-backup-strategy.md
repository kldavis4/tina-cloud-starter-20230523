---
title: My Hard Drive Crashed... And What I Learned From It
slug: hard-drive-crash-backup-strategy
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02938308-e72c-406e-a65d-d948a0dc71b7/hard-drive.jpg
date: 2012-12-28T21:04:29.000Z
author: ben-gremillion
description: >-
  During an emergency is a bad time to plan for one. It’s the feeling one might
  get jumping from a plane before checking one’s parachute. That’s one
  experience I’d rather avoid, but it happened. Not the skydiving part. My OS
  was dying, and I wasn’t prepared.
categories:
  - Tools
  - Workflow
---
The most valuable part of a computer is also its most fragile: <strong>Data</strong> are the wealth of a digital lifestyle, a currency of which many notes are irreplaceable. At least, that’s how I felt staring at a “Confirm you want to wipe your hard disk” message, my finger poised over the mouse.

Recommended reading: [What To Do When Your Website Goes Down](https://www.smashingmagazine.com/2010/12/what-to-do-when-your-website-goes-down/)

People who make websites face a triple threat: Live websites need backups; test environments need backups, especially when they double as backups for live websites. <a title="Subversion | software | Apache" href="https://subversion.apache.org">Subversion</a> and <a title="Everything is Local | software | Git" href="https://git-scm.com">Git</a> provide safety nets in case of data loss. But there are also support files: Photoshop files, fonts, reusable jQuery snippets — not to mention music collections, an essential part of many creative processes.

{{% feature-panel %}}

I kept regular backups of many files using Apple’s Time Machine. But “many” is not “all,” and just then my Mac was too erratic for me to tell which fraction I had missed. After copying vital files to a handful of spare hard drives, I took a breath, formatted the disc and reinstalled the OS.

An hour later I was dismayed to see how many files I’d failed to back up. Photoshop files, local test websites, PDFs and most text files were safe. But passwords saved in the OS, cached emails, FTP bookmarks, application preferences and serial numbers, browser history, plugins, color swatches, copies of old browsers for testing… Gone.

Anything digital is susceptible to loss. For a recovering digital packrat like myself, who lives (and now dies) by the Web, data loss is a disaster akin to a tornado, which may also destroy backups kept in the same office as the original files. Fire, theft, spilled coffee, overwritten files, disgruntled coworkers, zombie attacks — I played out nightmare scenarios in my head. Then I began to research better ways to safeguard my digital life.</p>

## Two Safeguard Services

Offsite backup systems help with disaster recovery by storing versions of files in secure facilities. Many services exist, but I compared the $50-per-year <a href="https://www.backblaze.com">Backblaze</a> service to $50-per-year <a href="https://crashplan.com">CrashPlan</a>+ Unlimited package. I’d read reviews of both before and often saw them compared against each other. Which was better? I wanted to find out.

My test environment was a 2011 MacBook Air running OS X 10.8.2. I tested backups from four different locations over a period of three weeks. <strong>Important note:</strong> While the online backup services I tested should also work on Windows machines, I didn’t have access to a computer with Windows OS on which to test. Anyone with backup experience on Windows or with services other than Backblaze and CrashPlan is welcome to share their experience in the comments.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec297284-614a-4167-bb64-793eacea3f75/backups-daisydisc.png" alt="Screenshot of DaisyDisk's colorful diagram of my hard drive" />

After two weeks of backups, I discovered a way to prioritize data. Using <a title="See what takes up your disk space | software | Software Ambience Corp." href="https://www.daisydiskapp.com/">DaisyDisk</a>, I determined that the largest folder — my music — was also the most replaceable. I instructed Backblaze and CrashPlan to avoid music for seven days, forcing them to focus on documents and Web files. Once I saw that my vital websites and support files were in both services, I felt safe enough to let them archive my music.

To expedite the backups and placate my neighbors, I also backed up overnight for two weeks, using <a title="Don’t let your Mac fall asleep | software | Lighthead" href="https://lightheadsw.com/caffeine/">Caffeine</a> to keep my Mac awake and <a title="Calibrating your computer’s battery for best performance | article | Apple" href="https://support.apple.com/kb/HT1490">calibrating my battery</a> after 10 days of continuous nightly charges.</p>

## Starting Backblaze

Backblaze customers may install an application for OS X (10.5 and up) or Windows (XP, Vista and 7). On OS X, Backblaze is accessible as a System Preferences pane. Whether Mac or PC, while a user’s computer is on and connected to the Internet, Backblaze uploads the contents of the hard drive to a custom facility in San Francisco. The app was <em>tiny</em>, occupying 829 KB on my hard drive and using 10 MB of RAM.

After a quick hard-drive scan, Backblaze determined I had 92.7 GB of files ready to be backed up, mostly in my <code>User</code> folder. As advertised, it proceeded to copy my files any time my Mac had access to Wi-Fi.

The nature of Backblaze is set and forget, which I often did. Aside from its menu bar icon and an occasional network lag, the application did not draw my attention. I could view my archive through Backblaze’s website the day after installation.</p>

## Starting CrashPlan

Like Backblaze, CrashPlan uploads selected sections of a hard drive to the service’s facility in <a href="https://www.code42.com/about.html">seven cities around the world</a>. It also works in the background, avoiding notice unless summoned. To that end, CrashPlan for OS X installs two applications: one program accessible from its menu item, and a second full program that provides statistics, account information and options to store data on devices other than CrashPlan’s servers. The menu bar shows how the current backup is proceeding, the current file being uploaded and pausing options.

Upon first launching, CrashPlan informed me that 101.6 GB was ready to be uploaded. I wasn’t able to determine why it saw more files than Backblaze. Backblaze claims it does not upload podcasts, but that didn’t account for 10 GB.</p>

## Comparative Features

From a casual glance, Backblaze and CrashPlan are similar enough to spawn their own patent war. Both systems share the same goal: to provide peace of mind by saving customers’ data on remote servers. Both systems work the same way, copying files via the Internet while the user works. But they differ in more than options, prices and controls. The more I looked, the more their differences became apparent.</p>

### Pause

Both Backblaze and CrashPlan feature pause buttons, the need for which I discovered after three days.

Editing a WordPress theme on a live website, I stepped away for a cup of liquid enthusiasm while my FTP program connected to the server. When I came back, it was still connecting. Even normally fast websites took up to 40 seconds to load. This was the kind of slow usually reserved for <a title="Top 10 worst IT disasters of all time | ZDNet | Colin Barker" href="https://www.zdnet.com/top-10-worst-it-disasters-of-all-time-1339284034/">Murphy’s Law</a>. (True to form, it was an emergency PHP error on deadline.) The culprit was running both backup services.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcdd7014-7e0f-4560-a08d-abefe8a78d80/backups-bb-dropdown-dashboard.png" alt="Backblaze's drop-down menu controls" />

Users may set Backblaze to run once per day or manually, but the application defaults to “continuous.” Continuous backups may be paused until told to resume. It also resumes upon log-in — say, after a reboot.

Whereas Backblaze stays paused until told otherwise, CrashPlan users may pause with a timer for 1, 2, 4, 8, 12 or 24 hours. CrashPlan’s “resume later” mentality was handy when, focused on my work, I would forget to reenable it. That cut both ways. More than once, I noticed a sudden Internet slowdown as CrashPlan reactivated. Backblaze gave me no such surprises.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/184e1331-34d5-4da2-955b-db3d2dc94d8f/backups-cp-dropdown-dashboard.png" alt="CrashPlan's drop-down menu controls" />

Both services stopped running when I put my Mac to sleep, switched users or otherwise logged out of my user account. However, both services can back up the entire contents of a computer’s hard drive — including user accounts not set to run the services. If someone else uses your Mac and you need access to their account, Backblaze and CrashPlan are happy to oblige.

Recommended reading: [How to find out why your website stopped working](https://www.smashingmagazine.com/2013/07/how-to-find-out-why-your-website-stopped-working/)

### Bandwidth

Although both applications stay out of the way, the fact that I was moving about 200 GB across the Internet did not go unnoticed. Neither backup service caused my Mac to slow down, but both I and people on the local network saw Internet speeds take a hit any time I had one or both running.

Slowdown was especially apparent as I was editing live websites. Websites at <a title="Web hosting | service | Rackspace US" href="https://www.rackspace.com">Rackspace</a>, <a title="Web hosting | service | New Dream Network" href="https://dreamhost.com">Dreamhost</a> and <a title="Web hosting | service | Pair Networks" href="https://www.pair.com">Pair</a> became tedious with either service running. Even the act of refreshing directories with <a title="Transmit for Mac | software | Panic" href="https://www.panic.com/transmit">Transmit</a> disrupted my train of thought. But were the problems consistent? And which service caused more lag?

To measure their impact on Internet access, I uploaded the same files, totaling 1.5 MB, to a remote Web server via FTP from different locations and different times of day.

One result was obvious. Locations with more than 10 laptops, smartphones and iPads jostling for bandwidth saw varied results. Especially because each test took between 5 and 15 minutes, demand for local Wi-Fi changed as people came and went. But running either Backblaze or CrashPlan always slowed my FTP upload and download time, regardless of the crowd.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d311ef9a-c840-48f1-b199-2bab8c5cc443/backup-speed-test-diagram.png" alt="Infographic of which service reduced my FTP speeds" />

The graph above shows the time it took to upload files to a website while either CrashPlan or Backblaze was running. Seven times, uploads were faster while CrashPlan was running than when Backblaze was. Four times, the opposite was true. Three times were too close to call. One time, uploading to FTP while Backblaze was running was <em>faster</em> than uploading with Backblaze off, a testament to erratic bandwidth usage at coffee shops.

Anecdotally, I learned to stop both services while working on live websites (transferring WordPress from local to live servers) or while otherwise performing network-intensive tasks. The blue shows upload times with neither Backblaze nor CrashPlan running. Not only was it faster in 13 of 14 tests, but turning off both services doubled my FTP speed.

At least, it <em>felt</em> like a speed boost. By chance, during one test I also updated software on my iPad via Wi-Fi. I thought the updates had stalled until I disabled the backup services.</p>

## Recovery

Backup is half the story. Getting files back is the other. Hopefully, few people will be parted from their data. But if the worst happens, customers of both Backblaze and CrashPlan can recover files via the Web. Customers can also use CrashPlan’s application and iPhone app to recover files — at least, on paper.</p>

### Backblaze’s Straightforward Process

Backblaze’s secure website lets users browse their files as they would their computer’s file structure. After I selected random HTML, CSS, JPG and PNG files from different folders for recovery, an email notified me that my files were ready on the “My restores” page. The selected files downloaded as a single ZIP file. Customers may also request their files to be sent on a USB jump drive for $99 or on a hard disk for $189.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/379d53a8-5689-4d91-8b83-f032376c9f75/backup-bb-recovery-screen.jpg" alt="Recovering files on Backblaze's website" />

### CrashPlan’s Many Options

The full CrashPlan application allowed me to select backed-up files to download to a destination folder on my Mac. Although CrashPlan warned me that it was “unable to restore until we have synchronized with the destination,” my files downloaded with no fuss. But I made the mistake of choosing my already-crowded desktop to receive a dozen recovered files. This differed from Backblaze, which downloaded one ZIP file that contained one folder.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8204eb2-b3cc-4ff0-9e48-d07b1b43d985/backup-cp-recovery-screen.png" alt="Recovering files in CrashPlan's application" />

Users may also restore files from CrashPlan’s Web application, although my experience indicated otherwise. While I had no trouble accessing my online account, five times over one week the website informed me it was “unable to log into server” to recover files. CrashPlan’s tech support said recovery via the Web was a known issue but had no estimate of when the problem would be fixed.

I never had problems recovering files from CrashPlan’s app for OS X. The iPhone app was a different story.</p>

### Backup to iPhone

<a title="iPhone app | software | CrashPlan" href="https://itunes.apple.com/us/app/crashplan/id462565520?mt=8">CrashPlan’s iOS app</a> (v1.3.2) allows users to browse and download their saved files to their iPhones. As with the OS X application, I navigated a copy of my Mac’s file structure by tapping the appropriate folders.

Tapping a single JavaScript, CSS, TXT or HTML document downloaded a copy of that file to my phone, after which I could read it as a text file in the CrashPlan app. The app let me copy text, email the file or open in other text-savvy apps, such as Evernote.

Rather than show source code, the app displayed HTML files as Web pages, including CSS styling, right down to clickable email links that opened my iPhone’s Mail app. Thus, I couldn’t tell, for example, whether a given HTML file had Google Analytics installed. PHP, JavaScript and CSS were legible as unformatted source code.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d3d6658-bd9a-4af9-ab7c-cd46cad9628f/backup-cp-iphone-screen1.jpg" alt="Recovering files in CrashPlan's iPhone app" />

For JPG and PNG images, the CrashPlan app offered to email, open in image-savvy apps or save to my photo roll. Files that it could not read — such as Pixelmator’s PXM files — were displayed as an icon, along with the file size and a “Send by email” option.

The app had two significant limitations. First, I could recover only one file at a time. Granted, an iPhone is not the ideal destination to recover hundreds of files. But if you want to restore whole websites, be prepared for a lot of tapping.

Secondly, a week after I recovered a few files with the iPhone app, some of those files did not appear on my phone. Although I downloaded a WordPress plugin, for example, according to the app, my “Downloads” folder was empty.

Backblaze has no iOS app — yet. At the time of writing, the company has only <a title="No app yet | tweet | Backblaze" href="https://twitter.com/backblaze/statuses/256897871566213120">hinted that it is developing an app</a>.</p>

## Options Abound

The services covered here aren’t the only two that sell peace of mind. Services such as <a title="Software backups | service | Mozy" href="https://mozy.com">Mozy</a> and <a title="Software backups | service | Carbonite" href="https://www.carbonite.com">Carbonite</a> follow the same approach: back up all of a customer’s data to a remote, secure location. But design agencies and Web developers with dedicated computers might find advantages in selectively saving.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1075294c-a8d8-4ff7-a392-130b9db1a832/backup-mozy.screenshot" alt="Mozy's product page" />

### LayerVault

Aimed at creative users, <a href="https://www.layervault.com">LayerVault</a> targets Adobe CS files, with an appropriately visual user interface. Its service includes full-sized previews of changes over time, collaborative change tracking and simple editing tools.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/134eec13-fb99-4cf6-8b1c-6b43b47d031a/backup-layervault.screenshot" alt="LayerVault's tour page" />

### Dropbox

Dropbox keeps more than the files that people entrust to it; <a href="https://www.dropbox.com/help/11/en">it keeps versions and deleted files</a> for 30 days as well.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff3634b3-0ec7-449f-b88a-bfd8e73254a2/backup-dropbox-versions.screenshot" alt="Dropbox's versions page" />

### Evernote

This free <a href="https://evernote.com/evernote/">note-taking software</a> captures any type of information users throw at it. While Evernote won’t back up files on one’s hard drive, it is a good repository for HTML, CSS and JavaScript snippets and commonly used JPG and PNG files. Evernote notebooks can be shared, enabling a Web design team to collaborate on the same library.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b4c3cc5-da88-4731-881c-f94b9e24b950/backups-evernote.screenshot" alt="Evernote's application" />

### Backupify

While Google Drive (née Google Docs) resides in a secure facility, <a title="" href="https://support.google.com/drive/bin/answer.py?hl=en&amp;answer=2405957&amp;topic=2428743&amp;ctx=topic">Google states</a> that deleted files are gone forever. <a title="" href="https://backupify.com">Backupify</a> protects Google Drive and Gmail from users’ accidental deletions.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0198a6fa-81df-4047-8740-a6afcccf5d66/backup-backupify.screenshot" alt="Backupify screenshot" />

### Backup Buddy for WordPress

Designers who use WordPress have many options to save their websites, both local and remote. Starting at $75, <a title="Backup Buddy | software | iThemes Media" href="https://ithemes.com/purchase/backupbuddy/">Backup Buddy</a> preserves and restores both the files and database of a WordPress website. If you have the files or don’t have the budget, try a <a title="Backing Up Your Database | article | Automattic" href="https://codex.wordpress.org/Backing_Up_Your_Database">database-only solution</a>, such as <a title="WP DB Manager | software | Lester Chan" href="https://wordpress.org/extend/plugins/wp-dbmanager/">WP DB Manager</a>.</p>

### Backup and Migrate for Drupal

Designers on Drupal can use the <a href="https://drupal.org/project/backup_migrate">Backup and Migrate module</a>, which does what it says. Drupal also recommends <a title="Backing up a site | article | Drupal" href="https://drupal.org/node/22281">other backup strategies</a> to save a website.</p>

## Choosing a Service

No one strategy applies to every user’s needs. But there’s enough overlap between Backblaze and CrashPlan to give would-be customers pause.

Ostensibly less developed, Backblaze offers fewer options, making for a streamlined service. One pricing plan and one application means that new customers can begin saving their data minutes after reading the sales pitch. <a title="Business backup, consumer price | service | Backblaze" href="https://www.backblaze.com/business.html">Its business package</a> follows the same prices but combines billing and data management for many computers into one account. The <a title="Buy now | service | Backblaze" href="https://secure.backblaze.com/buy.htm">price per month</a> decreases as customers buy more time: $95 for two years, $50 for one year and $5 per month.

CrashPlan plays to different digital needs with the following:

*   [Four plans for home users](https://www.crashplan.com/consumer/compare.html), one of which is free;
*   [Two for business users](https://www.crashplanpro.com/business/store.vtl), one of which may be purchased monthly, annually or every two years;
*   [A build-your-own package for enterprise](https://www.crashplan.com/enterprise/store.vtl), based on the number of devices to be backed up, the number of years to use the service and optional support.
*   The ability to back up to other computers or hard drives for free.

Both services worked well in my tests. While Backblaze delivers what it promises and no more, CrashPlan struck me as a business that targets specific markets. After using both for several weeks, I found Backblaze sufficient for my work. Your experience will vary, of course, and at the time of writing I have another 49 weeks with both. Which will I prefer this time next year? Time will tell.

Either service works better than doing nothing, as I discovered when I wiped my hard drive back to factory settings. Backblaze’s motto could speak for every service: “Back up, before you wish you had.”

{{< signature "al" >}}

