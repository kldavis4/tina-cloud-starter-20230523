---
title: 'How GDPR Will Change The Way You Develop'
slug: gdpr-for-web-developers
author: heather-burns
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dcb43cf-e60e-434b-8f95-e6e5ca9df199/gdpr-illustration.png
date: 2018-02-27T12:45:02+01:00
summary: >-
  GDPR requires you to be more thoughtful about the sites and services you build, more transparent about the ways you collect and use data, more considerate of your users, and more thorough in your development and documentation processes.
description: >-
  GDPR requires you to be more thoughtful about the sites and services you build, more transparent about the ways you collect and use data, more considerate of your users, and more thorough in your development and documentation processes.
categories:
  - Privacy
  - Security
  - GDPR
  - Guides
---
Europe’s imminent privacy overhaul means that we all have to become more diligent about what data we collect, how we collect it, and what we do with it. In our turbulent times, these privacy obligations are about ethics as well as law.

Web developers have a major role to play here. After all, healthy data protection practice is as much about the development side &mdash; code, data, and security &mdash; as it is about the business side of process, information, and strategy.

In this article, we’ll explore what you, as a developer, need to know about the new data protection regime. At the end, you’ll understand how the challenges posed by the privacy overhaul will ultimately help to make you a better developer.

**Important Note**: *This article does not constitute legal advice.*

## All Change For Data Protection

In May of 2018, a major upgrade to Europe’s overarching data protection framework becomes enforceable. This will be followed by a companion piece of legislation pertaining to data in transit. The extraterritorial nature of these two frameworks &mdash; they protect the privacy rights of people in Europe regardless of where their data is collected &mdash; means that they will become the *de facto* standard for privacy around the world.

The European privacy overhaul will bring positive changes to our business processes and development workflows. We all have to become more thoughtful about what data we collect, how we collect it, and what we do with it. Those changes could not have come soon enough. With data breaches and privacy violations in the headlines every day, not to mention governments expressing open malice against vulnerable citizens, our privacy obligations are as much about ethics and humanity as they are about law and policy.

{{% feature-panel %}}

Web developers like you have a major role to play in embracing the new frameworks as the positive tools that they are. The good news is that the obligations in the updated frameworks are not overly complex or technical, and in fact, they don’t even require lawyers. These rules are common-sense and can be immediately adopted.

Let’s explore what you need to know about the new data protection frameworks, and how you will need to adapt your development workflows to meet them. This article is not a comprehensive overview of the European privacy overhaul by any means; rather, it focuses on issues specific to web development.

## The Changing Privacy Landscape

Europe’s data protection and privacy overhaul comes in two parts.

The first half is the General Data Protection Regulation (GDPR), which becomes enforceable across Europe on 25 May 2018. This is an overhaul, modernization, and replacement of the existing framework, the Data Protection Directive of 1995 (yes, 1995.)

All of the existing principles from the original Directive stay with us under GDPR. What GDPR adds is new definitions and requirements to reflect changes in technology which simply did not exist in the dialup era. It also tightens up requirements for transparency, disclosure, and process: lessons learned from 23 years of experience.

The second half is the revamp of the ePrivacy Directive of 2002. (You know it, somewhat inaccurately, as the “cookie law.”) This revamp, which deals with data in transit such as cookies, telemetry, metadata, and consent for marketing, was originally planned to go live on 25 May, twinned with GDPR. However, as of this writing, the ePD is still in draft negotiations. The latest Brussels gossip says it should be finalized in late autumn or early winter. Regardless of when it is finalized, its requirements for consent will reference GDPR’s standards.

Developers may find the delay to be a good thing; it gives you a chance to get the wide scope of GDPR right, which will make the narrow scope of the ePD relatively easy when the time comes.

## What Is Personal Data?

The European data protection frameworks pertain to *personal data*. This is defined as “any information relating to an identified or identifiable natural person.” This can be one piece of information or multiple data points combined to create a record.

Beyond personal data there is also *sensitive personal data*, defined as information about a person’s:

- Racial or ethnic origin
- Political opinions
- Religious or philosophical beliefs
- Trade union membership
- Health data
- Sex life or sexual orientation
- Past or spent criminal convictions

Sensitive personal data requires stricter protections than regular personal data, and the consequences for its leakage or misuse are greater.

GDPR expands the definition of personal data to include:

- Genetic data
- Biometric data (such as facial recognition or fingerprint logins)
- Location data
- Pseudonymized data
- Online identifiers

The latter definition is important for developers. It includes things like IP addresses, mobile device IDs, browser fingerprints, RFID tags, MAC addresses, cookies, telemetry, user account IDs, and any other form of system-generated data which identifies a natural person.

The European term “personal data” differs from the American term “personally identifiable information.” The latter pertains to a much more limited set of information than the European model. It also does not see information as contextual, whereas the European framework emphasizes the risks inherent in data aggregation.

