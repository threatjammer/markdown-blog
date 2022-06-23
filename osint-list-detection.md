---
title: 'OSINT denylists in Threat Jammer'
excerpt: 'One of the abuse detection strategies in Threat Jammer uses Open Source Intelligence (OSINT) denylists found in net. Learn how to use them.'
coverImage: '/blogimg/osint-list-detection.png'
created: '2022-06-28'
updated: '2022-06-28'
readTime: 2
version: '1.0.0'
navigation:
  github: https://github.com/threatjammer/markdown-blog/blob/main/osint-list-detection.md
  home: /blog/main
  previous: 
  next: 
authors:
  - name: Diego Parrilla
    link: 'https://github.com/orgs/threatjammer/people/diegoparrilla'
ogImage:
  url: ''
---

## What are OSINT denylists?

Open source intelligence (OSINT) is the practice of collecting information from overt and publicly available sources to produce actionable intelligence. OSINT is of value to answer intelligence requirements and is distinguished from research in that it applies the process of intelligence to create tailored knowledge supportive of a specific decision.

In the context of Threat Jammer, OSINT denylists are a set of curated IPv4 and IPv6 datasets found from multiple sources in the internet that helps to answer the intelligence requirement of determining what is the risk of a connection made from a source IP address.

Threat Jammer has a search engine to query for the different types of OSINT denylists in the page [OSINT lists](https://threatjammer.com/osint-lists).


## Why OSINT denylists matter

There are hundreds or may be thousands of OSINT denylists in the wild with different level of *signal strength* and *signal/noise ratio*. We take care of curating and selecting which denylists are really relevant and accurate. Apart from the obvious, we also categorize them and assign a risk based on a multivariable function.

**We apply a process of intelligence to create the tailored knowledge described above.**

Threat Jammer implements a multifactorial approach to Threat Detection, and a very important factor are OSINT denylists. 

OSINT denylists can be a factor with a very high level of confidence in case of a positive. In case of a negative (no matter if it's true or false negative), we should rely on a different factor to determine a Threat. 

The downside of OSINT denylists has to do with the percentage of false-negatives (a Threat was not detected because the IP was not found in the denylist) higher than other type of detections methods like behavioural. 

To minimize false-negatives we try collect a very large dataset from multiple sources and also very frequently, with time ranges of less than an hour.

And to minimize too, we also implement the multifactor approach.

## What are dataset sources?

## What are the different time ranges for each denylist?

## Different OSINT sources for different subscription levels.

## Why risks are different depending on the denylist and the time range?

## And the future?

If you want to learn more, you can read the [documentation in our site](https://threatjammer.com/docs)

And of course you can follow us on [Twitter](https://twitter.com/threatjammer) and [Github](https://github.com/threatjammer). Or join our [community in Discord](https://threatjammer.com/community).
