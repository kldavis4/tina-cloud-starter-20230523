---
title: 'Building Your Security Strategy (Case Study)'
slug: ten-principles-consider-building-security-strategy-case-study
author: wix-security-team
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1504d71c-665f-4bef-81ff-f09c25cc55eb/building-your-security-strategy.jpg
date: 2022-09-29T12:00:00.000Z
summary: >-
  In this article, Wix security experts share ten “security by design” principles that emerged from their work in keeping the Wix platform secure. If you’re a developer, these tried-and-true principles can help you build your own secure applications.
description: >-
  In this article, Wix security experts share ten “security by design” principles that emerged from their work in keeping the Wix platform secure. If you’re a developer, these tried-and-true principles can help you build your own secure applications.
categories:
  - Tools
  - Security
  - Case Studies
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Wix
  link: https://www.wix.com/?utm_source=affiliate&utm_campaign=bd_smashingmag&experiment_id=0001
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d3a5c92-5ce3-4031-9fd2-e4ecf5b3c238/wix-svg.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.wix.com/?utm_source=affiliate&utm_campaign=bd_smashingmag&experiment_id=0001" style="text-shadow: none;">Wix</a> who are known to give you the freedom to create, design, manage and develop your web presence exactly the way you want. <em>Thank you!</em>
---