Personal data is used by *data controllers* and *data processors*. The *data controller* is a person or an entity, such as you or your organization, which decides what data is collected, how it is used, and whom it is shared with. The *data processor* is any entity other than the data controller who processes the data on their behalf. As a developer, you may be a data controller, you may be a data processor, and you may be both.

## Who Is Impacted By The Privacy Overhaul?

European data protection rules are, and always have been, extraterritorial. They apply to all personal data collected, processed, and retained about persons within the European Union regardless of citizenship or nationality.

That simply means that if you do business in Europe, or collect data on European users, you must protect their data in full accordance with the regulation as if you yourself were in Europe. If you are not prepared to meet that legal requirement, you should not do business in Europe. (Indeed, any developer collecting European data who is surprised to hear this news should explain what they have been doing with that data since 1995.)

GDPR applies to all businesses, organizations, sectors, situations, and scenarios, regardless of a business’s size, head count, or financial turnover. A small app studio is every bit as beholden to these rules as a large corporation.

Europe’s data protection regime stands in stark contrast to that of the U.S., which has no single overarching, cross-sector, or cross-situational data protection law. What little privacy law there is in the U.S. tends to be applicable only within sectors or states. The American approach also tends to view privacy as a subset of contract or property law, not its own discipline. This cultural difference often sees American developers struggling with the concept of privacy as a fundamental human right enshrined in law, a situation which has no U.S. equivalent. That gap does, unfortunately, add a few more steps to the compliance journey for U.S. developers tasked with getting to grips with the European framework.

## How Does Your Development Workflow Need To Change?

Whatever programming language you work in, role you hold, or product you create, GDPR requires you to be more structured and transparent about how you do things. Yet far from being a burden, you will find these obligations common-sense and surprisingly welcome.

Let’s go over the ways that GDPR will impact your development workflow. We can divide this into two broad areas: how you *work* within your business, and how you *develop* with the code.

### How You Work

GDPR will impact *how you work* in terms of business processes and project planning. These changes are cross-disciplinary and should involve your development, UX, marketing, legal, and management teams.

### Privacy By Design

GDPR requires the adoption of the Privacy by Design framework, a seven-point development methodology which requires optimal data protection to be provided as standard, by default, across all uses and applications.

We’ve previously covered the "[Privacy By Design Framework](https://www.smashingmagazine.com/2017/07/privacy-by-design-framework/)" in depth in its own article. Read it and then come back.

### Privacy Impact Assessments

A Privacy Impact Assessment (PIA), which is required under GDPR for data-intensive projects, is a living document which must be made accessible to all involved with a project. It is the process by which you discuss, audit, inventory, and mitigate the privacy risks inherent in the data you collect and process.

Like all GDPR documentation, a PIA can be requisitioned by a data protection regulator in the event of a privacy concern or data breach. Not having a PIA is not an option.

A robust PIA should document the following information:

#### Data collection and retention

1. What personal data is processed?
2. How is that data collected and retained?
3. Is the data stored locally, on our servers, or both?
4. For how long is data stored, and when is the data deleted?
5. Is the data collection and processing specified, explicit, and legitimate?
6. What is the process for granting consent for the data processing, and is consent explicit and verifiable?
7. What is the basis of the consent for the data processing?
8. If not based on consent, what is the legal basis for the data processing?
9. Is the data minimized to what is explicitly required?
10. Is the data accurate and kept up to date?
11. How are users informed about the data processing?
12. What controls do users have over the data collection and retention?

#### Technical and security measures

1. Is the data encrypted?
2. Is the data anonymized or pseudonymized?
3. Is the data backed up?
4. What are the technical and security measures at the host location?

#### Personnel

1. Who has access to the data?
2. What data protection training have those individuals received?
3. What security measures do those individuals work with?
4. What data breach notification and alert procedures are in place?
5. What procedures are in place for government requests?

#### Subject access rights

1. How does the data subject exercise their access rights?
2. How does the data subject exercise their right to data portability?
3. How does the data subject exercise their rights to erasure and the right to be forgotten?
4. How does the data subject exercise their right to restrict and object?

#### Legal

1. Are the obligations of all data processors, including subcontractors, covered by a contract?
2. If the data is transferred outside the European Union, what are the protective measures and safeguards?

#### Risks

1. What are the risks to the data subjects if the data is misused, mis-accessed, or breached?
2. What are the risks to the data subjects if the data is modified?
3. What are the risks to the data subjects if the data is lost?
4. What are the main sources of risk?
5. What steps have been taken to mitigate those risks?

### Training And Professional Development

Developing for data protection isn’t just about code: it’s about the people who write it. GDPR will require developers to know the legal and policy landscape of their profession. (This has been the norm for other fields for centuries: how embarrassing for us.)

