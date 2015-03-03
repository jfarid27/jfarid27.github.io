---
layout : post
title  : Mastering Metrics by Angrist & Pischke
snip   : A small review on a book with big ideas
---

Data science is rife with tools and programs to apply well regarded algorithms to data.
Most practitioners at all levels appear to have a mix of computer science, statistics,
and mathematical knowledge to apply these tools with reasonable efficiency in their fields, 
which combined with their own industry knowledge, allows them to extract information out of their
data to solve their specific business problems. As more fields open their arms to wielders of
these tools, it will become even more important that these data centric individuals are aware of
limitations of the methods available to them and methods to determine when limitations
have been met.

[Mastering Metrics](http://www.amazon.com/Mastering-Metrics-Path-Cause-Effect/dp/0691152845) is a book
that caught my attention through [an episode of EconTalk](http://www.econtalk.org/archives/2014/12/joshua_angrist.html),
that sits directly in the space of introductory Causal Inference. Written by two well known econometricians,
the book gives insight into the art of using statistics to determine whether outcomes are affected by known
variables, and teaches readers that significance through regression is far from the only truth. Through
a walkthrough of the five most important tools used by econometricians to effectively determine how outcomes
are affected by variables, the readers can expect to have a reasonable knowledge of issues in using statistics
as the only known truth, and should easily be able to springboard into a course on regression or experiment design.

**Are all things truly equal?**

The first major concept that is shown is that direct comparison of groups through difference of means is
likely a path to the darkside. An easy example, shown in the book, is comparison of mean salary earnings of ivy
league graduates and non-ivy league graduates. A direct regression will give you a strong difference of means
between the two groups, but a researcher that infers an ivy league degree is attributed to the higher salary
is woefully incorrect. As with all data, *data is contaminated by selection bias*.

Could the higher salary of an ivy league graduate also be attributed to the skill levels of the students admitted
to the program? The answer of course is yes; in many ways success is a self-fullfilling prophecy for extremely bright
students, regardless of the institutions they attend. To truly measure the affect of the ivy league blessing, researchers
would hope enough equally similar students from the same backgrounds, race, income levels were all born on the same
exact day, going to the same high schools and receiving the same test scores, showing their ability levels are equal enough
to use for their study. Then simply send half to ivy league, and half to the other. From there, we could quite simply measure
the differences in means. If its positive, we can then gladly go on a marketing campaign for the winner of the test.
Sadly, one would be hard pressed to find a mother and father willing to have enough children to apease the researcher 
(50 should be enough right?), let alone hold their environments constant enough to allow them to all reach the exact 
same levels of abilities at exactly the same time. The problem, the lack of true comparability, is the main focus of causal
inference, and is problem faced by anyone who uses statistics to infer causality.

**Selection bias and exploiting Law of Large Numbers**

Mastering Metrics begins by diving directly into selection bias and defining its manifestation in means across separate
groups. Drilled into the reader in the initial pages is the concept of *ceteris paribus*, the notion that comparing variables
between two groups is only sensible in a world where all other variables are held constant. Yet researchers are limited in
their abilities to control all variables, since we cannot hope to be able to control all possible variables in an experiment.
Interestingly enough, a dualism appears through the Law of Large Numbers. Rather than control all variables, one can randomly
select individuals to apply a treatment to forcing the means of variables that are not of interest to be equal on average.
By doing so, the effect of these variables on outcome measures are minimized, allowing researchers to compare the differences
of means without signal from the effects of variables that are not of interest contaminating the difference. An understanding
of selection bias is key for people attempting to infer causal effects on outcomes. The introduction gives readers useful
introductory intuition on the theory, along with the first of the five major tools used by 'metricians.

**Controlling bias**

After the introduction to selection bias, the next chapters highlight the other effective tools for practitioners caught in a 
world where truly random trials cannot exist. Thorough discussion through a number of key research studies describes
how in many cases, random trials are difficult. Given a particular set of research constraints, bias introduction hinders the data in each study, removing the possibility of being able to compare groups in the context of all things equal. Through this, a tour of five main tools to combat the lack of true equality are shown: Regression with Control Variables, Instrumental
Variables and the 2 Stage Least Squares Regression, Regression Discontinuity, and Differences of Differences methods. The approach shows readers not only the how, but the why behind each particular method's application, and gives an added intuition behind what each regression does in accounting for bias. 

**But its only the beginning**

The presentation of the material makes it an excellent side read for anyone interested in using data to make decisions. Stressed throughout the text is an insistence to attempt to recognize biased data and remove it as efficiently as possible. This focus sets a baseline for assessing the quality of research, even in a world where truly unbiased data is unlikely. Econometricians straddle the line between policies and science, so critical research can have long lasting influence on policies in the real world. While a true statistical text won't discuss this, it is important to try to assess causal relationships using proper research designs. Otherwise, the data can lead us astray, even with strong statistical significance. This book is clearly a winner at giving readers an introduction to the techniques used in causal inference to give Econometricians the best chance to design strong research, but a look into how to identify broken designs. While it won't be a true regression textbook, readers interested in using data to make decisions will not only enjoy the tour of research design used in economics, but find these common designs parallel any field where data is used to make decisions.
