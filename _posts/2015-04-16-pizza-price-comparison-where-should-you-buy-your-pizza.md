---
layout: post
title: Pizza Price Comparison - Where Should You Buy Your Pizza?
date: 2015-04-16 18:22:34.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- data
- money
tags:
- data
- pandas
- pizza
- price comparison
- visualisation
author:
  display_name: deparkes
permalink: "/2015/04/16/pizza-price-comparison-where-should-you-buy-your-pizza/"
---
<h1>Pizza Price Comparison - Where Should You Buy Your Pizza?</h1>
Not sure where to buy a pizza from for yourself or a group? Want to make sure you get the best value for money?
Use this <strong>pizza price comparison</strong> to help you decide.

<h2>Price vs Diameter - Pay More, Get More</h2>

Firstly let's take a look at how the pricing scales with pizza diameter - the number you look to when deciding how big a pizza you want.


| ![pizza price comparison - price vs diameter]({{site.baseurl}}/assets/2015/04/PriceVsDiameter-1024x632.png) |
|:--:|
| *pizza price comparison - price vs diameter* |

Not surprisingly the more pizza you get, the more you have to pay.

But more interestingly there are two clear groupings: the large chains vs the local takeaways.
The local places occupy more or less the same price points, with a pretty much linear scaling with price.
For the chain takeaways, whilst there is competition over the middle ground, the two chains seem to have gone for different strategies: Domino's offers a smaller 'personal' pizza while Papa John's sell a much larger XXL pizza. I wonder if this was a deliberate plan to try to offer something different to customers. As with the local takeaways, the price scaling is more or less linear.
Interesting, too, is that the two sit-down pizza restaurants listed generally occupy the middle ground of price between the local and the chain takeaways. Also evident is that the sit-down restaurants offer far fewer size options compared to the takeaways.
<h4><a href="https://gist.github.com/deparkes/cb23499ffa4226ac8ee6">Download data and plotting code</a></h4>
<h2>Price per Square Inch vs Diameter</h2>
Price is one thing, but often what we really care about is value for money - <strong>how much pizza do we get for our cash?</strong>

| ![Pizza price comparison - price per square inch]({{site.baseurl}}/assets/2015/04/PPSQ_Vs_Diameter-1024x622.png) |
|:--:|
| *Pizza price comparison - price per square inch* |

This graph is even more revealing than the first. Straight away we can see the obvious trend that generally speaking the more pizza you buy, the better value for money it is.
What is suprising though is that the Domino's tiny 'personal' pizza is actually relatively good value for money for its size. The Papa John's XXL pizza on the other hand scales relatively badly compared to the other more moderately sized pizzas sold by both Domino's and Papa John's.
Another point to note is that there is very little difference in value for money between the restaurant pizzas - buying more doesn't get you a much better deal. In fact at pizza hut, you seem to be getting slightly worse value for money when you buy a larger pizza.
<h2>Conclusion</h2>
To some extent we don't really know much more than we did before plotting the data: expensive places cost more and generally getting a larger pizza is better value for money.
But what we can say is:
<ul>
<li>Local takeaways have consistent, low price scaling</li>
<li>It doesn't always make that much more sense to get a larger pizza at a chain takeaway</li>
<li>If you really want to save money - go to the super market</li>
</ul>
<h1 class="attribution-info">The establishments:</h1>
<div class="attribution-info">
To check were the best value for money lies, we're comparing a selection of restaurants, local takeaways, as well as a supermarket:
Sit-down restaurants: <a href="http://www.pizzaexpress.com/">Pizza Express</a>, <a href="http://www.pizzahut.co.uk/">Pizza Hut</a>
Local Nottingham restaurants: <a href="http://www.just-eat.co.uk/restaurants-dinos/menu">Dino's Takeaway</a>, <a href="http://www.amigospizza-ng7.co.uk/">Amigo's Pizza</a>,  <a href="http://www.just-eat.co.uk/restaurants-luigis-ng9/menu">Luigi's Takeaway</a>.
Takeaway Chains: <a href="http://www.papajohns.co.uk/">Papa John's</a>, <a href="https://www.dominos.co.uk/">Domino's.</a>
Supermarket (as a base line): <a href="http://www.sainsburys.co.uk/sol/index.jsp">Sainsbury's</a>
</div>
<div class="attribution-info"></div>
<div class="attribution-info">
<strong>A note on the prices:</strong> the prices listed are for a standard 'margarita' <a href="http://en.wikipedia.org/wiki/Pizza">pizza </a>as listed on the websites of the different restaurants in December 2014. No attempt is made to account for any special offers or deals, or variation in quality or convenience of the different restaurants - you'll have to factor that in for yourself.</div>
<div class="attribution-info"></div>
<div class="attribution-info"><a class="owner-name truncate" title="Go to Matt Harris's photostream" href="https://www.flickr.com/photos/ecos/" data-rapid_p="24" data-track="attributionNameClick">Image: Matt Harris ; Some rights reserved
</a></div>
