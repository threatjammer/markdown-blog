---
title: 'Why Threat Jammer?'
excerpt: 'Threat Jammer is a cloud-based risk assessment platform to identify and mitigate abuse and threats, but why? Follow me in this story.'
coverImage: '/blogimg/why-threatjammer.png'
created: '2021-02-16'
updated: '2021-03-07'
readTime: 2
navigation:
  github: https://github.com/threatjammer/markdown-blog/blob/main/why-threatjammer.md
  home: /blog/main
  previous: 
  next: 
authors:
  - name: Diego Parrilla
    link: 'https://github.com/orgs/threatjammer/people/diegoparrilla'
ogImage:
  url: ''
---

## Why Threat Jammer?

I've been doing Threat Intelligence products for several years now and many more developing cloud services consumed via an API. Why a new service like Threat Jammer? What's so special about it? How did it all start? And what will it offer us in the future?

##  How did it all start?

After leaving my previous company (which incidentally [acqhired my previous threat-intel company](https://www.geekwire.com/2020/auth0-makes-first-ever-acquisition-launch-new-tools-protect-automated-cyberattacks/)) I spent several months reviewing studies and papers from universities. They take a more theoretical and less executive approach to the problem of threat detection than the one we usually take in the industry, but the conclusions are perfectly valid.

Although most of these studies have somewhat limited application in "real cyber warfare" scenarios, I did find approaches to the issues that could be perfectly valid if properly "grounded" in a professional, non-academic setting. 

When we face the detection of a threat, we must be aware of the following challenges:
- What was valid for detecting a threat yesterday may not be valid today: the **time** variable is critical. 
- Threat detection is a multi-factor problem: A multi-factor assessment function reduces errors, mainly False Positives and Negatives.
- Data quality is critical. It is more important to have good data than big data.

## What's so special about it?

Deciding whether an actor will perform a harmful action becomes a problem of selecting the best data and the best factors in that assessment function. And that's where Threat Jammer excels. 

While I was on my sabbatical, I had the chance to read a paper about how my previous company performed better than other OSINT tools detecting threats. It was announced in the [2020 International Conference on Computing, Networking, and Communications (ICNC)](https://www.researchgate.net/publication/340306013_IP_Reputation_Analysis_of_Public_Databases_and_Machine_Learning_Techniques) and it is a great read. Once my vanity was gone, I decided to understand why my previous company was performing better than other tools. My conclusion is that I unconsciously conducted a pre-assessment of the data, and I was able to identify the best OSINT sources.

So the question now was: can I implement a service that automatically pre-assesses the different data sources and then selects the best ones? Can I build a service that learns from the various external inputs and cherrypick the best factors to use in the assessment function?

Well, here's the answer: Welcome to Threat Jammer!

## Threat Jammer in a nutshell

Every company offering a digital service has a different approach to abuse detection because business models are not the same and their needs. Cybercriminals are always thinking about how to exploit the services. It becomes a never-ending cat and mouse game no matter how much a company dedicates to protection from abuse. The response to new ways of exploiting the services must be agile, prompt, and effective.

**Threat Jammer is a tool for builders.** Threat Jammer is a set of services acting as building blocks of the threat detection strategy of digital companies. We understand how hard it is to find a solution to detect and block malicious activity, and that's why our services are built to solve this problem: **you know what to do; we offer the tools to make it.**

The Threat Detection Engine constantly evolves. The factors used to detect and block malicious activity can change over time. For example, the user's IP address can vary over time from one network provider to another. The threat level associated with the network provider can change over time, so the user's overall risk level.

Threat Jammer updates the processes and data to maintain the most accurate and fresh information available. The assessments performed will always use the most up-to-date information available. As a result, the system's accuracy will always be the highest, plus reducing the false positives to the bare minimum.

## The pillars of Threat Jammer

### OSINT databases
Open Source Intelligence is a crucial ingredient of any threat intel strategy. The value of Threat Jammer is not just to gather all the different sources and integrate them into a single point of contact. The most relevant value is to categorize them and rank the datasets according to a pre-calculated risk score obtained using different techniques and algorithms transparent to the user.

### CSINT databases
Closed Source Intelligence is an ingredient that increases the quality of any threat intel strategy results. The highest quality and more reliable datasets are often obtained from custom-built extraction processes or directly acquired to external data providers for a fee. Following the same strategy of freshness and accuracy as the OSINT databases, the CSINT databases increase the capacity of our Assessment Engine to detect malicious activity.

### Heuristic Analysis
Heuristic Analysis -or rule-based analysis- is a very effective threat intel tool that, combined with rich and accurate data from the OSINT and CSINT databases—can detect malicious activity. This algorithmic approach is part of the existing set of Threat Jammer services.

### Machine Learning
The amount of data available in the Threat Jammer backend is massive. We have enough data to train different machine learning models to detect malicious activity. Threat Jammer uses the data obtained from OSINT and CSINT sources and the users' behavior, heuristic analysis, and automatic data report to train machine learning models.

### Crowdsourced Intelligence
Crowdsourced Intelligence means that our **users can report their data to the Threat Jammer system**. When users feed Threat Jammer with their data using the Report API, they increase the chance of finding malicious activity and reducing the false positives.

## And the future?

Today we start a journey to deliver the best risk assessment tool for the digital industry. We want to hear from our users about their needs and how they can use Threat Jammer to improve their risk assessment. So, why don't you follow us in this journey and [join us as a Threat Jammer user](https://threatjammer.com/api/signup)?

If you want to learn more, you can read the [documentation in our site](https://threatjammer.com/docs)

You can follow us on [Twitter](https://twitter.com/threatjammer) and [Github](https://github.com/threatjammer). Or join our [community in Discord](https://threatjammer.com/community).