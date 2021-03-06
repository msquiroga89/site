---
title: A year of R
author: 'Macarena Quiroga'
date: '2021-07-25'
slug: a-year-of-r
categories: []
tags:
 - rstats
 - rstudio
 - education
 - community
subtitle: 'Seven things I have learned along the way'
summary: 'I downloaded R and RStudio on June 2020. A year later, these are my learnings.'
authors: []
lastmod: '2021-07-25T13:21:03-03:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: [ciencia-de-datos]
#draft: falses
---

The pandemic and its unprecedented length made all of us think *a year ago...* or *it's been a year since...* (it's been a year since I've been to my office, the last time I saw that person was a year ago, I haven't been on a bus for a year, etc). Together with the fact that my employment situation had also changed in March 2020, this first semester was plagued with a remembrance sensation that is more typical of the end of the year. But what caught my attention was that **a year ago I started learning R**. These are the things I've learned along the way.

#### 1. The R community is extremely beautiful.

I know this isn't news and that people say it all the time, but I just can't avoid saying it. For a person that had always wanted to learn technology in a self-taught way but thad had never been able to sustain it (or deepened in it), the first thing I have to say is that surrounding R and Rstudio there is a **social net** of mutual assistance that I had never seen elsewhere.

#### 2. The R community is organised around a clear goal: to teach how to use R as many people as possible.

Again: it seems obvious. But it's not. Even though nowadays you can find infinite resources on the internet about almost anything you want to learn on your own, those resources aren't always created from a teaching approach. I've read hundreds of CSS documentations pages and I still can't use flexbox properly. But that's the issue: most of those resources, at least the free ones, are documentation pages and not didactic materiales (with the obvious exception of [freeCodeCamp](https://www.freecodecamp.org/)). They are lists of functions, definitions and examples, but they are not tutoriales, teaching lessons, excercises with feedback.

My experience with R is just the opposite: from the moment I took a step in, I found a lot of material that was **intended for people like me**, who where starting from scratch and needed a **step-by-step teaching**, prioritized and pleasant topics. Of course this wasn't always the easy way: one month after I downloaded Rstudio, I read in Twitter or in a blogpost that I should start with the [R4DS book](https://r4ds.had.co.nz/) and, no ofense, that is a terrible piece of advise for someone that knows literaly 0% of R. It's a book intended for someone that knows, let's say, 1.5% of R, but not for someone that still doesn't know there is a difference between base R and the Tidyverse, or even for someone without a coding background. Luckily, I didn't withdraw from the learning path; I chose different paths and then I returned to that book when I had a more solid foundation.