All contributors to a project, whether they are employees, contractors, or volunteers, will be expected to be competent in, at the very least:

- The European data protection and privacy frameworks (GDPR and ePD);
- Any additional local, regional, or national privacy laws;
- Any industry- or sector-specific data requirements, such as those in the health and financial service industries; and
- Any development frameworks and methodologies used as standard within the workplace.

A privacy-conscious workplace will provide training on these frameworks as part of a new employee’s induction, and will also provide refresher training as required.

In the coming years, we can expect to see knowledge of legal frameworks on privacy set forth as prerequisites in job descriptions. Schools and coding academies should include the frameworks within their curricula.

Under GDPR, a regulator’s investigation into a data breach or a privacy concern will include an examination of what training has been provided. If there is no documented evidence that staff and contributors have been given training, or were required to be competent in the data protection and privacy frameworks which govern their work, the investigation will be more unpleasant than it would have been otherwise.

### Technical And Security Measures

Technical and security measures are as much a part of a healthy GDPR compliance journey as data audits and file storage. These aspects, as with everything under GDPR, have been toughened and tightened up.

A privacy-conscious workflow should include an evaluation of physical access to data. This means on-premises access by staff and contractors. You will need to look at potential misuses of data such as employee logins, unencrypted hardware and peripherals, unprotected servers, and insecure connections.

Most external data breaches begin internally. For that reason, GDPR holds that unauthorized access to data, such as giving an unvetted temp full system access on a generic login account (and didn’t that happen to all of us?), constitutes a data breach as if the data had been passed externally. User access controls have a role to play here.

Good security measures involve system monitoring and logging. It’s worth noting that the data you capture solely for the purpose of security monitoring and prevention should not be conflated with user-generated personal data such as account information, although all technical and security logs should, of course, be collected, retained, and deleted in full accordance with the rest of GDPR’s provisions.

Outside people and peripherals, evaluating technical and security measures must also include auditing your international data transfers. Remember that one of the fundamental principles of the European data protection regime is safeguarding data sent outside Europe to third countries. You will need to ensure that any non-European third parties you use, whether that is a web host, cloud storage, or a business partner, guarantees they are safeguarding your European data to European standards. And yes, you need to get that in your contracts.

## How You Develop

So far we’ve reviewed how GDPR will impact your development workflow from the perspective of business processes and project planning. Now let’s look into the ways it will impact *how you code*. These changes will involve your IT and management teams.

### Coding Standards

Building healthy data protection workflows, and avoiding unnecessary data capture or loss, require everyone in your project to work from a clearly defined set of code libraries, tools, and frameworks. For that reason, your GDPR compliance journey should involve creating a list of approved standards and methodologies used for both coding and testing.

GDPR does not define a list of right or wrong programming languages, version control systems, or testing tools: what matters is that whatever you use is clearly defined and followed for each and every situation you use it in. You may, of course, modify your standard tools and infrastructure at any time, as long as you ensure they are acknowledged and documented as the frameworks which must be used.

Your coding standards must be preventive as well. You should disable unsafe or unnecessary modules, particularly in APIs and third-party libraries. An audit of what constitutes an unsafe module should be about privacy by design, such as the unnecessary capture and retention of personal data, as well as security vulnerabilities. Likewise, code reviews should include an audit for privacy by design principles, including mapping where data is physically and virtually stored, and how that data is protected, encrypted, and sandboxed.

### Design Requirements

Speaking of sandboxing, design requirements are also an integral part of a GDPR-conscious development workflow.

Data protection by default as a design process starts with developing with minimization in mind. Collect the absolute minimum amount of personal data required and no more, both on the front end and back end. Do not link personal data with other data sets stored in a single location. If aggregating data, remove personal and identifying data as much as possible. Anonymisation, although not explicitly required under GDPR, is recommended; however, the greater the risk that anonymized data could be indirectly identifiable or re-identified by aggregating it with additional data, the greater the risk of using it at all.

While GDPR requires you to define data retention and deletion schedules for all the personal data you hold, it does not require you to delete everything as a rule. You may, for example, wish to keep all purchasing records for ten years for tax and auditing purposes. That is perfectly acceptable, as long as you document that fact and its rationale. A user’s request for account deletion would not require you to delete their purchasing records from your tax and accounting records; the right to be forgotten is not the right to fly under the radar.

Data should be deleted, either automatically or through user actions, when it is no longer needed. Take care to think of how deleted data may still be present in archives and backups. You will also need to work with third parties whom you pass data to or receive it from, such as a SAAS or a cloud service, to ensure that a request for data deletion on your end also removes the data on their end, and to verify that this has been done.

Another aspect of privacy-conscious system design is hiding and protecting data from unnecessary user access. Personal data should not be visible in plain view, either on the front or back end, nor should all users of a system have universal access. Data should also be encrypted in transit and at rest.

