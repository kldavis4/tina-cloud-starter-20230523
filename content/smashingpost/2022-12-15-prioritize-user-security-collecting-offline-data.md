---
title: 'How To Prioritize User Security When Collecting Offline Data'
slug: prioritize-user-security-collecting-offline-data
author: suzanne-scacca
image: >-
  https://res.cloudinary.com/indysigner/image/upload/v1670867131/prioritize-user-security-collecting-offline-data_nozcsc.jpg
date: 2022-12-15T13:30:00.000Z
summary: >-
  Concerns over online privacy and security are nothing new. The best thing companies can do to put users’ minds at ease is to utilize technology that makes the digital exchange of data more secure. That goes just as much for the tools that users directly enter their data into as the tools that businesses use to move that data around behind the scenes. In this article, Suzanne Scacca explores how the right CSV importer can help businesses better prioritize user security.
description: >-
  Concerns over online privacy and security are nothing new. In this article, Suzanne Scacca explores how the right CSV importer can help businesses better prioritize user security.
categories:
  - Security
  - Privacy
  - Ethics
  - Design
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Flatfile
  link: https://flatfile.com/?utm_source=partner&utm_medium=content&utm_campaign=smashing-magazine-sponsorship-content_q4-2022-flatfile-promotion-december&utm_content=demo&utm_term=flatfile_status_tofu_dec
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67708e55-ec01-4e9a-bc01-c106ea94dfed/flatfile-full-logo-300x300.png
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.flatfile.io/product/concierge/?utm_source=partner&utm_medium=content&utm_campaign=smashing-magazine-content_q4-2020-portal-data-onboarding-post&utm_content=external-article-link&utm_term=non-technical-overview">Flatfile</a> who create beautiful, human-centric experiences to remove the barriers between people and data. <em>Thank you!</em>
---

With the explosive growth of cloud computing over the last decade, unprecedented volumes of data &mdash; customer data, product data, statistics, financials, and so on &mdash; are being shared between organizations every day. While it would be great if there were a universal API that could guarantee secure and accurate transfer of data, the reality is much more primitive.

Most data that is being shared between companies these days is contained in CSV (comma-separated values) files. **While CSVs are generally easy to create, they’re notoriously difficult to secure.** 

Because of this, the exchange of CSV files has the potential to cause serious problems for companies. And when it comes to user security and privacy, companies can’t afford to gamble on such liability.

## How To Create A Secure Data Importer For Your Clients

