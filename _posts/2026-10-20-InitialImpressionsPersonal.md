---
layout: single
title: "Initial impressions - Personal experiences"
date: 2026-10-20 11:42:00 +0200
tags:
  - Initial-Impressions
author: alexander
---
**Author:** {{ site.data.authors[page.author].name }}


I first heard about the question whether spectral information determines almost all graphs in a talk by Aida Abiad in 2022. She mentioned this as one of the notable open problems in spectral graph theory. The problem indeed has a rich history in the Netherlands, where I was a PhD student at the time, with notable contributions coming from Dutch mathematicians like Brouwer, Seidel, Van Dam, Haemers, and ofcourse Aida Abiad herself.  

I was working in random matrix theory, and it seemed to me that my subject could potentially give a fresh perspective. The problem had previously mainly been investigated by people in combinatorics. Thankfully, my supervisor, Jaron Sanders gave me the freedom to explore some of these connections independently. I continue to be thankful to him for this freedom, as it has turned out to be a deeply rewarding problem.  

The precise variety of random matrix theory that later turned out to be relevant was actually not at all obvious. I initially pursued some ways to try to combine classical ideas in random matrix theory with discreteness constraints from graphs. (For instance, to combine that eigenvalues of random matrices behave approximately like a determinantal point process with the fact that the coefficients of a graph's characteristic polynomials are integers). The first few ideas however went nowhere. 

What ultimately turned out to be relevant was the combination of arithmetic sufficient conditions developed by Wei Wang with a relatively recent abstract-algebraic branch of random matrix theory. Specifically, groups and modules associated to random integer matrices turn out to relate to the problem in a nontrivial way; see the next post. I discovered this connection rather fortuitously while researching literature for my initial approach, and this ended up being the subject of my first single-author paper in [2024](https://arxiv.org/abs/2401.12655). 

Since then, especially since starting my postdoc in Münster, I have been working on a research program that further develops the connection between random matrices and cospectrality. One of my concrete median-term goals was to prove that almost all graphs are determined by their generalized spectrum. While steady progress was being made in collaboration with Nikita, we expected a rigorous proof to still be quite a while away, as there continued to be a number of challenging technical problems that had to be addressed. 

 When I saw the title of the preprint [''Almost all graphs are determined by their generalized spectrum''](https://arxiv.org/abs/2610.11047) appear in my morning scroll of the arXiv feed, my initial reaction was correspondingly disbelief.  Was it really possible that a Large Language Model (LLM) solved this problem autonomously?  

Upon opening the preprint, my disbelief was significantly reduced. A high-level inspection of the 96-page manuscript showed that the general strategy was closely related to the approach that Nikita and I had outlined in some of our recent joint works. Given that I strongly believed that our approach was the "correct" perspective on the question, this reflected favorably on the plausibility of the LLM-generated manuscript.

Another aspect that positively reflected on the manuscript's plausibility is that I knew the author, Ziqing, from a previous (human-written) preprint ["Natural graph spectra" (2026)](https://arxiv.org/abs/2602.00936) that I liked. Although the techniques in that previous work differ significantly from what was necessary here, this at least meant that there was a human author with interests in the problem. This is not guaranteed in these modern times.

By noon, I had accepted the new reality and decided that I wanted to understand what ideas specifically were used. I hence sent a mail to Ziqing to ask whether he would be available for a Zoom call.  He agreed, but warned me that he may not be able to tell me much, since the LLM did the analysis completely autonomously.  

Actually, the Zoom chat was quite interesting! Ziqing explained the algebraic structures that the LLM had generated for the deterministic parts of the proofs. As I will in later posts, these structures are related to ideas that Nikita and I had been developing, but are different in some ways. Moreover, they suggest some beautiful underlying theory. 

The majority of the manuscript however concerns probabilistic results. Ziqing noted that he could not explain this part, as he had only read the combinatorial-algebraic part but not yet the remainder. There is presently hence not a single human who has digested the complete manuscript. 

As I mentioned earlier, Nikita and I had expected that that this result was still going to take a while (assuming human speeds) as there were technical bottlenecks that we had not yet resolved. For example, one of these bottlenecks relates to the _large prime problems_. My initial reading of the manuscript suggests that the approach in the preprint overcame, or rather had a method to circumvent, some of these bottlenecks. 

So, the manuscript does appear to include some interesting ideas. Moreover, some of these ideas lead to underlying beautiful theory! At any rate, it is clear that the LLM sped up the process. In fact, it may have been a bit _too_ fast. The value of the resolution of a fundamental problem comes from its appreciation by humans, but this requires more time. This issue is made worse by the fact that LLM-generated exposition is currently rather tedious.

The desire to understand and digest the new ideas as humans led to the formation of this work group. While I do grieve the loss of the opportunity to uncover the new ideas a slow organic way, there will also be some joy to be had in learning them. Moreover, organizing ideas into the clearest form possible will likely also offer a rewarding and challenging problem.  I am curious to see how my experience of the process will be in practice. 
