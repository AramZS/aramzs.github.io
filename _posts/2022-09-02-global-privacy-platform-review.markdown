---
title: Comment on the IAB Tech Lab's Global Privacy Platform (GPP)
date: 2022-09-02 10:00:00 -04:00
categories:
- web-standards
tags:
- ad-tech
- privacy
- IAB
- IAB Tech Lab
- compliance
- APIs
vertical: Ad Tech
image: https://github.com/AramZS/aramzs.github.io/blob/master/_includes/portrait_of_a_confused_person_looking_at_a_computer.png?raw=true
hashtag: IAB_GPP
excerpt: The Global Privacy Platform is presented as the final comprehensive answer
  for privacy signaling, but it repeats the worst mistakes of its predecessors.
overlay: red
toc: true
---

## Summary 

The Global Privacy Platform is intended to absorb the functionality of TCF and expand on it, as a consent-string-based privacy solution. While GPP expands the scope that the system can cover it does not resolve any of the intrinsic problems of the TCF approach. The result is a compounding of a deeply flawed system that, while it improves on the underlying concepts, does not resolve the core issues and therefore seems likely to face significant challenge from regulators and privacy advocates. 

While this is a standing issue of TCF, it is extremely troubling that GPP seems like it wants to push the boulder down the road, creating adoption costs, compliance work, and additional technical overhead only to be eventually abandoned for not addressing most regulatory concerns. This would be less of a concern if GPP showed any way that it could be hooked into better solutions, or clear paths towards transformation into a system that would meet compliance expectations. However, GPP–in this draft–does not do that.

While a publisher-based perspective doesn’t have leverage to turn this ship, I recommend against the IAB moving forward on the specification as it currently stands without a fundamental shift in methodology. If there was ever a time to significantly change our approach on consent management, it is now. GPP is not that change. 