What should you focus on when designing your [security strategy](https://www.wix.com/website-security?utm_source=affiliate&utm_campaign=bd_smashingmag&experiment_id=0001)? This question becomes more and more tricky as your organization grows and matures. At an initial stage, you might be able to make due with a periodic penetration test. But you will soon find that as you scale up to hundreds and thousands of services, some of the procedures have to change. The focus shifts from project-based assessments to building and maintaining a lasting mindset and framework with security at the core, so you can minimize risk across your environment.

In this article, we’ll share some guiding principles and ideas for incorporating security by design into your own development process, taken from our work at Wix serving 220M+ users.

## First And Foremost: Security By Design

Also known as security by default, **security by design** (SbD) is a concept in which we aim to “limit the opportunities” for making security-related mistakes. Consider a case where a developer builds a service to query a database. If the developer is required (or allowed) to build queries “from scratch” writing SQL directly into his code, they can very well end up introducing **SQL Injections** (SQLI) vulnerabilities. However, with a security by default approach, the developer can get a safe **Object-Relational Mapping** (ORM), letting the code focus on logic where the DB interactions are left for the ORM libraries. By ensuring the ORM library is safe once, we are able to block SQLI everywhere (or at least everywhere the library is used). This approach might restrict some developer liberties, but except for specific cases, the security benefits tend to outweigh the cons.

That previous example is rather well known, and if you use a mature application development framework, you’re probably using an ORM anyway. But the same logic can be applied to other types of vulnerabilities and issues. Input validation? Do this by default using your app framework, according to the declared var type. What about **Cross-Site Resource Forgery** ([CSRF](https://portswigger.net/web-security/csrf))? Solve it for everyone in your API gateway server. Authorization confusion? Create a central identity resolution logic to be consumed by all other services.

By following this methodology, we’re able to allow our developers the freedom to move quickly and efficiently, without needing to introduce security as a “blocker” in later stages before new features go live.  

### 1. Establish Secure Defaults For Your Services 

Take the time to ensure that your services are served by default with secure settings. For example, users should not need to actively choose to make their data private. Instead, the default should be “private” and users can have the option to make it public if they choose to. This of course depends on product decisions as well, but the concept stands. Let’s look at an example. When you build a site on our platform, you can easily set up a content “Collection”, which is like a simplified database. By default, editing permissions to this collection are restricted to admin users only, and the user has the option to expose it to other user types using the Roles & Permissions feature. The default is secure.

### 2. Apply The Principle Of Least Privilege (PoLP)

Put simply, users shouldn’t have permission for stuff they don’t need. A permission granted is a permission used, or if not needed, then abused. Let’s look at a simple example: When using Wix, which is a secure system with support for multiple users, a website owner can use Roles & Permissions to add a contributor, say with a Blog Writer role, to their site. As derived from the name, you would expect this user to have permissions to write blogs. However, would this new contributor have permissions, for example, to edit payments? When you put it like this, it sounds almost ridiculous. But the “least permission” concept (PoLP) is often misunderstood. You need to apply it not only to users, but also to employees, and even to systems. This way even if you _are_ vulnerable to something like CSRF and your employees are exploited, the damage is still limited.

In a rich microservice environment, thinking about least permission might become challenging. Which permission should Microservice A have? Should it be allowed to access Microservice B? The most straightforward way to tackle this question is simply starting with zero permissions. A newly launched service should have access to nothing. The developer, then, would have an easy, simple way to extend their service permission, according to need. For example, a “self service” solution for allowing developers to grant permissions for services to access non-sensitive databases makes sense. In such an environment, you can also look at sensitive permissions (say for a database holding PII data), and require a further control for granting permissions to them (for example, an OK from the data owner).

### 3. Embrace The Principle Of Defense In Depth (DiD)

As beautifully put by a colleague, security is like an onion &mdash; it’s made of many layers built on top of layers, and it can make you cry. In other words, when building a secure system, you need to account for different types of risk and threats, and subsequently you need to build different types of protections on top of others. 

Again, let’s look at a simple example of a login system. The first security gateway you can think of in this context is the “user-password” combination. But as we all know, passwords can leak, so one should always add a second layer of defense: **two-factor authentication** (2FA), also known as **multi-factor authentication** (MFA). Wix encourages users to enable this feature for their account security. And by now, MFA is pretty standard &mdash; but is it enough? Can we assume that someone who successfully logged into the system is now trusted? 

Unfortunately, not always. We looked until now at one type of attack (password stealing), and we provided another layer to protect against it, but there are certainly other attacks. For example, if we don’t protect ourselves, a **Cross Site Scripting** (XSS) attack can be used to hijack a user’s sessions (for example by stealing the cookies), which is as good as a login bypass. So we need to consider added layers of defense: cookie flags to prevent JS access (HTTP only), session timeouts, binding a session to a device, etc. And of course, we need to make sure we don’t expose XSS issues.

You can look at this concept in another way. When writing a feature, you should almost protect it “from scratch”, thinking all defenses might have been broken. That doesnt mean writing every line of code again, it just means being aware that certain assumptions cannot be made. For example, you can’t assume that just because your service does not have an externally reachable endpoint, it has never been accessed by malicious entities. An attacker exploiting **Server-Side Request Forgery** (SSRF) issues can hit your endpoint any minute. Is it protected against such issues? 

At Wix, we assume a “breach mindset” at all times, meaning each developer assumes the controls leading up to the application they’re working on have already been breached. That means checking permissions, input validations and even logic &mdash; we never assume previous services are sensible.

### 4. Minimize Attack Surface Area

What’s the safest way to secure a server? Disconnect it from the electricity socket. Jokes aside, while we don’t want to turn our services off just to ensure they’re not abused, we certainly don’t want to leave them on if they serve no real function. If something is not needed or being used, it should not be online. 

The most straightforward way to understand this concept is by looking at non-production environments (QA, staging, etc). While such environments are often needed internally during the development process, they have no business being exposed such that external users can access them. Being publicly available means they can serve as a target for an attack, as they are not “production ready” services (after all, they are in the testing phase). The probability for them to become vulnerable increases. 

But this concept doesn’t apply only to whole environments. If your code contains unused or unnecessary methods, remove them before pushing to production. Otherwise, they become pains instead of assets.

### 5. Fail Securely

If something fails, it should do so securely. If that’s confusing, you’re not alone. Many developers overlook this principle or misunderstand it. Imagining every possible edge case on which your logic can fail is almost impossible, but it is something you need to plan for, and more often than not it’s another question of adopting the right mindset. If you assume there _will_ be failures, then you’re more likely to include all possibilities.

For instance, a security check should have two possible outcomes: allow or deny. The credentials inputted are either correct, or they’re not. But what if the check fails entirely, say, because of an unexpected outage of electricity in the database server? Your code keeps running, but you get a “DB not found” error. Did you consider that? 

In this particular instance, the answer is probably “yes”, you thought of it, either because your framework forced you to consider it (such as Java’s “checked exceptions”) or simply because it actually happens often enough that your code failed in the past. But what if it is something more subtle? What if, for example, your SQL query fails due to non-unicode characters that suddenly appeared as input? What if your S3 bucket suddenly had its permissions changed and now you can’t read from it anymore? What if the DNS server you’re using is down and suddenly instead of an NPM repo you’re hitting a compromised host? 

These examples might seem ludacris to you, and it would be even more ludacris to expect you to write code to handle them. What you should do, however, is expect things to behave in an expected manner, and make sure if such things occur, you “fail securely”, like by just returning an error and stopping the execution flow. 

It would make no sense to continue the login flow if the DB server is down, and it will make no sense to continue the media processing if you can’t store that image on that bucket. Break the flow, log the error, alert to the relevant channel &mdash; but don’t drop your security controls in the process. 

### 6. Manage Your Third-Party Risk

Most modern applications use third-party services and/or import third-party code to enhance their offering. But how can we ensure secure integrations with third parties? We think about this principle a lot at Wix, as we offer third-party integrations to our user sites in many ways. For example, users can install apps from our App Market or add third-party software to their websites using our full-stack development platform called [Velo](https://www.wix.com/velo?utm_source=affiliate&utm_campaign=bd_smashingmag&experiment_id=0001).

Third-party code can be infiltrated, just like your own, but has the added complication that you have no control over it. MPM node libraries, for instance, are some of the most used in the world. But recently a few well-known cases involved them being compromised, leaving every site that used them exposed.

The most important thing is to be aware that this might happen. Keep track of all your open-source code in a **software bill of materials** (SBOM), and create processes for regularly reviewing it. If you can, run regular checks of all your third-party suppliers’ security practices. For example, at Wix we run a strict **Third-Party Risk Management Program** (TPRM) to vet third parties and assess security while working with them.

### 7. Remember Separation Of Duties (SoD)

Separation of duties really boils down to making sure tasks are split into (and limited to) appropriate user types, though this principle could also apply to subsystems.

The administrator of an eCommerce site, for example, should not be able to make purchases. And a user of the same site should not be promoted to administrator, as this might allow them to alter orders or give themselves free products.

The thinking behind this principle is simply that if one person is compromised or acting fraudulently, their actions shouldn’t compromise the whole environment.

### 8. Avoid Security By Obscurity

If you write a backdoor, it will be found. If you hard-code secrets in your code, they will be exposed. It’s not a question of “if”, but “when” &mdash; there is no way to keep things hidden forever. Hackers spend time and effort on building reconnaissance tools to target exactly these types of vulnerabilities (many such tools can be found with a quick Google search), and more often than not when you point at a target, you get a result. 

The bottom line is simple: you cannot rely on hidden features to remain hidden. Instead,  there should be enough security controls in place to keep your application safe when these features are found. 

For example, it is common to generate access links based on randomly generated UUIDs. Consider a scenario where an anonymous user makes a purchase on your store, and you want to serve the invoice online. You cannot protect the invoice with permissions, as the user is anonymous, but it is sensitive data. So you would generate a “secret” UUID, build it into the link, and treat the “knowledge” of the link as “proof” of identity ownership.  

But how long can this assumption remain true? Over time, such links (with UUID in them) might get indexed by search engines. They might end up on the Wayback Machine. They might be collected by a third-party service running on the end user’s browser (say a BI extension of some sort), then collected into some online DB, and one day accessed by a third party. 

Adding a short time limit to such links (based on UUIDs) is a good compromise. We don’t rely on the link staying secret for long (so there’s no security by obscurity), just for a few hours. When the link gets discovered, it’s already no longer valid. 

### 9. Keep Security Simple

Also known as KISS, or _keep it simple, stupid_. As developers, we need to keep users in mind at all times. If a service is too complicated to use, then its users might not know how to use it, and bypass it or use it incorrectly. 

Take 2FA for example. We all know it’s more secure, but the process also involves a degree of manual setup. Making it as simple as possible to follow means more users will follow it, and not compromise their own accounts with weaker protections.

Adding new security functionality always makes a system more complex, so it can have an unintended negative impact on security. So keep it simple. Always weigh the value of new functionality against its complexity, and keep security architecture as simple as possible.

### 10. Fix Security Issues, Then Check Your Work

Thoroughly fixing security issues is important for all aspects of a business. At Wix, for example, we partner with ethical hackers through our [Bug Bounty Program](https://www.hackerone.com/customer-stories/how-wix-improves-their-security-posture-ethical-hackers) to help us find issues and vulnerabilities in our system, and practice fixing them. We also employ internal security and penetration testing, and the security team is constantly reviewing the production services, looking for potential bugs.

But fixing a bug is just the start. You also need to understand the vulnerability thoroughly before you fix it, and often get whoever spotted it to check your fix too. And then, when a bug is fixed, carry out regression tests to make sure it’s not reintroduced by code rollbacks. This process is crucial to make sure you’re actually advancing your application security posture.

## Conclusion

By implementing security by design at Wix, we were able to build a robust and secure platform &mdash; and we hope that sharing our approach will help you do the same. We applied these principles not just to security features, but to all components of our system. We recommend considering this, whether you build from scratch or choose to rely on a secure platform like ours.

More importantly, following security by design instilled a security mindset into our company as a whole, from developers to marketing and sales. Cybersecurity should be top priority in everyone’s minds, as attacks increase and hackers find new ways of accessing sensitive information. 

Taking a defensive position right from the start will put you at an advantage. Because when thinking about cybersecurity, it’s not *if* a breach happens. It’s when.

* For more information on security by design, visit the [Open Web Application Security Project](https://owasp.org/). This non-profit community is dedicated to securing the web, and produces a range of free open-source tools, training and other resources to help improve software security. 
* To learn more about secure practices at Wix, check out [wix.com/trust-center/security](https://www.wix.com/trust-center/security?utm_source=affiliate&utm_campaign=bd_smashingmag&experiment_id=0001).

{{< signature "vf, il" >}}
