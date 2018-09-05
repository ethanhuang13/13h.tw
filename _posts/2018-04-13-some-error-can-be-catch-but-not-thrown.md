---
layout: post
title: Some Error can be catch but not thrown in Swift
---
There are SKError/HKError in StoreKit/HealthKit. They have errorCode, errorUserInfo, and errorDomain, which means they *could* conform to CustomNSError. You can catch them, but to throw them as Swift Error, you need to "extension SKError/HKError: Error { }" youself. 

Why? 🤔

Sample code is [here](https://gist.github.com/ethanhuang13/f8cd1494e7316bd0a47d30886110e918).
