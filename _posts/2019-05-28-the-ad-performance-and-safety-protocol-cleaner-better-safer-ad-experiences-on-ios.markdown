---
title: 'The Ad Performance and Safety Protocol: Cleaner, better, safer ad experiences on iOS '
date: 2019-08-28 18:20:00 -04:00
categories:
- written-for-the-washington-post
tags:
- ad-tech
- interventions
vertical: Ad Tech
hashtag: AdSafety
image: https://raw.githubusercontent.com/AramZS/aramzs.github.io/master/_includes/safety-key.jpg
excerpt: The Washington Post is taking a proactive approach to digital display advertising issues with a new project that is set to fix bad code.
isBasedOn: https://washpost.engineering/the-ad-performance-and-safety-protocol-cleaner-better-safer-ad-experiences-on-ios-a5d474468957
canonical: https://washpost.engineering/the-ad-performance-and-safety-protocol-cleaner-better-safer-ad-experiences-on-ios-a5d474468957
writtenFor: The Washington Post
---

The Washington Post is taking a proactive approach to digital display advertising issues with a new project that is set to fix bad code, while saving brands from code errors and cross-platform bugs in ad code. The Ad Performance and Safety Protocol (APSP) focuses on accidentally harmful ad behaviors to ensure a better user experience for all readers on The Post’s Classic iOS App.

Ad safety has become a major issue for publishers over the last few years. Most solutions that have approached the issue have done so with a fundamentally reactive mindset. The assumption is that the majority of ad problems experienced by users are malicious actors in the landscape. This approach is one that is needed, but it does make an incorrect assumption: that users’ bad experiences with ads are only found in malicious events.

While malicious events stand out to users and need to be secured, bad performing advertisements is a highly common experience users have with ads. The advertising technology landscape is filled with badly performant, slow, and malfunctioning advertisement code. While the largest impact this has is on slowing websites down, the issue became far more urgent for our Classic App when we determined users were experiencing two major problems at a high frequency. The first was a flaw in a common iOS package that was causing video to accidentally pop out of the ad frame. The second was a common script used to build ad animations that had a flaw causing an impact on iOS device performance. After testing and review, the iOS and RED teams at The Washington Post determined a fundamentally different approach was in order.

To supplement our existing anti-fraud and anti-malicious-ad measures, we needed a proactive approach that worked with ad code to alter it for better performance. The solution was the Ad Performance and Safety Protocol, a set of checks and responses that actively scanned ad code coming into the app and determined a way to increase ad performance and decrease cross-platform bugs that were causing a worse ad experience for users.

Changes to HTML specification a few years ago encouraged developers to replace common gif-style animation with background video elements. These elements are intended to be part of the ad’s overall presentation but a bug in some of the underlying standard code used to display ads in iOS can cause these videos to ‘pop out’. This is not an experience we or users want and because the video is intended to be background animation it is usually unbranded and strange to users. We resolve this issue with proactive code insertion.

Additionally, a few very common ad scripts used by auto-generating design tools have issues we have diagnosed as causing infinite looping of code functions. These excessively overuse device CPU long after they have completed doing anything for the ad itself. APSP will stop these loops at the point we have decided to no longer allow any type of ad animation, when the scripts no longer have any use for the ad. This should have no impact on well-implemented analytics and viewability tools within the ads themselves.

We have deployed this solution successfully, intervening in ads that would otherwise have negatively impacted reader devices and improving system performance for over a third of ads displayed. The result is faster ads, a better user experience and a safer overall environment for Washington Post iOS users.

<hr />
<br />

_[I originally wrote this on behalf of The Washington Post for their Engineering Blog. The original post can be found here](https://washpost.engineering/the-ad-performance-and-safety-protocol-cleaner-better-safer-ad-experiences-on-ios-a5d474468957)._

“Safety Key” by Got Credit is licensed with CC BY 2.0. To view a copy of this license, visit https://creativecommons.org/licenses/by/2.0/
