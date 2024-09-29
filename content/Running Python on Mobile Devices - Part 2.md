---
title: Running Python on Mobile Devices - PythonKit
draft: false
tags:
  - technical
date: 2024-06-24
---
I initially wrote this reflection as one very long piece, but there is a natural break in the two segments, with different skills developed. Therefore, I have split them into two reflections. You can read Part 1 here: [[Running Python on Mobile Devices - Part 1]].

I now understand the full scope required to run the machine learning (ML) models locally on the device; however, I didn't know where to begin implementing it. At this time, we were three weeks away from the beginning of the customer pilot, so there was not enough time to rewrite the Python code into native code and test it thoroughly. Will questioned me, "Why can't we just run Python on the phone?" this felt like an odd question from my point of view as, to my knowledge at the time, it wasn't possible to run Python on phones, especially iOS as Apple heavily restricts what code you can run outside of the supported languages of Objective-C & Swift. However, it sparked my curiosity to truly answer the question, as phones are just small computers, so it should be possible. 

That's how I discovered a fantastic open-source project named [Beeware](https://beeware.org/). Beeware is a project that allows developers to use Python to write applications for all platforms. As an open-source project, they have shared tools to enable running Python on each platform they support, including iOS. They also recently had their code accepted as part of Python version 3.13, so now the latest version of Python can be run on mobile devices as part of the base installation package.

To implement this into our application, I used their base repository as a template to write the code required to enable the Python service in our application. There was a lot of back and forth to troubleshoot some configuration issues. However, once set up, I could import Python as a package into Swift and have it run any ".py" file. This allowed me to make minimal changes to the Data Science team's code to run our ML pipeline all on the device, although the performance was less than ideal as it can not be run as a background process currently. 

This experience enlightened me on how much I enjoy working on mobile systems. The manufacturers lock down what it's possible for developers to do on these devices, but there are often escape hatches that enable complex and unique code. I also enjoy the fast feedback loop and the tactile interaction with my code, and I know that this is the field of Software Engineering I want to explore further. This experience also highlights the power of teamwork and exploring all possibilities, which led me to discover this fascinating niche.