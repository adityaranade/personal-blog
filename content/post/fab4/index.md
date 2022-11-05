---
title: Fabulous 4 of Indian Cricket: Comparing yearly batting averages
subtitle: A Bayesian hierarchical model to compare the yearly batting averages of the Indian test cricket team's fabulous four players from late 1990's and early 2000's. 

# Summary for listings and search engines
summary: A statistical analysis to compare the batting averages of the fabulous four players of Indian Test cricket team in the late 1990's and early 2000's. This analysis will help us answer some questions about who is the best among them.

# Link this post with a project
projects: []

# Date published
date: '2020-12-13T00:00:00Z'

# Date updated
lastmod: '2020-12-13T00:00:00Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/bY4cqxp7vos)'
  focal_point: ''
  placement: 5
  preview_only: false

authors:
  - admin

tags:
  - Academic

categories:
  - Cricket
---

Sachin Tendulkar, Rahul Dravid, Sourav Ganguly and VVS Laxman are usually dubbed the faboulous four of India cricket. In the late 1990's and early 2000's, these players were at their peak and were the backbone of Indian Test Cricket team from the batting perspective.


We will have a look at the batting average of each of the player on a yearly basis and try to understand which of the player has been a consistent performer. Sachin Tendulkar made his test cricket debut in 1989 whereas Rahul Dravid, Sourav Ganguly and VVS Laxman made their debuts in the year 1996. Sourav Ganguly was the first to retire in 2008 followed by Rahul Dravid, VVS Laxman both of whom retired in the year 2012 and lastly Sachin Tendulkar retired in the year 2013.


The career summary of the four players under consideration are as follows


| Player           	| Matches 	| Innings 	| Runs  	| Average 	|
|------------------	|-----------|-----------|---------|-----------|
| Sachin Tendulkar 	| 200     	| 329     	| 15921 	| 53.78   	|
| Rahul Dravid     	| 164     	| 286     	| 13288 	| 52.31   	|
| Sourav Ganguly   	| 113     	| 188     	| 7212  	| 41.02   	|
| VVS Laxman       	| 134     	| 225     	| 8781  	| 45.97   	|


Since all the players have played more that 100 matches (and more that 150 innings), we can compare the yearly batting averages for them. However, we will get a little adventurous and use a Bayesian approach to calculate the credible intervals for yearly average for each of the player.


In case you are wondering what a Bayesian method means, it is simply reconciling our belief (prior) with the data (likelihood) to obtain updated belief (posterior). And the credible interval gives us the plausible values for the yearly average based on the data we have. Along with the yearly average, we are incorporating the variation in the scoring as well which is nothing but considering how consistently or inconsistently the runs were scored.

We will incorporate another layer of uncertainty in the sense that we let the parameter at the first level have their own uncertainty and assign a distribution of their own. This is done through a Bayesian hierarchical model

The Bayesian Hierarchical model we will use for each player is as follows

{{< math >}}

$$Y_{i} \overset{\mathrm{i.i.d}}\sim N(\mu_{year[i]}, \sigma_{year[i]}^2)$$

$$\mu_{year} \overset{ind}{\sim} N(\theta,\tau^2)$$

$$\theta \sim N(\theta_{0}, \tau_{0}^2)$$

$$\tau \sim Uniform(10,100)$$

$$\sigma_{year} \sim Uniform(10,200)$$

{{< /math >}}

where $\mu_{0} = 50$ and $\tau_{0} = 10$ has been used which is consistent with each of the player's career average.

The model was run using a JAGS (Just Another Gibbs Sampler) which samples from the posterior distribution of the parameters. We will not go into much details about the individual parameters but use the parameters to come up with the credible intervals for the yearly average for all the players. We than combine the credible intervals for all the players into a single plot which can be found below.

{{< figure src="./fab4.png" caption="Credible intervals for yearly averages for each of the players"  numbered="true" >}}


We have the credible intervals for each of the four players from year 1989 to 2013. Year is indicated on the x axis and the horizontal lines corresponding to any of the year is the credible interval for yearly average. We use different colors to indicate which player the interval corresponds to. Purple colour corresponds to intervals for Sachin Tendulkar, red colour corresponds to intervals for Rahul Dravid, green colour corresponds to intervals for Sourav Ganguly and blue colour corresponds to intervals for VVS Laxman.

If the particular player has not played in a particular year, then there will not be a interval (horizontal line) corresponding to the player for that particular year. Since none of the players except Sachin Tendulkar was playing test cricket from 1989 to 1995, there is only one interval for those year. Similarly there is no interval for Sourav Ganguly (green colour) from 2009 upto 2013 since he retired in 2008. 


There are two characteristics which can be understood looking at any of the interval. The first is the width of interval which indicates how consistent the player was in any particular year. If the width of the interval is big, that indicates higher uncertainty about average for the particular player in that year. So we ideally want the interval to be as narrow as possible. 

The second is the location of the interval which indicates the average of the player for a particular year. If the average is higher, the location of the inteval will be towards the right and if the average is on the lower side the interval will lie towards the left side. Ideally we want a interval to be towards the right side.

Now that we have understood how to read the intervals, let us start comparing the intervals for players for different years. In professional sports, every player is bound to have some `good' years (narrow interval towards the right side) and 'bad' years (larger interval or interval towards the left side)




There are 2 particular thing which we should look at, namely how narrow (or wide) the interval is and the location of the interval (towards the right or left). 
