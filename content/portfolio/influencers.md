+++
date = "2016-11-05T19:41:01+05:30"
title = "Finding Instagram Influencers"
draft = false
image = "img/portfolio/influencer_graph.png"
showonlyimage = false
weight = 1
+++

Power-Middle influencers on Instagram are a more effective and authentic option for marketing niche products to targeted communities, but how do we find them?
<!--more-->

## tl;dr
> Power-Middle influencers on Instagram are a more effective and authentic option for marketing niche products to targeted communities. I created a methodology to select, construct, and analyze community networks within Instagram. Elite Power-Middle influencers were identified using social centrality measures and sentiment analysis of captions. Technologies used include Python, NetworkX, MongoDB, Selenium, and vaderSentiment.

## Introduction
Requesting promotion of a product from a celebrity with a large (millions) social media following is not just obscenely expensive - it is also obvious to followers that they have been solicited to sponsor certain brands or items, and therefore seems less authentic. To market to a smaller, targeted audience, it is more affordable and effective to identify a [“power-middle”](https://www.business2community.com/digital-marketing/power-middle-influencers-crushing-kim-kardashian-01515777#8OM20kRTpySksKoU.97) influencer. These power-middle influencers will be more influential to their intimate and loyal following they have amassed. If you are interested, check out some [examples](#examples) of power-middle influencers to get a better idea of who they are.

How do you find power-middle influencers who will be the most influential to the group of people you are trying to target? 



## Understanding and Preparing Data

Unfortunately there was no beautiful social-media dataset which would allow me to identify power-middle influencers, so I needed to collect the data myself. To do so, I narrowed the scope of the problem by choosing a community I wanted to target (take female climbers for instance). I then collected data on potential power-middle influencers by assuming people who posted content with a specific hashtag (#womenwhoclimb) were attempting to get their messages out into the universe. To estimate the rest of the community, I collected data about people who were influenced by the influencers -- therefore people who followed these potential power-middle influencers. I then amassed this data into an influencer-follower network. 

Turns out, that network was pretty big - 2,268,840 nodes and 3,582,464 edges! However, there were only 1775 unique potential influencers (out of 5000 scraped posts with #womenwhoclimb). The next step was to figure out who were the **elite** power-middle influencers.


## Modeling

### Assumptions about Elite Influencers:
To find the elite power-middle influencers, I made some assumptions about their Instagram qualities.

- They have a **critical mass** following so that *enough* people will view their content.
- They **interact** with their community so followers are more likely to like or comment on their posts.
- They **influence** a distinct community, therefore they are not just a celebrity with millions of random followers.
- They post **authentic** content and are not obviously marketing in an insincere way.

### Modeling to Identify Elite Influencers:
#### Critical Mass Filter: 
I filtered for influencers who had more than 5000 followers, assuming 5000 followers is *enough* for someone to be classified as a power-middle influencer.

#### Interaction Score:
The interaction score is equal to the ratio of likes to followers.

#### Influence Score:
The influence score is equal to eigenvector centrality -- a higher score is given to influencers who are connected to other key members of the community. This also prevents celebrities from rising on the scoreboard because they are connected to many random followers (higher degree centrality) instead of other key members from a very specific community (higher eigenvector centrality).

![Influence Score: Degree Centrality v. Eigenvector Centrality][2]

#### Authenticity Score: 
The authenticity score is inversely proportional to the positive sentiment in their captions, assuming that marketing text is often overly positive and followers are more likely to trust influencers that are more candid.

![Authenticity Score][3]

#### Overall Score:
Those scores were weighted and summed to determine and overall score. The top power-middle influencer is [Pamela Shanti Pack](https://www.instagram.com/shantipack/), a professional female rock climber. 

![Overall Score][1]

## Evaluation
To evaluate the performance of this unsupervised learning approach, I:

> Determined if top influencers were already endorsing products, meaning that industry experts had deemed them to be influencers already.

> Checked if top influencers on the leaderboard shave posts which show up in the "top results" of the search page for the #womenwhoclimb hashtag, which shows trending content.

Turns out, every person on the leaderboard was already sponsored in some fashion, and they all appeared in the "top results" section at least once over the span of this two-week project. 

## Conclusions and Future Work
The data pipeline for identifying power-middle influencers on Instagram yielded some promising first-cut results! Network analysis is a powerful way to analyze social media interactions and can be useful for niche marketing campaigns. 

The next steps for this project include expanding the interaction score to include comment-response interactions and averaging an authenticity score for all captions instead of only the caption for post with the specific hashtag. I would also like to create a scoring methodology for micro-influencers.

## Want to see more?
Check out the [code](https://github.com/sdmirch/instagram-influencer-graph) that made this project a reality.

## Examples {#examples}
Take a look at some examples of power-middle influencers:

* [briannamadia](https://www.instagram.com/briannamadia/)
* [negharfonooni](https://www.instagram.com/negharfonooni/)
* [brokenpinestudio](https://www.instagram.com/brokenpinestudio/)


[1]: /img/portfolio/OverallScore.png
[2]: /img/portfolio/InfluenceScore.png
[3]: /img/portfolio/AuthenticityScore.png