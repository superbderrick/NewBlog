---
emoji: 🎮 
title: Data Collection and Storage apple iOS inapp review
date: '2024-07-06 15:20:00'
author: Derrick
tags: Unity iOS adid firebase
categories: Unity iOS
---

    Guideline 5.1.1(v) - Data Collection and Storage
    5.1.1(v) Account Sign-In If your app doesn’t include significant account-based features, let people use it without a login. If your app supports account creation, you must also offer account deletion within the app. Apps may not require users to enter personal information to function, except when directly relevant to the core functionality of the app or required by law. If your core app functionality is not related to a specific social network (e.g. Facebook, WeChat, Weibo, Twitter, etc.), you must provide access without a login or via another mechanism. Pulling basic profile information, sharing to the social network, or inviting friends to use the app are not considered core app functionality. The app must also include a mechanism to revoke social network credentials and disable data access between the app and social network from within the app. An app may not store credentials or tokens to social networks off of the device and may only use such credentials or tokens to directly connect to the social network from the app itself while the app is in use.


I will write logs how to pass iOS in app review from Guideline 5.1.1(v) - Data Collection and Storage case

I currently work for is sensitive to data collection and storage because it is an app targeting Kids apps
Espacailly even it's kids app, if we have a ads module or any third parties data collecion module, it might be reject by app review 

In Firebase, we can enable the Analytics without IDFA (device advertising identifier) ​​collection
I successfully submitted my review using this option!


    pod 'Firebase/AnalyticsWithoutAdIdSupport'

https://firebase.google.com/docs/analytics/configure-data-collection?hl=ko&platform=ios
