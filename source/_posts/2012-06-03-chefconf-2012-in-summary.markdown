---
layout: post
title: "ChefConf 2012 in Summary"
date: 2012-06-03 21:07
comments: true
categories: 
---
This is a little late coming but figured I should post anyways. [ChefConf 2012] (http://chefconf.opscode.com/)
was an amazing event and absolutely surprising considering it's the first
conference [Opscode](http://www.opscode.com/) has put on. Here are a few things that I noticed:

### Culture

The attitude and culture around the people there was incredible. Everyone was
focused on the needs of the business that they worked for. Sometimes it meant
making developers more productive by being to provide consistent environments
or by lessening the pain operations have to go through in order to release
software created by development teams.

It inspired me to see so many people in the business to help others. There was
not a lot of ego, but there was definitely a sense of pride in the work that
many of the people did there.

### Demand

I was hoping to find some excited chefs out there that would love to work for
[ThoughtWorks](http://join.thoughtworks.com/) but it seemed everyone was doing the same. Attempts to recruit me
occured as I was trying to recruit them! This is definitely a hot part of the
software industry.

What made matters worse is that nearly everyone is extremely satisfied with
their jobs. Pretty hard to recruit people that are quite comfortable with their
positions and projects.

### Sessions of Note

Since I have a significant Windows background, I was really interested in the
two talks given by the folks from [Ancestry.com](http://www.ancestry.com/). The first one was a high level
summary of Ancenstry's path to Continuous Delivery. John Esser articulated the
principles well and was pleasantly surprised to see him promote ThoughtWorks
Studios' product Go

Next was a more technical discussion by 'INSERT NAME' which reminded me of all
the lessons I've learned in the Windows automation world. I had an excellent
chat with him and shared war stories that were all to familiar to him.

Adam Jacobs keynote was a good reminder that Chef is about providing us with
infrastructure primitives. As much as we like to standardize, the real world
isn't ever going to reach a global convergence. Every site is different and
they decided they didn't want to be the dictators on how you setup your
infrastructure. I think this is great because it allows Chef users to define
the opionated stacks that they require. It's a good seperation of concerns
in my opinion and a concept that I will try to pull into future projects.

'SO AND SO' from Lookout had an awesome slidedeck (hand drawn with paper and
crayola markers) that discussed Test Driven Development of cookbooks. I look
forward to trying out the concepts he discussed in my next project.

Lastly, CloudServe's 'SOME GUY' impressed everyone by discussing how they were
able to spin up $20 million dollars worth of infrastructure using AWS and only
paid $5k/hr for 3 hours use. Not only did the massive infrastructure speed
things up for them, it actually produced better results when performing protein
analysis. It begs the question of what other things are we missing because we
are yet to through large enough computing systems at them.

### Summary

The couple days were inspiring by I had to keep my energy in check because
I learned that certain things are not necessary for small projects with just
a handful of servers. I've been using chef-solo for all my machines because
the size of the environments I'm dealing with can easily be tracked in simpler
ways. I do look forward to the day when a chef server is necessary to deal
with all the infrastructure. That's where metrics like 1 engineer per 1000
machines is possible.


