---
layout: post
title:  "Why We Need to Stop Redefining ‘AI’"
date:   2018-05-02 18:25:00 +0900
categories: ai machine-learning
---
John McCarthy coined the term 'Artificial Intelligence' in the *Dartmouth Summer Research Project* on Artificial Intelligence back in 1956. Ever since then, it has always been just out of reach of the technology of the time. Indeed, the original proposal for the Dartmouth Workshop said that:

> "The study is to proceed on the basis of the conjecture that every aspect of learning or any other feature of intelligence can in principle be so precisely described that a machine can be made to simulate it."

At the time it there were a few milestones which would define having 'achieved' AI. There was, of course, the infamous Turing Test (I'll come back to that later). But there were also others such as beating humans at chess, understanding language, and image recognition. In my mind, these are acceptable measures of intelligence in machines. Before modern computers, these things were the domain of humans (or 'intelligent beings'). They only seem ordinary to us now because they are commonplace in our lives.

Games of Skill
==============

The first of these tests to drop was beating top-level humans at games of skill (such as chess). Arthur Samuel wrote a Checkers program that, by 1970, could beat a high-level amateur human. Then, in 1996 Deep Blue beat Kasparov (the reigning world champion of the time) at chess. At this point one would think, "We must have achieved artificial intelligence, if only in the domain of logical games". But there were plenty of people saying, "No, these are mere brute computation games. Computers still aren't competitive in games that need *intelligence*." The chief game pointed at was usually Go, which has too many potential moves per turn to brute force with computation power.

But, in 2015 AlphaGo beat Lee Sedol (one of the top ranked players in the world) in Go. It used an approximation of the low-level functions of the human brain (which we know as a *neural network*) to intelligently pick only the most promising moves to evaluate.

The thing is, if you do a quick search on the internet for "AlphaGo is not AI" you will find hundreds of articles on why we still haven't achieved Artificial Intelligence. The main theme being that we haven't achieved what we call Artificial General Intelligence.

Artificial General Intelligence
===============================
AGI (also called 'Strong-AI') is a system that takes input from its environment and uses that input to achieve some goal in an intelligent way. The key being that it doesn't follow some pre-programmed pattern, but uses reasoning and intuition like ours in pursuit of its goal. On some fronts we're very close to achieving this (building a world-model from sensor inputs and using that data to achieve short term goals) but there are other areas in which we have a long way to go (long term planning, logical reasoning, high dimensional output spaces).

Building an AGI is a very good goal to have, a strong one would that didn't need too many computational resources would solve a lot of problems in the world today. However,  this is where my gripe with the AI naysayers lies: AGI is not *true* AI. 'Intelligent' game AIs that intuitively evaluate moves are not *true* AI. AI is a system that exhibits intelligence artificially.

This needn't even be human level intelligence, a machine that does its best but still loses to the average 10 year old at noughts-and-crosses is still (a very bad) AI because it is a machine that contains some form of intelligence. Even proponents of AGI being the only true AI would have to agree that a machine that behaves like a monkey is an AGI despite the fact that it is far below human level in every mental faculty. It would exhibit tool use, long-term planning, self-preservation, drive to complete its goal (procreation), etc.

Once we achieve AGI, the people saying that AGI is the only true AI will move on to the next thing. It may be consciousness, saying that they are only machines and thus not *really* intelligent. It may be something else. But there will be something that makes them say that we still haven't achieved AI. This is because to them, AI is something magical, and once something becomes commonplace it ceases to be magical.

As Larry Tesler said:
> "AI is whatever hasn't been done yet".

The Turing Test
===============

Now, the people saying we haven't achieved AI do have one very good point. It is more or less accepted that we haven't beat the Turing Test, Alan Turing's original measure of whether a machine was 'intelligent' or not. Leaving out whether it actually is a good measure of intelligence (I can name a few *people* that might not pass the turing test), I would like to present some anecdotal evidence that we built machines that can pass it a while back. The biggest milestone in artificial intelligence may have coasted past us with very little fanfare.

Cleverbot is a chatbot from the mid to late 2000s. It works by storing a huge database of conversations it has had with humans and using fuzzy logic to consult that database and find appropriate responses to questions or statements directed at it. Around that same time Omegle, a website that pairs you up with a random stranger to talk, was also becoming popular. Someone wrote a Java applet that hooked the two up together and let a random stranger talk with Cleverbot (without telling them, of course). I had fun with this for a few days, and interestingly, only a *very* small percentage (a 4-5 out of about 100 conversations) of people caught on that they were talking to a machine.

Most interesting was one girl who talked with Cleverbot for 10 hours! During that time she had a few inklings that she was talking to a robot, but when she explicitly tested her suspicions (repeating the same statement multiple times, fact-checking things it said earlier, etc.) it repeatedly passed her tests. To me, this is the best example of how we have beat the Turing Test I have ever seen.

One last thing to note is that Indian Institute of Technology Guwahati performed a formal turing test using Cleverbot in 2011. 59.3% of people rated it as human (compared to 63.3% for actual humans).

Why We Need to Stop Redefining 'AI'
===================================

So, I've talked a lot about how we've achieved AI, but why is it so important that we accept that? The answer is that it is directing our focus in this field too narrowly. Michael I. Jordan's article *Artificial Intelligence --- The Revolution Hasn't Happened Yet* takes the stance of AGI being the only true AI, but he arrives at the same conclusion to me. By defining AI so narrowly (he dislikes it being defined as human imitative machines) we are ignoring a huge swathe of incredibly important fields. We are setting our sights very firmly on AGI (which is a brilliant goal, don't get me wrong) to the point of making any advances in areas that don't lead directly to AGI less prestigious.

For an example, just look at the top papers at any conference. Any paper linked with AGI is virtually guaranteed its place on the front page of Reddit's /r/machinelearning, as well as a nice spot at a conference. Take *Neural Architecture Search with Reinforcement Learning* from Barret Zoph and Quoc Le for example. While a very well written paper with good technical explanations of their process, it achieves very little. It used an incremental improvement on previous techniques to match the state of the art, yet got an oral presentation at ICLR 2017.

It got that because neural networks building other neural networks is an awful lot like a self-improving machine, which is an iconic part of an AGI. Meanwhile, papers that advance the field more but not in a way that is directly linked to AGI such as *Knowledge Adaption: Teaching to Adapt* by Sebastian Ruder, Parsa Ghaffari, and John G. Breslin, which made a great contribution to the field of domain adaptation, get rejected.