Your system design reviews should view your flows of personal data through the eyes of an attacker, be it human or otherwise. How would someone (looking for personal data to exploit) find what they were looking for and how easy have you made it for them?

### Consent And Subject Access Mechanisms

The European data protection overhaul is all about returning control over data to the people the data is about through consent and subject access mechanisms. We all need to be informed about the data flows containing our information, and our rights over them, in the most privacy-positive ways possible.

On the front end, this means providing better consent mechanisms and user controls. Your projects and applications should provide optimal control over consent settings through things like control panels, user dashboards, account settings, and privacy centers. These choices, at all times, must be granular; a user must be able to invoke any aspect of control over their data at any time. (The days of having to choose between accepting anything a site wants to do with your data or deactivating your account are over.)

You’ll also need to provide an interface for individual subject access rights, such as the rights to edit and correct information, the right to download data, the right to restrict processing, and the right to data deletion (the frequently misunderstood “right to be forgotten”). Account settings and privacy dashboards are the ideal homes for these options.

On the back end, you should develop to enforce user consent and choice. A user setting up an account for the first time should enjoy optimal privacy settings by default; they should not have to opt-in *to* privacy, or switch *off* defaults to achieve it.

Additionally, consent must never be assumed through a *lack* of action, such as a failure to tick a box or the mere creation of an account, so you should develop ways to alert users to the fact that they have not yet granted opt-in consent to any applicable choices and options.

Your back-end development process will also need to ensure timestamped documentation of what consent a user gave, how they gave it, and whether or not they have withdrawn it.

### Testing And Maintenance

Finally, developing for GDPR means adding privacy by design and data protection by default to your testing processes. These should supplement existing procedures such as penetration testing.

Your privacy testing procedures should predict the ways unauthorized users would access actual data on your system. Would a suspicious search for user data, or an alteration to a record, be logged as a security vulnerability? Is data stored in login cookies? Could someone gain access to data by intentionally triggering an error? What do you do about users who have used plaintext or silly passwords? If you are applying privacy by design retroactively to an existing project, have you tested how easy it is to access legacy data? This is where you have to think really creatively &mdash; and somewhat maliciously &mdash; about how and where data can escape to where it should not be.

Testing for data protection by default should also consider external alerts. Do you have a means for the public to alert you to data breaches, either potential or real? What about bug bounties and responsible disclosure programmes?

And remember the golden rule of GDPR &mdash; document it, or it didn’t happen. Your testing results, and the methodologies you used to achieve them, need to be noted and actioned as living documents.

## Get It Right From The Start

We’ve shown you how GDPR requires you to be more thoughtful about the sites and services you build, more transparent about the ways you collect and use data, more considerate of your users, and more thorough in your development and documentation processes. If you were expecting scary legal mumbo-jumbo, we won’t apologize. GDPR is only a complicated legal burden if you want it to be. The European privacy overhaul is really about adopting common-sense safeguards for data protection and privacy as fundamental parts of your development workflow on the code and process levels.

Now, did you notice that we only mentioned lawyers once? None of what we have discussed, save for contracts with your third-party suppliers, requires a legal department. You can get started with all of this right away. And you should. At a time when privacy and security are the biggest ethical challenges facing our industry, the European privacy overhaul is a powerful toolkit for taking responsibility for protecting the people in your data. Use that for what it is.

## Links And Resources

- "[The Ultimate GDPR Guide for Marketers and Businesses](https://appinstitute.com/gdpr-guide/)," A really detailed overview of GDPR
- "[Data protection: Better rules for small business
](https://ec.europa.eu/justice/smedataprotect/index_en.htm)," An overview of GDPR, European Commission
- "[Digital privacy](https://ec.europa.eu/digital-single-market/en/policies/online-privacy)," Digital Single Market, European Commission
- "[Software development with Data Protection by Design and by Default](https://www.datatilsynet.no/en/regulations-and-tools/guidelines/data-protection-by-design-and-by-default/)," Datatilsynet (Norwegian data protection regulator, in English)
- "[Designing for new digital rights](https://newdigitalrights.projectsbyif.com/)," Projects by IF (Prototypes for informed consent)
- "[Anonymisation: Managing data protection risk](https://ico.org.uk/media/for-organisations/documents/1061/anonymisation-code.pdf)," Code of practice, Data protection, Information Commissioner’s Office (PDF)
- "[GDPR national implementing legislation across Europe](https://www.twobirds.com/en/hot-topics/general-data-protection-regulation/gdpr-tracker)," GDPR Tracker
- "[Full EU legal text of the GDPR](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=OJ%3AL%3A2016%3A119%3ATOC)," EUR-Lex Access to European Union law
- "[Global privacy laws](https://globalprivacymatrix.bakermckenzie.com/)," Baker & McKenzie

{{< signature "ra, il" >}}

