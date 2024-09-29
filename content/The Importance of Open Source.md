---
title: The Importance of Open Source
draft: false
tags:
  - technical
date: 2024-08-03
---
While working on [[Running Python on Mobile Devices - Part 1]] and building our machine learning (ML) pipeline, I had difficulties optimising the performance of the code and freezing the UI while we processed the data. I had tried to implement asynchronous processing; however, due to the design of Python and the limited control of how it runs on the phone, I was unsuccessful. I investigated alternative solutions by performing a Google search and reviewing multiple StackOverflow posts and articles written on Medium and the Swift Developer Forums. 

[A post](https://forums.swift.org/t/does-anyone-know-if-pythonkit-supports-subthreads/68583/8) described a similar issue to what I was experiencing, and another developer offered his solution as an open-source fork of the original PythonKit library used to enable Python on iOS. It was serendipitous that the prior weekend, I was listening to an old episode of my favourite developer podcast, [Syntax.fm](https://syntax.fm/guest/bdougie) when they interviewed Brian Douglas, the creator of Opensauced, a website that encourages developers to participate in open-source development. This experience made me appreciate the importance of open-source work and contributing to the community when possible; without this repository, I wouldn't have been able to improve the app. 

This experience inspired me to make my first open-source contribution when I discovered an error in the documentation for the mobile app's error-tracking software I was implementing. Normally, after resolving the issue, I would move on, but instead, I updated the documentation and created a [pull request](https://github.com/getsentry/sentry-docs/pull/10645) for this to be shared with future developers. Learning how easy it was to submit my changes has removed my fear about open-source contributions, and I plan to make more contributions this coming summer break.

![[Pasted image 20240926184053.png]]
<p style="text-align: center; font-style: italic;">Artefact: Screenshot of open-source pull request made to Sentry</p>
<p style="text-align: center; font-style: italic;">Viewable at:  <a href="https://github.com/getsentry/sentry-docs/pull/10645">https://github.com/getsentry/sentry-docs/pull/10645</a></p>
