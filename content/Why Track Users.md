---
title: Why Track Users?
draft: false
tags:
  - UX
date: 2024-09-03
---
 User tracking is a complex issue that has developed greatly since the introduction of the internet. Many users are now aware that websites and apps may track what sites they visit, how long they visit them, and other data due to the introduction of data privacy laws such as the European GDPR or Apple's "Ask not to track" feature in iOS. I believe that user privacy is important and that users should be made aware and given a choice to opt into tracking features. This is even more paramount regarding private information, such as medical data, like what we collect to provide hydration values. 

Given this, we designed the application to store as little personal identifying information as possible and didn't implement any user tracking frameworks. This was great for the privacy of our users. However, it had consequences that I did not anticipate. Firstly, during the first week of the pilot, users reported intermittent crashes and poor performance to us; however, due to the lack of user tracking frameworks, I could not gather any crash log data, making it very difficult to troubleshoot. Users had to give up their time to give us more detailed feedback so we could recreate and correct the issues. There are privacy-friendly frameworks that could have provided us with this information. 

Furthermore, de-identifying our data became an issue when generating a summary report requested by the client. They wanted information regarding the amount of usage by workers, time spent in the application and an analysis of the impact of offline processing on data stability. These requests were impossible to fulfil as we had not collected any metrics regarding the app's usage.

This has taught me the double-edged sword of user tracking and its importance in enterprise business. After the pilot, I integrated a feedback & crash reporting tool to enable us to assist users better. I scoped a view within the application to explain what data we collect and why, allowing us to build in the company requirements for usage metrics while still following our ethics. 

![[Pasted image 20240929223043.png]] 
<p style="text-align: center; font-style: italic;">Artefact: A screenshot of our new Feedback & Crash Reporting Tool displaying an error </p> 
