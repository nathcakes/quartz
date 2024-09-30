---
title: Managing & Releasing Beta Applications
draft: false
tags:
  - technical
date: 2024-07-19
---
 Mobile applications must be distributed to users through the Apple App Store or Google Play Store. My application development classes at university didn't cover this aspect of development, so it was an excellent self-learning opportunity. Specifically for Omni, we needed to distribute a restricted version of the application that only allowed users we selected to download and use the app. 

Fortunately, both Apple and Google provide tools within their platform to enable easy management of beta applications. As our customer pilot was restricted to Apple devices, I focused on learning TestFlight. Once I had created the AppStore Connect account for Omni Biotech, I had to fill in some basic information about the application and submit a version for testing by Apple. This was the most difficult part of managing the beta release, as Apple has strict requirements. Due to running Python on the device, I was required to implement changes to the Omni Biotech website, links within the application and some application code.  

Once a version is approved, you can create groups of users that are invited via email to test your application. This provided some baseline statistics, such as the number of installs, crashes, and feedback submitted. Over the course of the 3-week pilot, I released 15 updates, and the application was used over 700 times, which was a really exciting feeling. I can now confidently say I know how to create and release an application all the way through to the user's device, and it is a critical skill for becoming a mobile application developer.

![[testflight_screenshot.png]]
<p style="text-align: center; font-style: italic;">Artefact: The dashboard page of our TestFlight showcasing most of the updates and statistics</p>