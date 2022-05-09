---
title: 'Browser Spoofing: How to detect it?'
excerpt: 'Browser Spoofing is when a web browser identifies itself as a different browser from the one in use.'
coverImage: '/blogimg/browser-spoofing-detect.png'
created: '2022-05-10'
updated: '2022-05-10'
readTime: 2
version: '1.0.0'
navigation:
  github: https://github.com/threatjammer/markdown-blog/blob/main/browser-spoofing-detect.md
  home: /blog/main
  previous: 
  next: 
authors:
  - name: Diego Parrilla
    link: 'https://github.com/orgs/threatjammer/people/diegoparrilla'
ogImage:
  url: ''
---

## What is Browser Spoofing?

When a user requests a web page, many websites check the type of browser used to deliver a specialized page to render it correctly. A lesser-known browser can identify itself as a popular browser as long as it renders pages in the same way. It is not a problem for most websites, but the user experience can sometimes change depending on the browser.

There is an entirely different scenario when the user is not a human but an automated script or a bot. In this case, the bot will try to tease our service by pretending to be a classic interactive browser to obtain an accurate version of the web page. 

A malicious actor can use this trick to hide their real identity and cover the path of their activities by pretending to be a human. 

## The user agent string

A browser's `User-Agent` string (UA) helps identify which browser is used, which version, device, and operating system. When feature detection APIs are unavailable, use the UA to customize behavior or content to specific browser versions. The information that identifies the user agent is transferred to the web server in the HTTP request header. The structure and content of this information of the `user-agent` header are not standardized. Each developer can insert and submit their information. The `User-agent` header was defined in [RFC 2616](https://datatracker.ietf.org/doc/html/rfc2616#section-14.43) and is part of the HTTP protocol.


The syntax of the `user-agent` header is:

```
User-Agent: <product> / <product-version> <comment>
```

A common format for web browsers are:

```
User-Agent: Mozilla/5.0 (<system-information>) <platform> (<platform-details>) <extensions>
```

Where the directives are:
* `product` : A product identifier — its name or development codename.
* `product-version` : Version number of the product.
* `comment` : Zero or more comments containing more details. For example, sub-product information.

And depending on the browser type, the following directives are used:

* `platform` : describes the native platform that the browser is running on (Windows, Mac, Linux, Android, etc.) and if it is a mobile phone. Firefox OS phones say Mobile — the web is the platform. Note that platform can consist of multiple ";"-separated tokens.
* `platform-details` : additional information about the platform. For example, the version of the operating system.
* `extensions` : a list of extensions that are installed in the browser.

As the reader can see, the `User-Agent` header can be a mess. In the history of User-Agent, browsers often pretended to be another browser because some websites serve content based on another type of browser. For example: pretending to be **Mozilla**  is the easiest way to receive the contents with frames. So now, every browser is disguised as another browser like Mozilla to the point that Chrome called itself `Mozilla/5.0`.