Another beautiful example of how the community is actively trying to build didactic spaces is [\#TidyTuesday](https://www.tidytuesday.com/): a project explicitly dedicated to bring over real data to people, so they can practise their analysis and visualization skills. Even though I didn't participate a lot, my few contributions received 100% positive comments (one of those made me understand how to reorder factors, so I'll be forever thankful). \#TidyTuesday project is a key aspect for those that don't have own data or for those whose data isn't still ready to analyze or to share with others.

#### 3. The R community knows that, even though it's global, access to knowledge isn't homogeneous.

There are different R communities around the globe: [Rladies](https://rladies.org/), [LatinR](https://latin-r.com/), [MiR](https://mircommunity.com/), [RForTheRestOfUs](https://rfortherestofus.com/), to mention just a few. I think I wouldn't be where I am if it weren't for the Rladies: not only because of the warmth and commitment of their events and materials, but also because of the didactic point of view they gave to the task. Every time I need to understand something new, my first choice is always go to YouTube and type "rladies + " the topic. And I've always found something valuable.

The choice to organise chapters located in different cities arounf the world has a positive impact on the knowledge expansion, because the **idiomatic barrier is real**. Even if we use English in a more or less natural way, when we are in a very basic stage of the learning path, there is an extra effort added to the effort of learning a new tool. I had never understood how hard was this extra effor until a few weeks ago, when I took part of a tutorial in the [UseR!2021 Conference](https://user2021.r-project.org/) that was being imparted in Spanish: the confidence and safety I felt when asking questions in that context wasn't the same I felt before, in almost exclusively English-speaking spaces. In other words, even if I can ask questions in non-spanish context, those questions are stricly and thorougly checked before pronounced; this, inevitably, puts me in a constant state of alert that isn't always optimal to foster learning.

The fact that they are *ladies* is also relevant. I would love to say that there aren't **gender differences in technology**, but we all know that isn't true. It's not that the R community specifically contributes to that inequality, but there is something that exceeds it, that is that women in general tend to have to overperform to reach the same places that men. And this means that we aren't equaly welcomed, our erros and doubts have different connotations. Women learn quickly what it means to enter a male-dominated field, and that tension stays with us and mediates between us and our subject of study. The experience of learning in a non-male dominated group removes that tension. It's like driving a car: women have the responsability of driving in a perfect way, because if we do it wrong we risk collaborating to the stereotype that women drive improperly. And we don't want to drag our partners with that.

Okay. Let move on:

#### 4. You can do everything with R. Really, everything.

I started using R because I needed to conduct statistical analysis; I ended up using it to build presentations and websites. The **flexibility** of R and Rstudio is really challenging and I confess that more than once I asked myself if I could this or that daily chore with R (I still write down the grocery list in a piece of paper, though).

Sometimes I wonder if I really have to use Rstudio for some tasks, if it weren't easier to do them in some other way (like this website, for instance). But what I learned is that there are some tools that have to be learned from scratch; insted, the Rstudio integration allows me to **delegate** some tasks and focus on what I want to specifically learn. I'm sure that my slides would look better in PowerPoint, but if I want to improve the accessibility of my teaching materials I need to have control over some aspects that PowerPoint doesn't give me. The same thing happens with the website: if my goal is to keep an active site, to write, maybe I don't want to deal with HTML and CSS flexbox, but I also don't want to lose access to that flexibility by using a preassembled site. Building my site with Rstudio (more specifically with the [blogdown](https://bookdown.org/yihui/blogdown/) package and the [Hugo Academic](https://wowchemy.com/) configuration) allows me to easily sustain it, as well as to focus on learning (R)markdown and in the hierarchical organization of the information.

You can do everything with R, but just because of that...

#### 5. R can be very overwhelming sometimes. 

For someone like me, who had a very basic programming background, learning R wasn't just about learning R: it was also about increasing my rudimentary understanding of Git, about dealing with StackOverflow communication codes, about accepting that I couldn't learn everything at the same time. My biggest frustration of the moment is Shinny: even though I'm dying to learn how to create a decent Shiny App, truth is that it's best for me to focus on statistical analysis, my goal with R. When I get to know everything about statistics, then I'll be able to devote myself to Shiny, and that's a very realistic goal... right?

The *overwhelming* issue is a direct consequence of the issues mentioned early: with R you can to very different things, which increases the probability of finding a lot of documentation about one topic; on the other hand, because R is open software, the variety of way of doing one thing gets multiplied, which can be very confusing when someone is starting to learn. But, for me, what hinders my own personal learning process is something else:

#### 6. There is a big gap, in terms of availability of educational material, between a begginners level and a intermediate level.

*Disclaimer*: I don't consider myself to be in an intermediate-advanced level; I think I'm still in the middle of an intermediate level, but as I reach the second half of that level and I start to try advanced stuff, I find that all those beautiful tutorials and educational videos aren't that frequent. This makes that, when trying to learn about not-so-basic stuff, the feeling is once more the same that I had with previous programming languages I've tried to learn in the past. Of course this situation is nobody's fault, but it does seem to me the evidence of a bottleneck in terms of learning (and maybe a niche where to work to contribute to the community and return everything that has given to me). And I think that this gap could be related to the next topic:

#### 7. In some corners of the community, there is people that hates the Tidyverse. But, really really hates.

I never thought it could ever be possible, but it is. I mean, I understand why it happens: when I started to learn R, with the little programming background I had, I didn't understand you could program in R beyond the use of packages, but instead I thought that the packages were R. My first encounters with baseR were nothing less that with StackOverflow answers to questions similar to the ones I had, and during those weeks I really thought they were talking about something else: what the heck were those \$ signs, those square brackets in odd places?

As the weeks and months went by, I started to understand baseR logic (for which an applied statistics course I took helped a lot, the first course I took after ten months of self-taught), and what I noticed was that many things were made more easily, more concisely and with less code than with the Tidyverse. This is one of the Tidyverse-haters motives.

But what I would like to say to those *haters* is that I was able to understand some things of baseR *because* I had previously learned to do it in Tidyverse. Even though there are things that are actually easier with baseR, its own information conciseness with just a few symbols makes it so much **opaque** than the code one would use with the Tidyverse. Although it takes more code lines, Tidyverse functions are more transparent for those that -once again- don't have a programming background, and that's what makes the Tidyverse a **pleasant, friendly and inclusive environment**.

I don't belive that, as some may say, that there are people that can code without using one single baseR code line: I belive that the own path that people take leads them to requiere at least some of its elements. We must put aside the **ode to the difficulty**: I still struggle when I have to do a *for loop*, but I don't usually need them, why should I feel bad about it? Programming languages have some common topics with human languages (that's right up my alley): communities choose those aspects of the language that they need for communicating and for functioning as a society; linguistic change is an intrinsic part of that process. There is no better way of talking than another one; there isn't a programming way that is more pure than other. There are, in truth, good and bad programming practices, but that's related to the way of using the available resources, and not with the choice of those resources.

And, talking about loops, this issue takes me back to the first one: I don't know how was the R community before the Tidyverse explosion, but I do know how it is now: a warm, tremendously diverse community, that greets with open arms people with different journeys and different goals. I don't know if all, but some of those that hate the Tidyverse maybe can't see that is just that transparency that allows people like me, that didn't arrive to R from a programming background, from software engineer, maths nor statistics. Things don't have to be difficult to work: the idea of some *rite of passage*, in which everyone must first learn baseR to be considered worthy of being called R programmers, is a remarkably excluding idea, that doesn't correspond to the community's spirit.


#### What is waiting for me the next year?

I would like to write a new post on July 2020 telling that I learned Shiny, that I published a package or even that I filed an issue in Github. Chances are that for the first goal I would only have done one or two tutorials, for the second one I would only have an idea lost in some folder of my computer, and for the last one, no news. But it's fine: when I first downloaded RStudio on June 2020 I had no idea that I would reach this far. I have no doubts that the path will still be spectacular.
