---
title: 'Eliminating Known Vulnerabilities With Snyk'
slug: eliminating-known-security-vulnerabilities-with-snyk
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5d31571-1063-4f2a-a495-fee3f58e1459/snyk-opt.png'
date: 2016-01-13T15:48:06.000Z
author: guypodjarny
summary: ->
  Over the time, OSS has turned into crowd-sourced marketplaces and this big range open source functionality is great, but it also carries big risks. Whenever you are running a stranger’s code inside your applications, you might question yourself "Do you know if these authors understand or care about security?" or "Do you know if they have vulnerabilities?" A good way to start acknowledging and handling this risk is to address the known vulnerabilities in your dependencies and Snyk makes it easy for you to find, fix and monitor these  vulnerabilities in Node.js.
description: >-
  Open Source packages carry big security risks. Snyk makes it easy for you to find, fix and monitor the known vulnerabilities in Node.js to easily address these vulnerabilities in your dependencies.
categories:
  - Coding
  - Performance
  - Security
---
The way we consume **open source software (OSS) dramatically changed** over the past decade or two. Flash back to the early 2000s, we mostly used large OSS projects from a small number of providers, such as Apache, MySQL, Linux and OpenSSL. These projects came from well&ndash;known software shops that maintained good development and quality practices. It wasn’t our code, but it felt trustworthy, and it was safe to assume it didn’t hold more bugs than our own code.