Where are we today? Everyone claims to be `Mozilla 5.0`; Android Chrome claims to be Mobile Safari; Mobile Safari claims to be Gecko. It can get very confusing very quickly. The new [Threat Jammer User Agent API endpoint](https://dublin.api.threatjammer.com/docs#/User%20Agent) helps developers to easily classify the user agent string within multiples categories and implement easily policies based on the user agent string.

## Extracting the information from the User-Agent

### Operating systems

You can find information on both the operating system and its version number within a UA string. Each software vendor determines its versioning system and its format. The primary OS used by various devices is Android, Windows, Linux, and Chrome OS. For Apple devices, we have iOS, iPadOS, macOS (previously Mac OS X and later OS X), tvOS, and watchOS.

It seems simple, but don’t assume a software vendor will always follow the same pattern for a new release – sometimes conventions can change, or version numbers are skipped. And if that wasn’t enough, User Agents don’t always present the operating system, devices, browser names, and version numbers consistently.

A UA string of Safari in Mac OS X 10.15.17 shows the Operating system with the substring `(Macintosh; Intel Mac OS X 10_15_7)`.
```
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36
```

A UA string of Firefox in Mac OS X 10.15 shows the Operating system with the substring `(Macintosh; Intel Mac OS X 10.15; rv:99.0)`.

```
Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:99.0) Gecko/20100101 Firefox/99.0
```

### The Browser

The UA string also contains information on the type of web browser of the client. Some are very well-known browsers like Chrome, Safari, Edge, or Firefox.

Each browser vendor (Google for Chrome and Mozilla for Firefox) determines its versioning system. Again, the browser name and version number aren’t always presented consistently.

A UA string of Chrome in Windows shows the version with four numbers separated by dots.
```
Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36
```

A UA string of Firefox in Windows shows the version with two numbers separated by dots.
```
Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:99.0) Gecko/20100101 Firefox/99.0
```

### Device hardware

There is a crucial element that can be used to detect the device. This element details whether the physical device accessing the website is a mobile phone, tablet, e-reader, smart TV, games console, etc.

For example, the UA string below tells us that the device is a 2018 model Samsung Galaxy A6+ (SM-A605FN):

```
Mozilla/5.0 (Linux; Android 10; SAMSUNG SM-A605FN) AppleWebKit/537.36 (KHTML, like Gecko) SamsungBrowser/12.1 Chrome/79.0.3945.136 Mobile Safari/537.36
```

Sometimes, it’s challenging to find the device’s hardware. The biggest reason for this is that the UA string lacks information.

### Crawlers

User-Agent strings aren’t always associated with a client device used by humans. Sometimes they represent something called a *crawler*.

A *crawler* is a type of web traffic that operates without human interaction. Its purpose is to monitor the availability or performance, retrieving information to be included in search engines or monitoring services.

A good crawler will identify itself as a crawler, often including “bot” at some point within their UA string:

```
Mozilla/5.0 AppleWebKit/537.36 (KHTML, like Gecko; compatible; Googlebot/2.1; +http://www.google.com/bot.html) Chrome/99.0.4844.84 Safari/537.36
```

However, malicious crawlers may scrape your website, harvest your data, or take advantage of potential vulnerabilities. They will actively try to hide their intentions and spoof their User-Agent to look like an ordinary string.

## Using the Threat Jammer User-Agent parser

The Threat Jammer User-Agent parser API comes to rescue. It is a simple API REST endpoint that can be used to extract all the information from a User-Agent string and return it classified into different categories in a JSON object. The developer only has to pass as argument the User-Agent string (or the list User-Agents) and the API will return the parsed UA in such a way that it can be easily used in your application.

> **You need an API Key to access the endpoints. Sign up for free at [Threat Jammer](https://threatjammer.com) and get your API Key.**

The group of endpoints to manage User Agents are [here](https://dublin.api.threatjammer.com/docs#/User%20Agent):

![Threat Jammer User Agent Endpoints](/blogimg/user-agent-endpoints.png)

### Parse a User-Agent of a browser

The endpoints that can be used to parse a User-Agent string are:

- `GET /v1/ua/{user_agent_urlencoded}` : The User Agent can be passed as an argument in query string. It must be URL enconded, otherwise it will not be recognized.
- `POST /v1/ua` : A list of User Agents can be passed as a body. The User Agents do not need to be URL encoded.
- `POST /v1/ua/csv` : A list of User Agents can be uploaded as a CSV file. The User Agents do not need to be URL encoded.

For the sake of simplicity, we will use the endpoint `POST /v1/ua` with a single UA.

```
curl -X 'POST' \
  'https://dublin.api.threatjammer.com/v1/ua' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer YOUR_API_TOKEN' \
  -H 'Content-Type: application/json' \
  -d '[
  "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36"
]'
```

The response is a JSON object with the following structure:

```
{
  "self": "/v1/ua",
  "results": [
    {
      "self": "/v1/ua/Mozilla%2F5.0%20%28Windows%20NT%2010.0%3B%20Win64%3B%20x64%29%20AppleWebKit%2F537.36%20%28KHTML%2C%20like%20Gecko%29%20Chrome%2F100.0.4896.127%20Safari%2F537.36",
      "string": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36",
      "classification": "CLIENT",
      "type": "/v1/ua/type/BROWSER",
      "agent": "Chrome 100.0.4896.127",
      "engine": "WebKit/Blink",
      "version": "100",
      "latest": "101",
      "family": "/v1/ua/family/CHROME",
      "vendor": "/v1/ua/vendor/GOOGLEINC",
      "os": "/v1/ua/os/WINDOWS10",
      "device": "/v1/ua/device/DESKTOP",
      "frequent": "COMMON"
    }
  ]
}
```

The information extracted from the User-Agent string can be classified using different categories:

- `classification`: The classification of the User-Agent string based on the interactive use: `CLIENT` for an interactive browser, `CRAWLER` for an automated crawler and `UNKNOWN` for an unknown user agent.
- `type`: The type of the User-Agent string.
- `agent`: The name of the agent and the version, if any.
- `engine`: Agent render engine.
- `version`: Agent version.
- `latest`: Latest version of the agent. If the agent is up to date, the latest version is the same as the current version.
- `family`: URI to the family of the agent.
- `vendor`: URI to the vendor that produces the agent.
- `os`: URI to the operating system used by the agent.
- `device`: URI to the device used by the agent.
- `frequent`: If the agent is frequently used worlwide or not. The values are `COMMON`, `RARE`, and `UNKNOWN`. A `COMMON` agent means that the agent is in the top 50 of the most used client devices worlwide.

With our API endpoint, the user can get a very accurate and detailed categorization of the User-Agent string and implement a risk management system policy based on structured data.

### Parse a User-Agent of a crawler

Now we will use the same endpoint to parse a very common crawler UA string. The Google Search bot:

```
curl -X 'POST' \
  'https://dublin.api.threatjammer.com/v1/ua' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer YOUR_API_TOKEN' \
  -H 'Content-Type: application/json' \
  -d '[
  "Mozilla/5.0 AppleWebKit/537.36 (KHTML, like Gecko; compatible; Googlebot/2.1; +http://www.google.com/bot.html) Chrome/99.0.4844.84 Safari/537.36"
]'
```

The response is a JSON object with the exact same structure of the browser, but the classification is now `CRAWLER` and the categories can differ:

```
{
  "self": "/v1/ua",
  "results": [
    {
      "self": "/v1/ua/Mozilla%2F5.0%20AppleWebKit%2F537.36%20%28KHTML%2C%20like%20Gecko%3B%20compatible%3B%20Googlebot%2F2.1%3B%20%2Bhttp%3A%2F%2Fwww.google.com%2Fbot.html%29%20Chrome%2F99.0.4844.84%20Safari%2F537.36",
      "string": "Mozilla/5.0 AppleWebKit/537.36 (KHTML, like Gecko; compatible; Googlebot/2.1; +http://www.google.com/bot.html) Chrome/99.0.4844.84 Safari/537.36",
      "classification": "CRAWLER",
      "type": "/v1/ua/type/SEARCH_ENGINE_BOT",
      "agent": "Googlebot/2.1",
      "engine": "",
      "version": "2.1",
      "latest": "2",
      "family": "/v1/ua/family/GOOGLEBOT",
      "vendor": "/v1/ua/vendor/GOOGLEINC",
      "os": "/v1/ua/os/UNKNOWN",
      "device": "/v1/ua/device/DESKTOP",
      "frequent": "RARE"
    }
  ]
}
```

The crawler was identified as a Google Search bot type for Desktop crawling. The `frequent` field is now `RARE` because the agent is not a client device.

## Implementing a User-Agent based risk detection policy

### Check if the User-Agent is a client device

The first and obvious thing to do is to check if the User-Agent is a client device. We can do this by checking the `classification` field. If it is `CLIENT`, we can assume that the user is a client device, otherwise we can assume that the user is a crawler. It can be useful to implement a policy to block crawlers or to allow only a specific set of them.

### Check if the version of a client device is up to date

The second thing to do is to check if the version of the client device is up to date. We can do this by checking the `latest` and `version` fields. A client device that it is not up to date does not mean that the user is a crawler or a malicious user, but malicious crawlers don't update the User Agent very often and are a good signal to perform more security checks or add friction to the experience of the user.

### Check if the User-Agent is frequently used

The third thing to do is to check if the User-Agent is frequently used. We can do this by checking the `frequent` field. If the agent is `RARE`, we can assume that the user is not frequently used -as I explained above malicious crawlers don't update the User Agent very often- and therefore the user can be a candidate to be a hidden crawler.

### Check if the User-Agent changes from one connection to another

The fourth thing to do is to check if the User-Agent changes from one connection to another. We can do this by checking the `string` field. This check implies that the developer can track the user across different connections or sessions. A change in the User-Agent from the same connection or session does not mean that the user is a crawler or a malicious user, but if it happens it can be a good idea to perform more security checks or add friction to the experience of the user.

## And the future?

The User Agent information is a great way to detect malicious users and crawlers. However, it is not enough. Just the User Agent information is not enough to detect fraudsters. We are working on new features to discriminate bad actors from good ones. Stay tuned!

If you want to learn more, you can read the [documentation in our site](https://threatjammer.com/docs)

And of course you can follow us on [Twitter](https://twitter.com/threatjammer) and [Github](https://github.com/threatjammer). Or join our [community in Discord](https://threatjammer.com/community).

**(C) 2022 - Browser logos images are [property of their respective owners.](https://github.com/alrra/browser-logos)**