- [Summary](#summary)
- [System Assessment](#system-assessment)
  * [API Layering for GPP’s Technical System](#api-layering-for-gpp-s-technical-system)
    + [addEventListener](#addeventlistener)
  * [Notes on Accountability and Signal Integrity](#notes-on-accountability-and-signal-integrity)
  * [GPP’s API](#gpp-s-api)
    + [postMessage](#postmessage)
    + [Stub Code](#stub-code)
    + [cmpId](#cmpid)
    + [Manifest Issues](#manifest-issues)
    + [The Global Vendor List](#the-global-vendor-list)
    + [The Registry API](#the-registry-api)
    + [Mobile SDKs](#mobile-sdks)
  * [Consent String Creation and Management](#consent-string-creation-and-management)
    + [Vendor Consents](#vendor-consents)
    + [A note on the Consent String and Server to Server operations](#a-note-on-the-consent-string-and-server-to-server-operations)
- [GPP Principles](#gpp-principles)
  * [A Note on UI](#a-note-on-ui)
- [Notes on Compliance Issues and GPP’s Relation to EU Court Findings](#notes-on-compliance-issues-and-gpp-s-relation-to-eu-court-findings)
- [Ways Forward](#ways-forward)

## System Assessment

The Global Privacy Platform can be looked at as a four part system. 

The first part is composed of the interactions with previous compliance APIs, including TCF and USPAPI. This has its own flaws, outside of the flaws of the underlying systems which will not be discussed on their own here. 

The second part is the Accountability Platform (AP). While the AP is technically a different set of standards, it is both intended to interact with the GPP and is a fundamental part of supporting the concept of the GPP as an answer to the open legal challenges TCF faces. 

The third part is the GPP API, this system is the technical means by which a user’s consent can be signaled and transmitted. GPP offers some new functionality over the TCF system on which it is modeled, but is mostly derived from TCF, as stated in the proposal: “this RFC builds so heavily upon TCF v2.0 technical design.

The fourth part of the system is the Consent String. This also has some technical improvements and changes over TCF but is identified by the proposal itself as being heavily derived from the TCF2 approach. 

This section breaks down analysis and criticism over each section of the GPP proposal. 


### API Layering for GPP’s Technical System

Where GPP is intended to interact with OpenRTB, I agree with the authors that `ext.gpp` is the correct placement. Placing it on the user object would be confusing and the authors are correct to avoid it.

The GPP proposal would layer over existing APIs. This means that the specification expects that there would be at least 2 APIs preexisting on the page along with GPP instead of being supplanted (TCFv2 and USPrivacy). This is natural as a first step for deployment, I don’t want any gaps in coverage and can’t assume upgraders will do so evenly. However, the spec does not describe any future progression past this point. It is generally undesirable to have to maintain a growing list of window level objects, especially since the specification allows for the concept that other APIs might grow _underneath_ GPP, creating situations where individual APIs multiply and increase complexity of compliance. 

The system also creates a replica command API, to quote the spec:		


> a call to __gpp('iabtcfeuv2.getTCData',myfunction) will be translated by the CMP to __tcfapi('getTCData',2,myfunction).

My hope is that this is conceived as a path towards the eventual depreciation of underlying APIs. However, the spec does not make this clear and it is an unnecessary ballooning of on-page code to handle. 

Even as a path towards depreciation of TCF and the other underlying APIs it seems overcautious. Systems could attempt to use `__gpp` commands first with the `getSection` argument and, if either the on page object or the command doesn’t work, they could then fall back to `__tcf`. In fact, almost every system is likely to do something very much like this anyway. It’s a great deal of unnecessary overhead on the publisher and CMP that will then almost certainly be replicated on the side of other systems. Additional complexity and code like this is undesirable and the spec does not seem to make sufficient arguments for its inclusion. 

This additional complexity also makes the existing flows for the __gpp-level generic commands less clear. The most prominent example is `addEventListener`. 


#### addEventListener

Is it expected that `addEventListener` will also be applied to all the underlying APIs so that every API, _gpp, __tcf, __uspapi, and others on page, will trigger the callback? If __gpp commands that can also apply to underlying APIs are intended to be generic instead of GPP-only this signature is poorly designed and should be reconsidered. Any commands intended to be generic should follow the pattern of the API-specific commands with a format like `all.addEventListener` or some other prefix that makes clear its intended execution. 

“_The addEventListener command returns an EventListener object immediately. It will then call the callback function every time the CMP detects a change (see events below)._” should be rephrased for clarity. Suggested: “_The addEventListener command returns an EventListener object immediately. The GPP script will then call the callback function and return a new EventListener object every time the CMP detects a change (see events below)._”


### Notes on Accountability and Signal Integrity

It is unclear if the Accountability Platform has made significant progress since the last RFC for it. At that time and on review of the accountability approach it was clear the proposals in that space are interesting for after-the-fact auditing. Some of the other proposals are interesting from the perspective of attempting to secure the bidstream data from alteration. None of the proposals seem to address the core problem at the heart of TCF and now GPP, which is that they do not create enforcement mechanisms to force particular data to flow or not flow; they do not guarantee that a single platform would be compliant with a consent signal as received; and they do little to secure the ad tech ecosystem against abuses by buy-side operators, such as misinformation or malware operators, anymore than the existing system does.

Further, the accountability systems do not empower users or organizations that might represent users, be they activist coalitions or individuals seeking to exercise their full rights under privacy regulations, to act to protect themselves. 

Finally, an audit system as proposed means that bad actors are not held credible during a transaction, but after the fact. Existing reports of non-compliant actors in the ad tech ecosystem indicate that there is willingness, capability, and profitability for bad actors to manipulate the bidstream. This would just as easily extend to logs. The 2021 Accountability RFC suggests real-time hooks for accountability and it seems those should be a clear priority over non-real-time attempts at accountability and maintaining signal integrity. 

While there might be some proposals, perhaps even stemming from those linked in the GPP RFC, that could solidify signal integrity of the GPP signal, the current presentation of solutions does not appear to do so. At the current state of the associated proposals there are no sufficient accountability or signal integrity guarantees. 


### GPP’s API

TCF2’s current state is faced with considerable objections from the EU courts. The fact that the GPP API seems to do very little other than replicate it is discouraging. 

Promise operations on-page are a fingerprinting vector, as timing around the response could be used as part of a set of properties that could identify the user. This is an existing problem with TCF and promises are an existing browser-level privacy issue. However, it may be worthwhile to discuss, since GPP is a privacy-related technology, requiring some level of noise in promise return time. While this might be outside of the scope of the GPP specification, I think it would be worthwhile for the IAB to investigate both in terms of risk and the feasibility of avoiding that risk.


#### postMessage

There is no clear statement as to how or if postMessage use is intended to be extended [from the IAB’s TCF2 API](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20CMP%20API%20v2.md#using-postmessage) to GPP. Without notice otherwise, I assume so. postMessage is increasingly at risk for this use, FencedFrames may render it useless. Cross-domain operations with GPP should be explored more in depth in the specification.  


#### Stub Code

I recommend that additional information be added to the spec for the _gpp “stub code”. In the wild under TCF this code is often lacking. Bad implementation causes compliance issues. Many CMPs do not have the stub as part of the default implementation. A stand-alone section should outline the expectations around stub code in more detail. 


#### cmpId

`cmpId` is another carry over from TCF that is generally undesirable. It creates the problem of a centralized list of CMPs, over which gatekeeping can occur. That centralized list is also an obstacle for new entrants. And it is unclear why it is needed in any of the API responses? `cmpId` may be 0 in some responses, as noted by the specification. If the concern is allowing downstream or upstream systems to note a bad actor CMP, why would that system not just fake the CMP ID? What is this number intended to protect or accomplish? It seems like an addition of complexity, data, and oversight to no clear end. 


#### Manifest Issues

The documentation of the Manifest is extremely unclear and requires additional details. Is it expected that every participant would have a manifest including CMPs and Publishers? Published as a JSON or on a simple web page by whom? Where? To what end? Is the manifest expected to just be within the API or the GPP string? Is it expected to be encoded? How is it expected to be used? The specification needs to answer these questions.

Both the `dataUses` and `possibleStates` are poorly documented in this specification. The final specification should be clearer about the intent and use of these fields. They are getting their values from the preceding tables but it is unclear what their use is. Presumably regulatory requirements are understood by all parties? If so why would these fields ever differ between participants? Why would they differ between publishers or CMPs? If so, how are readers of the manifest expected to take that information and use it?


#### The Global Vendor List

The Manifest lists a `gvlUrl` property, GVL presumably indicates the “Global Vendor List”, an IAB-maintained list. Does that mean that property will always be the GVL for the particular compliance framework? Or is it intended that it could be filled by one of the other vendor lists the spec notes. 

As the specification notes, some vendors are on more than one Vendor List. Some vendors are on only one Vendor List. Should the `gvlUrl` be an array to support multiple lists? The GPP specification suggests that all build on the IAB’s Global Vendor List… but the IAB has not gotten even some major advertising systems to sign on to their TCF2 list, which contains a mere 1,142 vendors at last check, a miniscule number compared to the count of overall ad tech operators. As a result it isn’t uncommon for sites to need to reference both the IAB’s list and Google’s ATP list under TCF. Major ad tech vendors have also failed to sign the LSPA. This seems unlikely to change under GPP but this is not acknowledged. Suggesting everyone use the IAB’s GVL is clearly unrealistic. There does not appear to be effective solutions designed for this problem beyond the already insufficient solutions in TCF2, which are overly complex and require significant transmission of data that can max out headers and URLs for ad requests. The discussion about the GPP Identifier in the specification is not a sufficient answer to these questions.


#### The Registry API

The Registry API discussion appears to be an extension of the GVL conversation above it. Beyond the existing functionality of the GVL being questionable, if the specification proposes that there might be use of other vendor lists and the capability to point to them as the primary vendor list in the use of the specification, it should go further and propose a common format, API, and method of access that can be expected by any list that is intended to interact with the GPP and Accountability system. These and future vendor lists are, of course, not bound by any IAB suggestions, but it is ludicrous to propose that vendors might be identified by significantly different IDs across different CMPs or maybe even different GPP calls, without specifying the format by which those vendor lists might be accessed to resolve those IDs. A finalized specification should include the expected format for Vendor Lists and the expected access methods. 

Without specific information about the expected format of vendor lists why wouldn’t bad actors simply specify different vendor lists that are harder to access or audit.  


#### Mobile SDKs

It seems that there is likely to be a great deal of overlap between existing TCF key values in the app and new GPP key values. It’s hard to tell right now since “A full list of all the names will be published in the final specification.” GPP should create more documentation around how the existing values might overlap, what could be an eventual path towards depreciation of replica values, and how that can be minimized. Attaching more and more consent data to users in the app will significantly increase the risk of it becoming a fingerprinting vector, especially when dealing with uneven depreciation of fields, and should be avoided.


### Consent String Creation and Management 

Much of the consent string generation process is replicated wholesale from TCF, including its problems and concerning processes, many of which are already well-detailed by the EU’s courts. This is highly concerning and seems to indicate that work on GPP should be paused. 

Putting that aside for now, GPP has brought forward some useful innovations. After technical testing it appears that the approach of Fibonacci Encoding does not require much additional code and executes quickly. In running an initial test using the most popular encoding algorithm I found that this required less than 2kbs of additional code and was able to execute at a speed ranging from sub-millisecond to 2ms, both server and client side. There are indications that encoding can be handled even faster and with less code. I found this way forward highly effective for compression of data in the way the GPP RFC proposes. 

One of the subsections handles Legitimate Interest. It seems clear from recent EU court cases that this is not possible to claim against a users’ consent and as a methodology it does not seem likely to be replicated by future privacy laws. It should be noted as depreciated or perhaps fully removed from the spec. This also opens up the question of what happens to depreciated data uses or states, which it might be useful to explore in the spec. 

Finally, I really appreciate the un-encoded iteration of the USPrivacy String attached to the end of the GPP string. I believe that the USPrivacy approach represents a clear, transparent, and easy for users to understand methodology that I wish was more broadly applied.


#### Vendor Consents

At the end of the day however, GPP, even with the improvements like Fibonacci Encoding, represents an unbound string that could theoretically expand forever, getting larger and more difficult to manage as the number of privacy laws and vendors increase. Per-vendor consents represent significant problems: the EU courts have challenged them, they are the biggest source of consent string bloat, vendor registry and identification issues plague both TCF and this proposal. It seems impossible to continue with this process, and unrealistic to expect users to dig into those nuances. 

So many problems that GPP faces would be resolved by removing this concept. Vendor consents do not reflect regulator or user expectations for a system like GPP. They encourage the creation of dark patterns and bad UX. Worse they increase the fingerprinting risk for users and the overhead for transmission for publishers and all participants.


#### A note on the Consent String and Server to Server operations

Server to Server operations are not fully explored in this specification beyond use of OpenRTB. However, consent states apply to all sorts of other data transactions including the growing use of 2nd party data trading and clean rooms for targeting. It would be useful for the specification to include a section that addresses how, if at all, it might be used in these contexts. 


## GPP Principles

I generally agree with the GPP principles. I’m especially interested in the ideas around converging regional- and country-level laws into standard compliance signals (“jurisdictional overlap”) that understand rights as overlapping and capable of being commonly represented. I think these are good principles. However, they do not seem to broadly inform the specification. 

The existing GDPR purposes are just added to by the CCPA purpose instead of specifying some sort of overlap or understanding of the CCPA’s opt out as a compounding of other signals or–more usefully–visa versa. In fact the generalized opt-out specified by the USP API is so much more useful because of its generalness it has become a way to specify privacy in other situations. It would be great to see a deeper exploration of the GPP principles in the GPP specification; especially when leveraging a concept like jurisdictional overlap could result in significant simplification. 


### A Note on UI

The GPP specification does not explore the user interfaces that might support it. In the case of a privacy tool that is irresponsible, especially considering the IAB is facing legal action over encouraging ineffective and misleading user experiences through TCF’s design. Without express guidance around UI, participants have to assume that systems will default to the TCF UI recommendations and patterns. These UIs are not as effective as they should be, are perpetually under challenge in courts and the loose rules around them allow the creation of outright anti-user designs. The GPP should not repeat the mistakes of TCF here and make clear specific user flows, especially where the API identifies interactions with specific screens as it extends from TCF. 


## Notes on Compliance Issues and GPP’s Relation to EU Court Findings 

GPP does not appear to address any of the standing objections by EU courts around TCF. In fact the specification makes it very clear that it is pulling from TCF wherever possible, repeating many of its mistakes. It is hard to see any entity getting behind adoption of GPP while the fundamental underlying assumptions of TCF which it replicates continue to be under threat of being declared illegal. 

It was my hope that GPP would represent a progression, a resolution of some of the problems TCF presents for compliance. 

It does not. 

GPP’s transmission of consent strings downstream still presents a fingerprinting risk through their complexity. GPP does not provide active enforcement mechanisms. The system does not do anything meaningful to assure that individual users’ choices are respected throughout the ecosystem. 

GPP’s continuation of vendor-level consents is overwhelmingly complex, unfair to users, and creates unnecessary technical complications. It also encourages difficult or bad user interfaces in order to handle compliance on top of GPP; ones that would seem to be only more complex than TCF. 

With the potential for endless expansion, both on-interface and on-string, is unbound and could grow infinitely over time. 

Considering the objections that TCF faces, an attempt to present GPP as an evolution of TCF that would address TCF’s problems–when it does not truely address those problems–is a threat to the continuing existence of Open RTB. The real time bidding ecosystem is desperately in need of an effective consent system. 

Without a reliable consent system RTB may be declared fully illegal by regulators, lawmakers or courts. GPP is not a reliable or effective consent system and pretending otherwise only puts the entire ecosystem at further risk. 


## Ways Forward

It is time to go back to the drawing board on the parts of GPP that replicate the flaws of TCF. 

GPP should consider enforcement mechanisms, real time hooks, active script control on the page, and active protection of users who do not consent to tracking. It is within GPP’s scope to build and standardize such systems. 

GPP should remove the concept of vendor-level consents. Expecting vendor-level consents is not consistent with user behavior and, while I previously had no data to back that assumption up, years of TCF shows vendor-level consent to be pointless. No significant number of users is going to go through even the smaller list of over one thousand ad tech entities and make specific consents for one of them outside of their choice for the other. That is even less likely should vendor lists expand to encompass more and more vendors, which is likely to happen as additional ad tech operations become relevant to privacy regulators. It’s time for the IAB Tech Lab to drop vendor-level consents. Anything less would give us an insufficient specification. 

The IAB’s work on the USPrivacy API should be taking the lead here: simple, human-readable, privacy signals. The IAB Tech Lab’s excellent work on understanding jurisdictional overlap can be used to support simpler, better and more straightforward privacy strings that operate along those lines.

---

Cover image is "portrait of a confused person at a computer" generated by [Midjourney](https://www.midjourney.com/app/)