Fast&ndash;forward to today and OSS has turned into crowd&ndash;sourced marketplaces. Node’s [npm](https://npmjs.com/) carries over 210,000 packages from over 60,000 contributors; RubyGems holds [over 110,000](https://rubygems.org/stats) gems, and Maven’s central repository indexes [nearly 130,000](https://search.maven.org/#stats) artifacts. Packages can be written by anybody, and range from small utilities that convert [milliseconds](https://www.npmjs.com/package/ms) to full&ndash;blown [web](https://www.npmjs.com/package/express) [servers](https://www.npmjs.com/package/hapi). Packages often use other packages in turn, ending with a typical application holding hundreds if not thousands of OSS packages.

This wealth of open source functionality is awesome, **but it also carries risk**. You’re running a stranger’s code inside your applications. Do you know which packages you’re running? Do you know if their authors understand or care about security? Do you know if they have vulnerabilities?


The web community needs multiple new tools and practices to help us track and scrutinize these components &mdash; and [Snyk](https://snyk.io/) takes on the security part of the story.

## Security Risks And Known Vulnerabilities

Running untrusted code inside your system poses a broad security risk. Tackling it isn’t simple, but **a good place to start is by addressing known vulnerabilities**. These are publicly disclosed security bugs, typically found and logged by users, or intentionally found and reported by security researchers. Being public makes these issues the [easiest ones for attackers to find and exploit](https://www.theregister.co.uk/2015/02/23/hp_hack_vulnerable_threat_study/), and so very important to address.

Right now, roughly 14% of the top npm packages carry known vulnerabilities. The stats are far worse for full applications: **over 80% of Snyk users find vulnerabilities when testing their applications**. Some of these issues are minor in nature, and some are very severe. You can see a live demo of a hacker exploiting one such vulnerability in [this video](https://www.youtube.com/watch?v=iXA14OFXxZA) (roughly four minutes in).

Fortunately, there’s a new free tool that can help you find and fix vulnerabilities in Node.js &mdash; [Snyk](https://snyk.io/). This article will walk you through how you can use Snyk to make your applications more secure.

{{% feature-panel %}}

## Getting Started

First off, you’ll need a project to test. If you don’t have one handy, you can use the demo application we’ll review in this article, [snyk-demo-app](https://github.com/Snyk/snyk-demo-app). Simply run these lines to clone it and install its dependencies:

<pre><code class="language-bash">git clone https://github.com/Snyk/snyk-demo-app.git
cd snyk-demo-app
npm install</code></pre>

Now that you have a project to test, you need to install Snyk from npm, change directory to your project’s folder and run Snyk’s [Wizard](https://snyk.io/docs/#wizard). We’ll install Snyk as a global tool for now; later we’ll touch on using it as a local dependency of your automated tests. Run the following in your project’s folder:

<pre><code class="language-bash">npm install –g snyk
snyk wizard</code></pre>

As its name implies, the wizard is a guided walkthrough. It walks you through finding and fixing the issues found through upgrades and patches, and creates a Snyk policy (a *.snyk* file) with your decisions. The wizard leverages four other Snyk commands &mdash; [`auth`](https://snyk.io/docs/#authentication), [`test`](https://snyk.io/docs/#test), [`protect`](https://snyk.io/docs/#protect) and [`monitor`](https://snyk.io/docs/#monitor) - which we’ll explain as we advance.

## Authentication

If this is the first time you use Snyk, the wizard will first ask you to register using your GitHub account. Note that **Snyk does not require access to your repositories**. It only requests access to your email, using GitHub as an authentication system.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d0e5b08-fa5b-487a-802f-3a2706641837/snyk-wizard-auth-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d0e5b08-fa5b-487a-802f-3a2706641837/snyk-wizard-auth-preview-opt.png" width="500" height="175" alt="screen showing Snyk Wizard Authentication" /></a><figcaption>Snyk wizard authentication.</figcaption></figure>

Once authenticated, the wizard will get an API key to store locally and get on with the testing. The same authentication process can be done by running [`snyk auth`](https://snyk.io/docs/#authentication), or running [`snyk auth &lt;api-key&gt;`](https://snyk.io/docs/#authentication) (especially useful when integrating Snyk into your build/continuous integration (CI) system).

## Testing

The next step is to find the vulnerabilities. The wizard will traverse the local project and collect the packages it uses (note this means you should only run it *after* you run `npm install`). It then posts this list to the Snyk service, where they’re matched against Snyk’s [open source vulnerability database](https://github.com/Snyk/vulndb). This test also can be performed by running [`snyk test`](https://snyk.io/docs/#test), which is useful when integrating Snyk into your CI (more on that later).

Once the vulnerabilities are determined, the wizard will go through them and guide you through the remediation steps needed. It remembers the answers you give, and when the questions end it makes the changes you asked for.

Let’s go through the findings on the snyk demo app.

You can see the wizard found 11 vulnerabilities in the 314 dependencies used. The first one is a high severity issue in a direct dependency called bassmaster. There’s only so much detail we can share in a terminal, but you can use the [info link](https://snyk.io/vuln/npm:bassmaster:20140927) to get more information about the vulnerability itself.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7ff4dde-bd5f-4913-ab06-cf8a94e7a53c/snyk-wizard-bassmaster-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7ff4dde-bd5f-4913-ab06-cf8a94e7a53c/snyk-wizard-bassmaster-preview-opt.png" width="500" height="149" alt="screen showing Snyk Wizard Upgrade Bassmaster Prompt: 314 dependencies tested, 11 vulnerabilities found" /></a><figcaption>Snyk Wizard Upgrade Bassmaster Prompt.</figcaption></figure>

In many cases, disclosed vulnerabilities are fixed shortly after they’re discovered, and all you need to do is upgrade to the relevant version. When that’s possible, upgrade is the cleanest and best way to address such a security bug. In the case of bassmaster, all we need to apply is a ‘fix’ upgrade, making the decision to upgrade a no brainer.

Next, the wizard reports three vulnerabilities in the hapi@10.5.0 dependency. This typically happens when you are several versions behind the latest version, and in the meantime multiple vulnerabilities have been found and fixed. In this case, clicking [the info link](https://snyk.io/test/npm/hapi/10.5.0) will show three vulnerabilities fixed in version 11.0.0, 11.1.3 and 11.1.4 of hapi.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5b74986-9263-426d-a399-ac58cd616c9a/snyk-wizard-hapi-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5b74986-9263-426d-a399-ac58cd616c9a/snyk-wizard-hapi-preview-opt.png" width="500" height="99" alt="screen showing Upgrade to hapi@11.1.4 selected" /></a><figcaption>Snyk Wizard Upgrade Hapi Prompt.</figcaption></figure>

The wizard’s default suggestion is to upgrade to the latest version, addressing all three issues, but you can also choose to review and act on each vulnerability separately.

Next, we see that a direct dependency, falcor-router-demo@1.0.3, introduced three vulnerabilities. The vulnerabilities in this case aren’t in the `falcor-router-demo` code, but rather in the dependencies it pulls in. This is a very common scenario, as most of the packages used by your application are actually pulled in indirectly.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6d81609-bb8a-42be-a59f-a762373604d7/snyk-wizard-falcor-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6d81609-bb8a-42be-a59f-a762373604d7/snyk-wizard-falcor-preview-opt.png" width="500" height="111" alt="Snyk Wizard Upgrade Falcor Prompt" /></a><figcaption>Snyk Wizard Upgrade Falcor Prompt.</figcaption></figure>

The info link, which brings you to a [test page on the direct dependency](https://snyk.io/package/npm/falcor-router-demo/1.0.3), further shows two different vulnerabilities in `qs` and one in `semver`.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b4ed933-fa70-4052-8c35-5c7c7d92aa0b/snyk-web-falcor-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b4ed933-fa70-4052-8c35-5c7c7d92aa0b/snyk-web-falcor-preview-opt.png" width="500" height="264" alt="Snyk Web Test Report on Falcor" /></a><figcaption>Snyk Web Test Report on Falcor.</figcaption></figure>

Unfortunately, you can’t upgrade a deep dependency, both for technical reasons and for fear of breaking functionality. Your remediation step therefore is to upgrade the direct dependency, triggering the deep dependency upgrade. In this case, upgrading `falcor-router-demo` to version 1.0.5 (a ‘fix’ upgrade) will trigger the `qs` and `semver` upgrades you need to fix the vulnerabilities.

{{% ad-panel-leaderboard %}}

## Patch And Protect

The next issue the wizard reports on our demo app is different.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93ad6b3b-52fc-42f2-8f58-3f940e7e838e/snyk-wizard-handlebars-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93ad6b3b-52fc-42f2-8f58-3f940e7e838e/snyk-wizard-handlebars-preview-opt.png" width="500" height="106" alt="Snyk Wizard Patch Handlebars" /></a><figcaption>Snyk Wizard Patch Handlebars.</figcaption></figure>

Snyk found a vulnerability in handlebars, pulled in via the direct dependency `snyk-demo-child`. Although the vulnerability [was fixed](https://snyk.io/vuln/npm:handlebars:20151207) in Handlebars 4.0.0, `snyk-demo-child` has not upgraded to that version &mdash; so you can’t upgrade the vulnerability away.

This scenario is especially common in recently disclosed vulnerabilities, as it takes a while for the dependency chain to catch up. In addition, sometimes an upgrade *is* available, but it’s a major upgrade with breaking changes, and you can’t handle it right now. In cases when you have no upgrade option, instead of simply remaining vulnerable, Snyk suggests you **patch** the vulnerability.

Patching means changing the locally installed package files to fix the vulnerability. The patches are created and maintained by Snyk, and typically start with the code changes the package owner made to fix the issue, having removed any cosmetic or unrelated changes. The Snyk security team then verifies them, back&ndash;ports them to older versions, and tests they’ve not broken functionality. The patches are a part of Snyk’s [open source vulnerability database](https://github.com/Snyk/vulndb/), and here’s an example of patch for the [`ms` ReDoS vulnerability](https://github.com/Snyk/vulndb/tree/master/data/npm/ms/20151024).

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c3b7327-ff9d-4d06-ac50-09b6d982f567/snyk-patch-sample-ms-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c3b7327-ff9d-4d06-ac50-09b6d982f567/snyk-patch-sample-ms-preview-opt.png" width="500" height="176" alt="Snyk Sample Patch on ms package" /></a><figcaption>Snyk Sample Patch on ms package.</figcaption></figure>

After we patch Handlebars, the wizard prompts about two instances of uglify&ndash;js vulnerabilities, suggesting you patch them all.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/158d4d1f-4ce5-4314-9803-1149d7e8c556/snyk-wizard-uglify-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/158d4d1f-4ce5-4314-9803-1149d7e8c556/snyk-wizard-uglify-preview-opt.png" width="500" height="112" alt="Snyk Wizard Patch Uglify" /></a><figcaption>Snyk Wizard Patch Uglify.</figcaption></figure>

As projects expand, it’s common to find the same package repeated in the dependency tree, and it’s not that rare for one package to have multiple vulnerabilities. When the wizard sees multiple instances of a vulnerable package, it offers a shortcut to patch them all to save time. You can still choose to review and patch each issue separately, and if an instance was sufficiently upgraded by previously chosen upgrades it won’t be touched.

Note the wizard only patches the *locally installed* files. This means you need to reapply this patch every time dependencies are reinstalled, which you can do by running [`snyk protect`](https://snyk.io/docs/#protect). The wizard stores the patches you chose in the Snyk policy (*.snyk*), and [`snyk protect`](https://snyk.io/docs/#protect) will apply those patches, and those patches alone &mdash; it never unilaterally applies a patch. Each time you reinstall your dependencies, you should run [`snyk protect`](https://snyk.io/docs/#protect) to close the vulnerabilities. The wizard can do this for you, as we’ll see later on.

## Ignore

The next issue the wizard shows is not as easily solved.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e435309d-783b-4a15-b52b-b55347bace83/snyk-wizard-validator-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e435309d-783b-4a15-b52b-b55347bace83/snyk-wizard-validator-preview-opt.png" width="500" height="60" alt="Snyk Wizard Validator Vulnerability" /></a><figcaption>Snyk Wizard Validator Vulnerability.</figcaption></figure>

A vulnerability is found in a deep `validator` dependency, which has neither an upgrade nor a patch available. There are many combinations of vulnerability and module versions, and not all of them can be patched. Snyk’s security team is constantly adding more patches to the [open source VulnDB](https://github.com/Snyk/vulndb) and would [welcome pull requests](https://github.com/Snyk/vulndb/blob/master/CONTRIBUTING.md), but some issues still have no patch.

There’s no easy fix for these issues. You’ll need to better understand the risk this issue presents to your system, and weigh this risk against the effort of fixing the issue &mdash; for instance, by removing the dependency. While you consider your actions, you can ‘snooze’ the issue with Snyk, telling it to ignore the issue for 30 days. Snyk will prompt you to provide a reason for ignoring, to help you remember why you did it later on.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/196c43c3-f32b-4ecc-ad24-9c9d29d13f4a/snyk-wizard-validator-ignore-reason-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/196c43c3-f32b-4ecc-ad24-9c9d29d13f4a/snyk-wizard-validator-ignore-reason-preview-opt.png" width="500" height="99" alt="Snyk Wizard Validator Ignore Reason" /></a><figcaption>Snyk Wizard Validator Ignore Reason.</figcaption></figure>

If you assess the vulnerability and decide it’s not an issue (for instance, because a component is not really deployed to production), you can manually edit the Snyk policy (*.snyk*) file to use a far&ndash;future expiry date for this instance. Note that Snyk does not test devDependencies by default, avoiding most such red herrings.

In addition to any action you take, Snyk will let you know when a patch or upgrade become available for this scenario, so you can apply a better solution.

## Applying Your Choices

That’s it, we’ve tackled all the issues &mdash; hurray!

Before the wizard applies the requested changes, it suggests adding two steps to your *Package.json* workflow to keep you vulnerability free.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df801f8c-9989-41da-8cb0-68f79677af82/snyk-wizard-q-add-test-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df801f8c-9989-41da-8cb0-68f79677af82/snyk-wizard-q-add-test-preview-opt.png" width="500" height="14" alt="Snyk Wizard Add Snyk to Test Prompt" /></a><figcaption>Snyk Wizard Add Snyk to Test Prompt.</figcaption></figure>

First, the wizard suggests adding Snyk’s test to your regular `npm test` action. If a vulnerable package was added, the test would fail, keeping you safe. The wizard will also add `snyk` as devDependency, as you’ll need it in your test or CI environment. You can use the same logic to run this test in any favourite CI/test platform.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6f987b3-32ef-4424-94a5-eb0a9a8405cb/snyk-wizard-q-add-postinstall-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6f987b3-32ef-4424-94a5-eb0a9a8405cb/snyk-wizard-q-add-postinstall-opt.png" width="800" height="37" alt="Snyk Wizard Add Snyk to PostInstall Prompt" /></a><figcaption>Snyk Wizard Add Snyk to PostInstall Prompt. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6f987b3-32ef-4424-94a5-eb0a9a8405cb/snyk-wizard-q-add-postinstall-opt.png">Large preview</a>)</figcaption></figure>

If you’ve chosen to patch an issue, the wizard will also suggest adding [`snyk protect`](https://snyk.io/docs/#protect) to the `postinstall` step. The `postinstall` hook runs every time you install this package’s dependencies, ensuring those dependencies are always properly patched. Note that such a hook requires adding `snyk` as a dependency (not devDependency).

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c10af810-2540-4452-ab4f-ad8fe8daa22c/snyk-wizard-finalize-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c10af810-2540-4452-ab4f-ad8fe8daa22c/snyk-wizard-finalize-preview-opt.png" width="500" height="125" alt="Snyk Wizard applies changes" /></a><figcaption>Snyk Wizard applies changes.</figcaption></figure>

With all the questions answered, the wizard proceeds to apply the changes. It modifies the *Package.json* file with any upgrade requests or hooks, runs `npm update` to apply the changes, and stores the Snyk policy in the *.snyk* file (you can pretty&ndash;print it by running `snyk policy`). Make sure to add this *.snyk* file to your source control for patch and ignore instructions to apply.

Lastly, the wizard takes a snapshot of your dependencies, so it can monitor them over time.

{{% ad-panel-leaderboard %}}

## Monitor

Now that you’re free of known vulnerabilities, there are two ways that can change. The first is adding vulnerable packages to your code, which we handle by adding [`snyk test`](https://snyk.io/docs/#test) to your test/CI system. The second is through newly disclosed vulnerabilities. These are new disclosures of vulnerabilities in old code &mdash; the code you’re running in production!

This is addressed by Snyk’s last step &mdash; monitor. The snapshot the wizard takes is saved on Snyk’s servers, remembering the dependencies used on this application. If a new disclosed vulnerability affects your application, you’ll get an email alerting you to it. You can then run the wizard again to upgrade or patch as needed, and deploy the secure code.

Below is an example of an email you may get. As we mentioned above, you’ll also be notified about new remediation options; for instance, a patch or upgrade path that didn’t exist before.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4007fd8a-1d92-4546-85bf-49a0d7d766a3/snyk-new-vuln-email-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4007fd8a-1d92-4546-85bf-49a0d7d766a3/snyk-new-vuln-email-preview-opt.png" width="500" height="293" alt="Snyk Sample New Vulnerability Notification" /></a><figcaption>Snyk Sample New Vulnerability Notification.</figcaption></figure>

To keep Snyk’s understanding of your application up to date, you can run [`snyk monitor`](https://snyk.io/docs/#monitor) at the end of your deployment process. Doing so will take a fresh snapshot of your application, just like the wizard does, and will ensure Snyk’s alerts apply to your most recent code.

## Summary

Open Source packages are awesome, but they carry with them a substantial security risk. A good way to start acknowledging and handling this risk is to address the known vulnerabilities in your dependencies, as those are the ones attackers are most likely to exploit.

Snyk makes it easy for you to find, fix and monitor for known vulnerabilities in Node.js. I recommend you:

*   Run [`snyk wizard`](https://snyk.io/docs/#wizard) on your application and fix current issues. Upgrade when possible, patch when you can’t upgrade, and manually assess the rest of the issues.
*   Add [`snyk test`](https://snyk.io/docs/#test) to your tests and CI, to avoid adding vulnerable packages.
*   If you’ve patched issues, run [`snyk protect`](https://snyk.io/docs/#protect) whenever you reinstall your dependencies; for instance, by adding it to your `postinstall` script.
*   Add [`snyk monitor`](https://snyk.io/docs/#monitor) to your deployment process, to ensure you’re monitoring for vulnerabilities in the most up&ndash;to&ndash;date dependencies.
*   Stay alert for email notifications from Snyk about new vulnerabilities, and act quickly when they arrive.

If you own a public GitHub project, [add a badge](https://snyk.io/docs/#badge) to show you’re vulnerability free, and remind your users security matters.

<figure><a href="https://snyk.io/test/npm/name/badge.svg?src=SmashingMag"><img src="https://snyk.io/test/npm/name/badge.svg?src=SmashingMag" width="110" height="20"  alt="Vulnerabilities Badge" /></a>
<figcaption>Sample Snyk badge with no vulnerabilities.</figcaption></figure>

If you’re not using Node.js, [register](https://snyk.io/auth/github) to get notified when we add new languages, or [let us know](mailto:contact@snyk.io) which platforms you’d like us to support next!

### Further Reading on Smashing Magazine:

*   “[I Contributed To An Open-Source Editor, And So Can You](https://www.smashingmagazine.com/2016/08/contributing-open-source/),” Christian Heilmann
*   “[A Short Guide To Open-Source And Similar Licenses](https://www.smashingmagazine.com/2010/03/a-short-guide-to-open-source-and-similar-licenses/),” Cameron Chapman
*   “[So You’ve Decided To Open-Source A Project At Work. What Now?](https://www.smashingmagazine.com/2013/12/open-sourcing-projects-guide-getting-started/),” Nicholas C. Zakas
*   “[Front-End Performance Checklist 2017](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/),” Vitaly Friedman

{{< signature "og, nl" >}}