---
title: Topics API Review
date: 2022-08-04 13:00:00 -04:00
categories:
- web-standards
tags:
- ad-tech
- privacy
- Google
- Privacy Sandbox
vertical: Ad Tech
image: https://github.com/AramZS/aramzs.github.io/blob/master/_includes/people-being-categorized.png?raw=true
hashtag: TopicsAPI
excerpt: Taking a look at the Topics API as it stands today.
---

With the [Topics API](https://github.com/patcg-individual-drafts/topics) now in [origin tests](https://developer.chrome.com/en/docs/privacy-sandbox/topics-experiment/), it has been interesting to see just how the web gets categorized. I do see a lot of potential in the technology and I can’t argue with the privacy promise being a significant improvement over third party cookies. The biggest issue with Topics is how it will exist within the larger network of advertising technology entities and the market mechanics of the ecosystem. 

Topics might provide useful transitional technology to move off third party cookies and create privacy improvements, but the ad tech marketplace provides a clear history of such technologies becoming used in problematic ways: to enrich middlemen, confuse and mislead buyers, and disempower the site owners on which the associated ads would be run.


## Qualities of Concern

I make some assumptions in this assessment that may be less common among others examining Topics API.

1: **Topics will become the system of highest trust**. Trust between participants in the ad tech ecosystem is extremely low. At the same time, almost all participants are seeking the “surest thing” within ad tech. Or at least the capacity to represent themselves as providing the “surest thing” to buyers. This includes metrics, anti-fraud and, perhaps most of all, tracking. While other systems operate mostly on a closed basis and provide tracking and tagging of users through black box systems of decreasing (if ever successful) accuracy, Topics would provide a transparent system of user categorization, based on open source technology, created through insights generated though a browser’s full access into users’ history online. As buyers flock towards accuracy, Topics will–if released to all Chrome users–quickly become the most desired dimension of user tracking. _I therefore assume buyers will assign Topics high value._

2: **Inevitable Commoditization of Topics within Blackbox Systems**. Because Topics will become the most trusted property for defining users, Topics will quickly become integrated in multiple other systems where it will become mixed with other signals as part of a way to keep these systems’ proprietary user signals competitive with Topics. Pressure to activate Topics will become increasingly high as requests by buyers’ for this targeting are paired with 3rd party ad tech systems’ pressure to activate them as well. Ad tech intermediaries will consider the ability to collect Topics to be of high value, and the wider variety of Topics the better. _It is inevitable that the launch of Topics will be followed by the emergence of a market in closed-source Topics prediction and Shadow Topics that will become of high value because of the borrowed trust from the browser system._

3: **Sites will bend towards optimizing for Topics**. Because Topics will be of high value for ad pricing and ad tech intermediaries will consider access to a variety of Topics to be of high value, I believe that their entry into the ecosystem will inevitably push to alter the web publishing ecosystem back towards single-topic-per-domain sites with narrow focus. Small, focused sites that can acquire large audiences will find ecosystem-level advantages over large general-focus sites and gain high value CPMs through arbitrage. This is not the first time the advertising ecosystem has encouraged this exact change and it was not advantageous long-term in the past, not to mention: potentially misleading users, encouraging spammy sites, and forcing sites into configurations that will become extremely disadvantageous after third-party cookies are entirely eliminated. Some sites will debundle into networks of topically focused sites in order to acquire users with the particular Topics that mark them as high CPM opportunities. Only the general news sites that are already part of a large ranging network of smaller Topically-focused properties with which they share an internal ad tech domain will see the monetary benefits of Topics without altering their behavior. Other large general coverage sites will be forced to load a large variety of third party scripts to participate effectively in Topics and will lose any potential gains to ad tech tax, performance decreases, and arbitrage behavior. In any case _this will replicate and worsen the phenomenon of ad systems deforming the behavior of publishers._         


## Privilege of Large Scope Systems

I believe that the objections to FLoC on the basis of creating an even playing field for all systems that query the API were incorrect. If there is to be any access to these types of tracking terms, as decided by a browser, privileging that access to only those systems with the widest scope of domains on which they have a presence replicates, solidifies and may even worsen the worst behavior of the ad tech ecosystem. It will further discourage new entrants and competition while solidifying the status of current ad tech participants who run scripts across a wide range of domains. If large ad tech participants are the only participants to have broad access to Topics, the privacy risks are just as great, if not greater, because of their capacity to record a wide variety of user behavior. Solidifying the ecosystem around these participants also increases privacy risk as it empowers them to further attempt to breach users’ privacy using their preexisting massive tracking apparatus and capacity to join data with other systems through data purchases and corporate mergers. At the same time it lacks the capacity to keep such ad tech systems honest by giving other participants the capacity to check big systems’ Topics reporting with their own.

However, broad access to Topics gives an opportunity for smaller participants to act competitively on the open market and potentially refuse to participate with large ad tech systems that wish to mix Topics into proprietary black-box targeting. If, as I assume, Topics becomes the user property of highest value, then sites willing to transmit Topics in clear text will be able to avoid the market dynamics that pressure them to implement third party scripts, by making the highest value property available directly to the buyer. 

There has been some discussion of a large-scope publisher consortium to share and retransmit Topics, but this does not solve the problem of running such a script on non-publisher sites where users are likely to obtain valuable topics (like advertisers’ pages). Further, the costs involved in running such a system would seem to inevitably force it into replicating the exact undesirable models of behavior publishers would see from other participants, in order to compete and cover costs. 


## Large, Multi-topic, Reputable domains

Large general topic news and information sites will not contribute meaningfully to the generation of high-value user Topics. Considering that Topics will be considered high value and mixed into black box ad tech systems, a shadow market of Topics prediction will almost certainly arise and be given value. This market will generate Shadow Topics on the basis of particular domains seeing Topics commonly held by multiple users over multiple Topics generation epochs. This will mean that Shadow Topics will be more likely to appear within predictive ad tech systems (especially the blackbox systems that claim to pass along Topics, who can treat predicted and actual topics the same) on small topically-focused sites. The result will disadvantage large generally-focused sites from participating within the Shadow Topic ecosystem and disadvantage them in CPMs. It will also increase incentives for dishonest user categorization by ad tech ecosystem middlemen who maintain these Shadow Topic systems.  


## Arbitrage and “Drive to the Bottom” Pricing 

The per-domain classification process that Topics currently uses will generate significant incentives in user valuation towards driving users towards topically focused sites and therefore attaching Topics to them. This will further increase those sites that see common participation among users in high value topics incentive to participate in a Shadow Topic ecosystem which will reward them with high CPMs. This will replicate, worsen, and calcify the current system of ad arbitrage to the advantage of sites that can be spun up quickly, generate content that will focus users into specific Topics, send those users through a funnel of well-known Topic sites, buy a great deal of traffic, and then resell that traffic on their own site for high CPMs. This will drive CPMs down on reputable sites while encouraging the creation of low-quality but topically focused sites. It will also force large general-coverage sites to spend more money on arbitraging users with specific Topics, paying to have them come to the reputable site to sell ads against them and also to increase bids on the reputable site by training predictive systems systems to include high value Topics for a domain in that domain’s Shadow Topics. This is a cycle that already exists because of third party cookies and does not advantage users, buyers, legitimate operators of ad tech or the health of the web. If Topics replicates it as is and does not provide a way to curtail this cycle (which I cannot see it doing in its current format) then it is reinforcing one of the very negative outcomes of third party cookies I had hoped to see ended. 


## Ad Safety Risk

While the limited set of Topics is relatively unlikely to trigger negative targeting, it is easy to see a future expanded Topics set where a Topic will cause a user to be negatively targeted in a way that could be dangerous. Even among the current topic set there are risks. `243. News` could become a negative targeting vector for buyers who wish to spread misinformation. `140. Software` could become a positive targeting vector for crypto currency scams. While these are dangers intrinsic to any tagging system, including contextual, an inability to block specific Topics could leave a site vulnerable to malicious buyers who would pay higher sums for highly accurate Topics, while the pressure from good buyers will leave legitimate publishers with little choice but to participate. All user-based tracking presents this risk, but the inevitable buyer preference for Topics increases this pressure. 


## Sites who Cannot Exclude a Low Value Topic will be at a Disadvantage

Sites may find themselves commonly attracting users with low value Topics, or potentially seeing an attack by user agents who intentionally acquire low value Topics and go to the site in order to train ad tech middlemen running Shadow Topic systems to believe that the site attracts low-valued Topics traffic. These sites will find themselves having to choose between the pressure of buyers and buy-side systems who want Topics and turning it off entirely. This risks the entire Topics ecosystem as some high value sites may find it more advantageous to turn off the Topics system. Alternatively, sites may find themselves unable to withdraw from Topics due to market pressure and see their CPM values slowly drop with no clear solution. It is clear that individual domains should have the capability to have more nuanced options than Topics being active or inactive. Sites should have the capability to block any Topics-consumer operating on their domain from receiving specific Topic terms. 


## Privacy Promise 

Outside of the larger ecosystem impact I foresee Topics could have, user privacy here is well preserved. I have been impressed by the privacy improvements and believe that Topics presents a privacy improvement over both FLoC and third party cookies. Obviously some users will not want to be tracked at all, and others will continue to find the idea of being ‘followed’ by interest-based advertising unsettling. Topics is not perfect for privacy for these reasons and I’m sure for others that more focused privacy advocates may discover. Implied decisionmaking on the basis of Topics and their ability to contribute towards more indirect algorithmic redlining and discrimination is still a risk. However, I recognize that there is some privacy risk that has been determined to be desirable in exchange for the wider functioning and profitability of the web, especially in a time of transition. 

Additionally there will be periods of higher and lower risk for Topics use. It may be worthwhile for Chrome, or any implementer, to consider agreeing on block-out dates for Topics epochs. It would be wise to define sensitive periods where any additional user tracking has a higher risk of being used maliciously and the need for user privacy has an increased societal weight, like elections. 


## A High Risk of Reversal on Performance 

The past few years have seen an increasing focus on site performance, in part led by Google’s introduction of Core Web Vitals as a Search Optimization signal. Increased performance has benefited the users of the web and digital publishers. Because Topics assignments are only visible to those systems that are on the page when a Topic is assigned, it is likely to reverse the recent trend towards moving ad tech systems to small-script or no-script approaches that keep third parties' scripts off domains. Because of the high desirability of Topics and the high desirability of Topics-mixed products every ad tech system will want to have a script on-page and they will want to participate in as many domains as possible. This is not a desirable outcome for users or site performance. 


## Assessment:

At this time I do not find Topics a desirable proposal. While I have made some suggestions here that could lead to improvement, perhaps drastic, I believe that Topics’ capacity to impact the larger ad tech ecosystem in a negative way and to solidify some of the existing problems within that ecosystem, presents a high risk to the health of the web, even looking at Topics as a temporary measure. There was significant feedback on FLoC from privacy advocates around the question of access, but Topics particular approach to limiting access means that the pressures and mechanics of the ad tech ecosystem would damage improvements in privacy that Topics’ current construction around limiting access could create. If this system were to go forward it is more desirable that Topics be broadly accessible. Especially because doing otherwise will inevitably become a false privacy promise when ad tech systems will predict and trade in Topics information the same way they have with other user data. This type of access limitation is fundamentally not maintainable when the rest of the ad tech ecosystem comes into play, even if accuracy is lower. Privacy for users is further threatened by how Topics is likely to be rolled into the larger ecosystem. 

While this assessment is generally negative on Topics, it is not intended to be a discouraging one. Topics does show many interesting properties and I would like to see this style of browser mediation of advertising potentially built upon further in privacy-preserving ways. With the addition of more nuanced controls given to domain-owners/publishers, I see a potential compromise in the future of such systems. As long as users can make the choice of if they trust their browser with these operations, there is potential to create a smooth offramp from third party cookies towards better privacy across the web with these methods. 

---

Cover image is "people being categorized" generated by [Midjourney](https://www.midjourney.com/app/)