[TechRepublic](https://www.techrepublic.com/article/data-privacy-is-a-growing-concern-for-more-consumers/) recently published the findings from a KPMG report regarding data privacy. 64% of respondents said that they don’t believe that companies do much in the way of securing and protecting the data that’s been shared with them. 

We know what the solution to this is and how to reduce those justifiable concerns. The first piece is to **handle customer data responsibly and be transparent about what you’re doing with it**. Regulations like GDPR and HIPAA provide the framework for this.

The other solution is to **use technology that prioritizes user security**. Just as you’d only add secure data handling features to your digital product &mdash; like contact forms, payment processors, and so on &mdash; the same applies to your data importer. 

CSV importers are already a step in the right direction when it comes to security. Rather than sending email files back and forth over insecure email platforms, companies pass their data through CSV importers. The trick is to build or use a data importer that prioritizes security. 

Next, you can find some things your importer will need in order for that to be true.

### Protect Your Data With A Secure Infrastructure

When you build a website or app, there are certain measures you take to secure it. One of the most important measures is choosing a hosting provider with the proper infrastructure to support, stabilize and secure your digital product and the data that moves through it. 

If you’re building your own data importer, then your product hosting will serve as the underlying infrastructure for it. Just make sure that it is capable of protecting the integrity of your product as well as securing the data transmissions that take place through your importer.

If you’re going to use a pre-built data importer solution, then spend some time reviewing the technology and systems that power it. Your users &mdash; and *their* customers &mdash; won’t be too happy if a data breach occurs and you try to put the blame on an external solution.

Here are some things that a secure data importer needs in terms of infrastructure:

#### Built In The Cloud

Cloud hosting offers a high degree of protection. When reviewing data importer options, take a look under the hood of each to confirm that they’re running in the cloud. 

For instance, Flatfile’s servers are built on Amazon Web Services (AWS) cloud infrastructure. As a result, data that passes through Flatfile’s systems is fully encrypted using the AES-256 block cipher. This encryption protects data while it passes through the data importer as well as once it’s stored. 

#### Security Testing And Monitoring

You and your clients aren’t the only ones who should be keeping an eye on what’s going on with your data importer. The company that devised the solution should be doing so, too.

There are a number of ways to ensure that the data importer and its infrastructure haven’t been compromised:

- Application monitoring;
- Continuous logging;
- User action tracing;
- Penetration testing;
- Malicious activity monitoring;
- Automated blocking.

It’s also important to find a data importer solution and provider that will be transparent about detected issues and alert you to any they’ve found.

#### Resource Management

Application performance goes hand-in-hand with security. This is critical for companies like [EmployUS](https://flatfile.com/customer-stories/employus/?utm_source=partner&utm_medium=content&utm_campaign=smashing-magazine-sponsorship-content_q4-2022-flatfile-promotion-december&utm_content=conetnt&utm_term=employus_customer_story_tofu_dec) who promise users that their data will be secured, compliant *and* available.

In addition to reviewing your data importer solution for security features, also look for what it’s doing to optimize performance and uptime. 

Load balancing and resource scaling are two things to look for. Another thing you should do is check out the company’s “Status” page. Here’s an example of what the “Status” page looks like for Flatfile:

{{< rimg href="https://res.cloudinary.com/indysigner/image/upload/v1670859717/flatfile-status-updates_zxgafs.png" src="https://res.cloudinary.com/indysigner/image/upload/v1670859717/flatfile-status-updates_zxgafs.png" width="800" height="389" sizes="100vw" caption="A screenshot of the Flatfile “Status” page shows that all systems are operational. (Source: <a href='https://flatfile.com/?utm_source=partner&utm_medium=content&utm_campaign=smashing-magazine-sponsorship-content_q4-2022-flatfile-promotion-december&utm_content=demo&utm_term=flatfile_status_tofu_dec'>Flatfile</a>) (<a href='https://res.cloudinary.com/indysigner/image/upload/v1670859717/flatfile-status-updates_zxgafs.png'>Large preview</a>)" alt="Flatfile users can visit the ‘Status’ page to check on systems operational issues. This screenshot shows that all systems are operational" >}}

If there are issues with any aspect of the data importer technology, you’ll find proof of it on this page. Users can also subscribe for real-time updates. Having this level of visibility and transparency is essential when you outsource a critical piece of your application to another provider’s solution.

### Ensure Regulatory And Legal Compliance

Different types of digital products have to maintain certain levels of compliance. This can be due to the types of data they handle (like in the medical and financial industries) or because of where they or their users are located in the world. 

Whether you’re building your own importer or using a pre-built solution, your technology and data handling processes need to be compliant with all relevant security and privacy regulations. 

For example, Flatfile’s solution maintains compliance with the following:

- **GDPR**    
Although this data security and privacy regulation was passed to protect EU citizens’ personal data, it has far-reaching effects. Because many businesses these days serve customers all around the world, GDPR compliance is essential for anyone doing business online.
- **AICPA SOC 2 (Types I and II)**  
The Association of International Certified Professional Accountants has its own regulations related to data privacy and protection. SOC and SOC 2 refer to the audit that service providers must pass in order to ensure they’re securely handling employee and customer data.
- **EU/U.S. Privacy Shield**  
The U.S. Department of Commerce put together this framework in conjunction with the European Commission and the Swiss Administration. It provides companies that conduct transatlantic commerce with a set of data protection requirements to follow when transferring data. 
- **HIPAA**  
HIPAA is a U.S. law concerned with the protection of sensitive patient data. It ensures that their health information is private and secure. It also gives patients more control over how their information is used and to whom it is disclosed. 

{{< rimg href="https://res.cloudinary.com/indysigner/image/upload/v1670859926/flatfile-security-trust-seals_mhy2hm.png" src="https://res.cloudinary.com/indysigner/image/upload/v1670859926/flatfile-security-trust-seals_mhy2hm.png" width="800" height="139" sizes="100vw" caption="Flatfile is SOC 2 Type I, SOC 2 Type II, HIPAA, Privacy Shield and GDPR compliant. (Source: <a href='https://flatfile.com/?utm_source=partner&utm_medium=content&utm_campaign=smashing-magazine-sponsorship-content_q4-2022-flatfile-promotion-december&utm_content=demo&utm_term=flatfile_status_tofu_dec'>Flatfile</a>) (<a href='https://res.cloudinary.com/indysigner/image/upload/v1670859926/flatfile-security-trust-seals_mhy2hm.png'>Large preview</a>)" alt="A row of 5 security seals appears on the Flatfile website. They represent the five types of compliance the data importer meets: GDPR, AICPA SOC, AICPA SOC2, EU/U.S. Privacy Shield, and HIPAA" >}}

With so many regulations to stay on top of, a data importer can become a huge chore to maintain and update. This is why many developers and companies choose to use a pre-built data importer solution. 

[Osmind](https://flatfile.com/customer-stories/osmind/?utm_source=partner&utm_medium=content&utm_campaign=smashing-magazine-sponsorship-content_q4-2022-flatfile-promotion-december&utm_content=content&utm_term=osmind_customer_story_tofu_dec), for instance, not only streamlined its data transfer process with Flatfile Workspaces, but it enabled them to achieve HIPAA compliance &mdash; something that’s critical when working with sensitive health records.

**Bottom line**: By finding a data importer that maintains various regulatory compliances, you won’t have to spend time down the road looking for alternative solutions to fill in the missing gaps. Plus, a provider that keeps its systems updated as regulations and standards change will greatly reduce the risk of your data importer falling out of compliance. 

### Prevent Your Importer From Breaking So Easily

Whether you are populating databases for a warehouse catalog, an ERP, or just a list of every town in which you operate, your importer needs to be strong. 

For instance, let’s say a user ignores your file preparation instructions and rushes to import the files they have. Before it even gets to the point of cleaning up the data, you want to make sure the importer is able to *process* it without breaking down.

A broken data importer can leave users with a bad impression of the product they’re using and the company behind it. It doesn’t matter if it’s their fault for not reading the instructions or for poorly formatting their file. Encountering a broken feature is frustrating and can quickly lead to concerns with regard to security and privacy. 

<blockquote>“What happened?”<br />“Did my data even go through?”<br />“Should I try it again, or is it too risky?”</blockquote>

With how advanced technology has gotten today, users will likely wonder why *you* hadn’t anticipated these kinds of issues and sorted them out already. So, in order to prevent end users from encountering a broken data importer, it will need to be smart and flexible. 

{{< rimg href="https://res.cloudinary.com/indysigner/image/upload/v1670860785/flatfile-secure-data-onboarding-message_w31wzg.png" src="https://res.cloudinary.com/indysigner/image/upload/v1670860785/flatfile-secure-data-onboarding-message_w31wzg.png" width="800" height="394" sizes="100vw" caption="Even with scant details about file types or data formats, Flatfile will enable you to create error-free data upload experiences. (Source: <a href='https://flatfile.com/?utm_source=partner&utm_medium=content&utm_campaign=smashing-magazine-sponsorship-content_q4-2022-flatfile-promotion-december&utm_content=demo&utm_term=flatfile_status_tofu_dec'>Flatfile</a>) (<a href='https://res.cloudinary.com/indysigner/image/upload/v1670860785/flatfile-secure-data-onboarding-message_w31wzg.png'>Large preview</a>)" alt="A screenshot is taken from Developer Mode inside of Flatfile. We see a sample data importer asking users to ‘Upload your file’. They can drop their CSV or XLSX file into the center of the screen or select it. There’s also a message at the bottom that reads: ‘You’re securely onboarding data with Flatfile’" >}}

This means using a data importer that:

- Provides no more than a few guidelines so that users don’t have to read an entire manual in order to prepare their files;
- Moves massive amounts of files with thousands of rows of data without erroring out;
- Accepts files just as the customer has prepared them;
- Easily maps and validates data no matter how inconsistent or varied the formats are;
- Detects and notifies you (or your users) of serious errors before uploading.

An importer that breaks down all the time is going to cause issues for everyone involved. So too will one that brings tons of garbled data into your system &mdash; especially when that data is mission-critical. 

By creating or using a strong and agile data importer, you can reduce the frequency with which errors occur. This will make your data importer more reliable and valuable to your users and help them instill greater trust in their own customers. 

## Wrapping Up

User security &mdash; as well as the *perception* of how secure the products are that they use &mdash; should matter a good deal to companies who collect data from their customers. That’s why it’s essential for developers to use CSV importers that they trust and that won’t put their clients or their end users in harm’s way.

As for whether you should [build or buy a data importer](https://flatfile.com/build-vs-buy/?utm_source=partner&utm_medium=content&utm_campaign=smashing-magazine-sponsorship-content_q4-2022-flatfile-promotion-december&utm_content=content&utm_term=build_vs_buy_content_tofu_dec), that decision is yours to make. However, if security and compliance are top priorities, then purchasing a pre-built importer like Flatfile would be the more economical and practical choice.

{{< signature "yk, il" >}}
