---
layout: post
title:  "Configuring Web Applications"
date:   2015-03-21
tags: ['mobile', 'html']
---

Specifying a Webpage Icon for Web Clip:

```html
<link rel="apple-touch-icon" href="touch-icon-iphone.png">
<link rel="apple-touch-icon" sizes="152x152" href="touch-icon-ipad-retina.png">
<link rel="icon" sizes="152x152" href="touch-icon-android.png">
```

Specifying a Startup Image:

```html
<link rel="apple-touch-startup-image" href="/startup.png">
```

Hiding Safari User Interface Components:

```html
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="mobile-web-app-capable" content="yes"> <!-- android -->
```

Changing the Status Bar Appearance:

```html
<meta name="apple-mobile-web-app-status-bar-style" content="black">
```

Setting the Launcher Title：

```html
<meta name="apple-mobile-web-app-title" content="Kojitsu">
```

format-detection:

```html
<meta name="format-detection" content="telephone=no">
```

Linking to Other Native Apps:

```html
<a href="tel:1-408-555-5555">Call me</a>
<a href="facetime:01234567890">Call using FaceTime</a>
<a href="facetime:hello@example.com">Call using FaceTime</a>
<a href="sms:">Launch Messages App</a>
<a href="sms:01234567890">Send an SMS</a>
<a href="http://maps.apple.com/?q=cupertino">Cupertino</a>
```

see more: [Safari Web Content Guide](https://developer.apple.com/library/mac/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html#//apple_ref/doc/uid/TP40002051-CH3-SW2)，[Safari HTML Reference](https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html)，[Apple URL Scheme Reference](https://developer.apple.com/library/mac/featuredarticles/iPhoneURLScheme_Reference/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007899)
