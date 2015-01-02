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
that sits directly in the space of introductory Causal Inference. Written by two well known Economatricians,
the book gives insight into the art of using statistics to determine whether outcomes are affected by known
variables, and teaches readers that significance through regression is far from the only truth. Through
a walkthrough of the five most important tools used by economatricians to effectively determine how outcomes
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
same levels of abilities at exactly the same time. This is problem faced by anyone who uses statistics to infer causality.

**Selection bias and exploiting Central Limit Theorem**


