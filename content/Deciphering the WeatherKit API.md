---
title: Deciphering the WeatherKit API
draft: true
tags:
  - technical
  - API
date: 2024-04-27
---
Idea 
- Talk about the issues with the Apple WeatherKit API compared to standard APIs 
- Talk about how you used modern tools and experimentation to solve the problem

The current environmental conditions are an important factor when determining the heat stress of an individual and providing a recommendation on whether they should continue work. We needed to get the predicted conditions for the user's current location and store it for up to 5 days in case there was intermittent or reduced internet access. After investigating multiple solutions, I decided to use Apple's WeatherKit API as they use government sources from around the globe, and we receive a monthly quota of API calls as part of our license fees for developing iOS applications.




I intend to write a blog post in the coming weeks to provide a walkthrough of the steps I had to take and provide more complete documentation for using the API. This will help develop my writing skills and progress towards my goal of building an online presence this year,  to improve my resume for a role as a developer relations manager. 