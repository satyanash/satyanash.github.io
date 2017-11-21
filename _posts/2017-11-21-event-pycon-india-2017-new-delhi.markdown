---
layout: post
title: "[Event] PyCon India 2017 - New Delhi"
date: 2017-11-21T23:10:05+05:30
tags: events
---

This was my third PyCon India, the first two being PyCon India 2015 and 2016.
Unlike the last two times, I had planned better and had a full day before and after the conference to spend in New Delhi and check things out.

![PyCon India 2017 - New Delhi](/img/pycon_india_2017_billboard_5.png 'PyCon India 2017 - New Delhi')

I really wanted to understand _how_ the community worked and made sure I talked to as much people as possible.
I'd already subscribed to the pydelhi, bangpypers and #dgplug mailing lists so I had a general idea of what was going on and who was who.
It was also a good thing that the conference had set aside two days specifically for the dev sprints.
Last year, the dev sprints were held in parallel to the talks and I wasn't able to decide between what I wanted to attend.

Since this a long blog post, following is a table of contents:

* [2nd Nov 2017 - Day 1](#day1)
* [3rd Nov 2017 - Day 2](#day2)
* [4th Nov 2017 - Day 3](#day3)
    1. [Mentoring: What, Why, How - Noufal Ibrahim](#keynote1)
    1. [Visualizing machine learning algorithms in Python - Anand S](#viz-ml)
    1. [Liberating tabular data from the clutches of PDFs - jayant](#liberate-pdf)
    1. [Panel Discussion on 'Where Python Fails'](#panel1)
    1. [Lightning Talks](#lightning1)
    1. [Building single page javascript apps with Django, Graphql, Relay and React! - Nicolas Romero](#building-spa)
    1. [Self-Healing Code: A Journey Through Auto-Remediation - Arun Singh](#self-healing-code)
    1. [Keynote - Python Community Principles by Elizabeth Ferrao](#keynote2)
    1. [After Events](#day3-after-events)
* [5th Nov 2017 - Day 4](#day4)
    1. [Keynote - Python and Data: Past, Present and Future by Peter Wang](#keynote3)
    1. [Spinning local DNS server sourcing responses over HTTPS to combat Man-in-the-middle attack - Arnav Kumar](#dns-over-http)
    1. [How import works in Python - Sasidhar Donaparthi](#how-import-works)
    1. [Panel Discussion on Women in Open Source](#panel2)
    1. [Django on Steroids - Building Applications at Web Scale - Sanket Sourav](#django-steroids)
    1. [Clean Architecture Applications in Python - Subhash Bhushan](#clean-arch)
* [After Effects](#after-effects)
* [1st Nov 2017 - Day 0 (Appendix)](#day0)


## 2nd Nov 2017 - Day 1
{: #day1}

This was the first day of the two day dev sprints that I wanted to attend.
It took me about one and a half hour by metro to _Shaheed Sukhdev College of Business Studies_ in Delhi University.
I'd miscalculated the location a bit and ended up reaching around 20 mins late.
Once I got there, I found out that they'd run out of dev sprint registrations :(.

I still wanted to get in, so I bought a workshop ticket on _Introduction to Concurrency in Python_.
The workshop was conducted by [Anand](https://github.com/pythonhacker) [Pillai](https://twitter.com/skeptichacker), who I was already following on Twitter and knew to be a cool Pythonista.
The workshop was already ten minutes in when I entered, but I already had a general idea of what was being covered.

Anand covered quite a lot of interesting ideas and had (in his own words) overprepared for the workshop.
The demos for matrix multiplication and maze solvers served as excellent examples of embarrassingly parallel problems that could benefit from Python's `multiprocessing` module.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Fantastic morning session with <a href="https://twitter.com/skeptichacker?ref_src=twsrc%5Etfw">@skeptichacker</a> on parallel programming in Python <a href="https://twitter.com/hashtag/PyConIndia?src=hash&amp;ref_src=twsrc%5Etfw">#PyConIndia</a> <a href="https://t.co/usJSpR5Pmm">pic.twitter.com/usJSpR5Pmm</a></p>&mdash; nonbeing (@anattaguy) <a href="https://twitter.com/anattaguy/status/926006291016900610?ref_src=twsrc%5Etfw">November 2, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

There were also a couple interesting questions from the audience about how one could restrict the `multiprocessing` library to use only a couple cores instead of dedicating all the cores in a given machine.
Anand acknowledged that he'd never tried it, but then theorized that reducing the pool size to the desired number should do the trick.
And lo, doing just that worked beautifully and we could see just two cores hitting 100% parallel usage in the system monitor visualization.
I'll admit that I could stare at the CPU usage monitor for hours as it charts the usage for my system under varying loads.

Once the workshop was over, the lunch counters were opened and I met a few of the cool friends I had made at Science Hack Day India 2017 in Belgaum just a month ago and PyCon India 2016. This included:
* Akshay Shirpurkar [@AkkiShipurkar](https://twitter.com/AkkiShipurkar)
* Amol Kahat [@AmolKahat](https://www.twitter.com/AmolKahat)
* Jaidev Deshpande [@jaidevd](https://www.twitter.com/jaidevd)
* Saptak Sengupta [@saptak013](https://www.twitter.com/saptak013)
* Sayan Chowdhary [@yudocaa](https://www.twitter.com/yudocaa)
* Suraj Deshmukh [@surajd\_](https://www.twitter.com/surajd_)
* Vaishali Thakkar [@kernel\_girl](https://www.twitter.com/kernel_girl)

The #dgplug connection should already be evident.
I had taken it upon myself to find out more about this community the last time I met these people, but had conveniently forgotten about it once I left Belgaum.
I plan on not repeating the mistake this time.

I was also introduced to other folk who I met for the first time:

* Himanshu Awasthi [@IHackPY](https://www.twitter.com/IHackPY)
* Jaysinh Shukla [@Jaysinhp](https://www.twitter.com/Jaysinhp)
* Sanyam Khurana [@ErSanyamKhurana](https://www.twitter.com/ErSanyamKhurana)
* Shivam Singhal [@championshuttler](https://github.com/championshuttler)
* Priyank Trivedi [@priyankt68](https://github.com/priyankt68)

Following Lunch, I decided to check out the dev sprints and made my way to the seventh floor of the building.
I could see all the mattresses that were laid out and I people spread out over them burried into their laptops.

I found a place for myself and opened up [the etherpad](https://etherpad.wikimedia.org/p/dev_sprint_pycon_india_2017) that was used for keeping track of the devsprints and pull requests that people were working on.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Devsprints enthusiasts at pycon. Came for the language, stayed for the community. <a href="https://twitter.com/pyconindia?ref_src=twsrc%5Etfw">@pyconindia</a> <a href="https://twitter.com/hashtag/PyConIndia?src=hash&amp;ref_src=twsrc%5Etfw">#PyConIndia</a> <a href="https://twitter.com/hashtag/pycon2017?src=hash&amp;ref_src=twsrc%5Etfw">#pycon2017</a> <a href="https://t.co/EQe04l2Ad0">pic.twitter.com/EQe04l2Ad0</a></p>&mdash; Pritesh Srivastava (@anshu686) <a href="https://twitter.com/anshu686/status/926340633450618880?ref_src=twsrc%5Etfw">November 3, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

One of the projects was the task of converting a book from PDF to markdown so that it could be hosted on GitHub and easily disseminated.
The book was titled [_Internals of CPython_](https://intopython.com/) by [Prashanth Raghu](https://www.twitter.com/PrashanthRaghu).
By the time I reached, almost all the chapters had been already claimed and conversion was already under way.
I perused through the book and decided to bookmark it for later reading/experimenting.

So I kept looking at other projects and I found out about [Bhavin](https://github.com/bhavin192) and his project called [review-board](https://github.com/geeksocket/review-board).
I also checked out his blog called <https://geeksocket.in> which was very well written.

Then I mostly hung around the place and began reading about Clojurescript.
I'd been wanting to try it out for a while and decided that this was a good time.

After that in the evening, all the PyDelhi and #dgplug people had begun assembling in one place and wanted to go somewhere together for a dinner or something.
I decided to tag along so that I could soak up all the wisdom that was probably flowing from the group.

We ended up at a Domino's in a nearby mall and I managed to get a place at a table with a few guys from RedHat: [Zeeshan Ahmed](https://www.twitter.com/zee_10000), [Suraj Deshmukh](https://www.twitter.com/surajd_) and [Suraj Narwade](https://www.twitter.com/red_suraj).
We had some interesting discussions on what containers were and Suraj explained how Docker was essentially a layer around linux system calls to create certain namespaces for process isolation.
He also talked about the current state of the Kubernetes support for container providers and how it is being standardized with a unified API.

Once dinner was over, we split up and Day 1 had ended.

------

## 3rd Nov 2017 - Day 2
{: #day2}

This was the second day of the dev sprints and I managed to reach much earlier than the day before.
I also secured a place in the _first come, first served_ devsprints list and proceeded straight to the seventh floor.

I went and went through the github repositories of all the new projects that were added on the etherpad.
One project that caught my eye was [Junction](https://github.com/pythonindia/junction), which was a Django web application being used to manage the CFP process for the PyCon India conference.
The dev sprint was being led by [Krace Kumar](https://github.com/kracekumar) who was also one of the maintainers for the project.

The first half of the day was spent getting to know the project's functionality and the codebase.
I also got the project running on my local machine and familiarized myself with the models.
While looking for open issues, I helped bring attention to a few which were already resolved but weren't marked as such.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Because food is important <a href="https://twitter.com/hashtag/pyconindia?src=hash&amp;ref_src=twsrc%5Etfw">#pyconindia</a> <a href="https://twitter.com/hashtag/pyconindia2017?src=hash&amp;ref_src=twsrc%5Etfw">#pyconindia2017</a> <a href="https://twitter.com/pyconindia?ref_src=twsrc%5Etfw">@pyconindia</a> <a href="https://t.co/zKuifytD8S">pic.twitter.com/zKuifytD8S</a></p>&mdash; Sayani Bhattacharjee (@sayani0_0) <a href="https://twitter.com/sayani0_0/status/926743034653315072?ref_src=twsrc%5Etfw">November 4, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Met a few more people during lunch and just then found out that a volunteers meeting was called.
I had always wanted to volunteer ever since I found out about the first PyCon but never got the chance to do so.
Taking up on the offer I proceeded to the mentioned room where we were briefed of all areas the managing team needed volunteers for.
I chose to volunteer for mic handling during the QA sessions in the main auditorium.
The track lead for the main auditorium was [Jaidev Deshpande](https://www.twitter.com/jaidevd).
I'd interacted with him a bit last year and particularly enjoyed his talk on Commoditization of Machine Learning Libraries.
We exchanged contact information and other details for the next day.

Later in the evening, I didn't have any plans so I decided to tag along with the RedHat guys to a nearby Burger King for dinner.
We discussed a lot of computery things like Kubernetes, Go, Kotlin, Java, Rust, systems programming, Python Express and #dgplug.
We also exchanged contact information and they asked me to check out the Kubernetes meetup group that they organize in Bangalore.
After consuming what were abnormally sized burgers, we parted our way for the day.

------

## 4th Nov 2017 - Day 3
{: #day3}

This was the first day of the actual conference of PyCon India 2017.
After I registered myself and collected the swag, I made a beeline for the coffee stall and met [Ratan](https://github.com/RatanShreshtha) who was also a member of #dgplug.
He talked about his work at Reliance Jio and how they used the various technologies that he knew.
After the breakfast, I headed to the main conference hall to coordinate with Jaidev.
I assumed my position as mic and lighting controller in the gallery of the main auditorium.

### Mentoring: What, Why, How - Noufal Ibrahim
{: #keynote1}

The first talk was the keynote on "Mentoring : What, Why, How" by Noufal Ibrahim.
I'd been following Noufal on Twitter for a while, but had no idea that he was such an important part of the Python community in India.
The keynote was one of the most beautiful ones I'd seen.
He'd used his calligraphy skills to create gorgeous handmade slides that gave him away as a perfectionist.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Excellent keynote session by Noufal Ibrahim<a href="https://twitter.com/hashtag/pyconindia2017?src=hash&amp;ref_src=twsrc%5Etfw">#pyconindia2017</a> <a href="https://twitter.com/pyconindia?ref_src=twsrc%5Etfw">@pyconindia</a> <a href="https://t.co/QNXQBYl5TC">pic.twitter.com/QNXQBYl5TC</a></p>&mdash; Mehul Prajapati🐍 (@Mehul2802) <a href="https://twitter.com/Mehul2802/status/926670127864496128?ref_src=twsrc%5Etfw">November 4, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

The wisdom shared was quite insightful as I could closely relate to it even though I'd only taught(not mentored) a couple of people.
I think that speaks quite a bit about the generality of the ideas presented in the talk.
I also particularly enjoyed the Oath of a Mentor which was adapted from the Oath of the Night's Watch from A Game of Thrones. 

------

### Visualizing machine learning algorithms in Python - Anand S
{: #viz-ml}

[Talk Proposal](https://in.pycon.org/cfp/2017/proposals/visualizing-machine-learning-algorithms-in-python~eE64a/) -- Anand S ([@sanand0](https://twitter.com/sanand0))

I was always interested in data visualization and had problems coming up with ways to present data beyond a boring bar chart.
I attended this talk hoping that it would shed some light on how I could better create present my data.

Instead, it was a wonderful surprise as the talk was much deeper.
The speaker talked about how the machine learning algorithms were treated as a black box that worked really well.
The results however were often unintuitive and the algorithm's couldn't provide a reasoning behind a specific result.
This made the end users who were supposed to consume the results were very uncomfortable following it.

This was a real challenge which will grow bigger as Artificial Intelligence becomes heavily used.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Currency forecast viz by <a href="https://twitter.com/sanand0?ref_src=twsrc%5Etfw">@sanand0</a> <a href="https://twitter.com/hashtag/pyconindia?src=hash&amp;ref_src=twsrc%5Etfw">#pyconindia</a> <a href="https://twitter.com/pyconindia?ref_src=twsrc%5Etfw">@pyconindia</a> <a href="https://t.co/zYXzpY5ek2">pic.twitter.com/zYXzpY5ek2</a></p>&mdash; Rajat Goyal (@rajat404) <a href="https://twitter.com/rajat404/status/926695278849044480?ref_src=twsrc%5Etfw">November 4, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

He described a sample TV channel use case with a population dataset.
He demonstrated how the input data can be filtered along all its dimensions and then overlayed with the algorithm's clusters to provide intuitive visualizations on how the cluster's were derived.

In my opinion, this was easily the best talk I attended in the entire conference.

------

### Liberating tabular data from the clutches of PDFs - jayant
{: #liberate-pdf}

[Talk Proposal](https://in.pycon.org/cfp/2017/proposals/liberating-tabular-data-from-the-clutches-of-pdfs~dRjwd/)

If someone came to me asking if I could parse thousands of PDFs and convert it into structured usable data, I would've laughed and sent them away.
To my surprise, someone is actually doing this and quite successfully at that.
It involves doing all kinds of things that greatly benefit from the increased computational power that is available today.
This includes line and table detection through image processing, followed by text extraction and converting it to structured data.
It was a very enlightening talk on something that I'd previously considered infeasible.

------

### Panel Discussion on 'Where Python Fails'
{: #panel1}

I was hoping for an interesting panel discussion, given the topic and the fact that the entire conference was about Python.
People on the panel were: [Noufal Ibrahim](https://github.com/nibrahim), [Peter Wang](https://www.twitter.com/pwang), [Anand Chitipothu](https://twitter.com/anandology) and [Anand S](https://www.twitter.com/sanand0). The host was a prof from IIT-B.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr"><a href="https://twitter.com/hashtag/pyconindia?src=hash&amp;ref_src=twsrc%5Etfw">#pyconindia</a> <a href="https://twitter.com/hashtag/pyconindia2017?src=hash&amp;ref_src=twsrc%5Etfw">#pyconindia2017</a>  what is python not good at? Python 3 migration? GIL? Interesting panel discussion <a href="https://t.co/1jsF8ag6O1">pic.twitter.com/1jsF8ag6O1</a></p>&mdash; Aubergine Solutions (@auberginetweets) <a href="https://twitter.com/auberginetweets/status/926712977008476160?ref_src=twsrc%5Etfw">November 4, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Lots of things were discussed including packaging, Python 2 vs 3, charting libraries, GIL, the threat of Javascript.
Most of the panelists had very differing views.
I'll still try to summarize the takeaways as follows:
 * everybody should upgrade to Python 3 or start new projects in Python 3
 * the packaging scenario is much better right now than it was a few years ago
 * the GIL is going nowhere and waiting for it to disappear is futile
 * new charting libraries will always keep coming up because meeting all the requirements of a given use case is impossible in a single library
 * and finally Javascript is inescapable and things need to work with it regardless of one's opinion the language

------

### Lightning Talks
{: #lightning1}

The lightning talks were quite fast and lively.
Most people talked about their local Python communities and how you could be a part of them.
This included [KanpurPython](https://kanpurpython.wordpress.com/), [PyKutch](http://pykachchh.github.io/workshop/), [PythonPune](http://pune.python.org.in/), [PyDelhi](https://pydelhi.org/), [BangPypers](http://bangalore.python.org.in/) and [#dpglug](https://dgplug.org/) among many others.

------

### Building single page javascript apps with Django, Graphql, Relay and React! - Nicolas Romero
{: #building-spa}

[Talk Proposal](https://in.pycon.org/cfp/2017/proposals/building-single-page-javascript-apps-with-django-graphql-relay-and-react~axoze/)

What really caught my attention here was GraphQL and I wanted to know more about how it was being used with Django and Relay.
But it turned out to be a talk about a boilerplate generation tool called [Reango](https://github.com/ncrmro/reango).
Since I hadn't user GraphQL or Relay, I didn't understand some part of the talk.
Regardless, it still provided me with some insight on how the libraries could work together.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">We are really excited to host Nicholas Romero <a href="https://twitter.com/pyconindia?ref_src=twsrc%5Etfw">@pyconindia</a> talking about Django, React, Graphql to built SPAs.<a href="https://twitter.com/hashtag/pyconindia?src=hash&amp;ref_src=twsrc%5Etfw">#pyconindia</a> <a href="https://twitter.com/hashtag/Django?src=hash&amp;ref_src=twsrc%5Etfw">#Django</a> <a href="https://t.co/uUC1JxuscJ">pic.twitter.com/uUC1JxuscJ</a></p>&mdash; Gourav Chawla (@TechDeviant) <a href="https://twitter.com/TechDeviant/status/926746725246570497?ref_src=twsrc%5Etfw">November 4, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

------

### Self-Healing Code: A Journey Through Auto-Remediation - Arun Singh
{: #self-healing-code}

[Talk Proposal](https://in.pycon.org/cfp/2017/proposals/self-healing-code-a-journey-through-auto-remediation~dw2Xb/)

This was a talk on Saltstack and how one could implement and automate a self healing cluster of services.
The speaker described in detail the push/pull mechanism that Saltstack supports and how it enables a wide variety of workflows.
He discussed how it was deployed at Adobe to automatically kill off unresponsive nodes in a cluster of servers and spin up new nodes as replacements.
This let him fill out reports and perform the root cause analyses the next morning instead of having to prop up his laptop in the bed at three in the night.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Last talk for the day in seminar hall 1. <a href="https://twitter.com/pyconindia?ref_src=twsrc%5Etfw">@pyconindia</a> <a href="https://twitter.com/hashtag/PyConIndia?src=hash&amp;ref_src=twsrc%5Etfw">#PyConIndia</a> Self-healing code. <a href="https://t.co/vpCkBrxn5T">pic.twitter.com/vpCkBrxn5T</a></p>&mdash; Ayush Kesarwani (@ayushkesar) <a href="https://twitter.com/ayushkesar/status/926765549320773632?ref_src=twsrc%5Etfw">November 4, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

------

### Keynote - Python Community Principles by Elizabeth Ferrao
{: #keynote2}

Elizabeth is the Co Founder of [Women Who Code NYC](https://www.womenwhocode.com/nyc) and delivered the closing keynote of the day.
This was a non-technical presentation on community principles and their importance in software development.
She drew primarily from her experiences organizing Women Who Code NYC and various conferences around the world.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Keynote on &quot;Python Community Principles&quot; by <a href="https://twitter.com/MusingMurmurs?ref_src=twsrc%5Etfw">@MusingMurmurs</a> at <a href="https://twitter.com/pyconindia?ref_src=twsrc%5Etfw">@pyconindia</a> <a href="https://twitter.com/hashtag/pyconindia?src=hash&amp;ref_src=twsrc%5Etfw">#pyconindia</a> <a href="https://t.co/8Af5g9CYYt">pic.twitter.com/8Af5g9CYYt</a></p>&mdash; Tasdik Rahman (@tasdikrahman) <a href="https://twitter.com/tasdikrahman/status/927101689538035712?ref_src=twsrc%5Etfw">November 5, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

It was a nice and relaxed talk on what different tech communities were doing around the world.
She talked about the things new communities should keep in mind when starting up and how existing communities could improve themselves so that they becomes an attractive place for more people to participate in.

------

### After Events
{: #day3-after-events}

Once the first day of the conference ended, I proceeded to join the rest of the volunteers for a retrospective on how the day went.
We discussed what went wrong and what could be improved, this included any tech glitches that cropped up with the mic system, the video recordings and other issues related to scheduling and catering.
Some responsibilities were reassigned and new volunteers joined in while some others went missing.

I also found out that a volunteer's dinner had been organized at a barbecue restaurant close by.
The dinner was a lot fun and I had deep discussions on Python, math, books and games with some of the new friends I'd made.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">volunteers party <a href="https://twitter.com/pyconindia?ref_src=twsrc%5Etfw">@pyconindia</a><a href="https://twitter.com/This_is_Devesh_?ref_src=twsrc%5Etfw">@This_is_Devesh_</a>  <a href="https://twitter.com/IHackPY?ref_src=twsrc%5Etfw">@IHackPY</a> <a href="https://twitter.com/techy_tushar?ref_src=twsrc%5Etfw">@techy_tushar</a>  <a href="https://twitter.com/rajkmaurya111?ref_src=twsrc%5Etfw">@rajkmaurya111</a> <a href="https://twitter.com/UB_Shubh?ref_src=twsrc%5Etfw">@UB_Shubh</a> @abhi895312<a href="https://twitter.com/hashtag/pyconindia?src=hash&amp;ref_src=twsrc%5Etfw">#pyconindia</a> <a href="https://twitter.com/hashtag/KanpurPython?src=hash&amp;ref_src=twsrc%5Etfw">#KanpurPython</a> <a href="https://t.co/pTiWOLwkwA">pic.twitter.com/pTiWOLwkwA</a></p>&mdash; Aniket uttam (@Aniketuttam1) <a href="https://twitter.com/Aniketuttam1/status/926826939372810241?ref_src=twsrc%5Etfw">November 4, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Post dinner, I rode the Metro back home with [Sanyam Khurana](https://github.com/CuriousLearner), one of the organizers of the PyDelhi community.
He talked about his attempts to spread Python and Open Source in his college and the challenges that he had to overcome in doing so.
I really enjoyed his colorful style of narrating his endeavours.

------

## 5th Nov 2017 - Day 4
{: #day4}

This was the last day of the whole PyCon India 2017 event.
I arrived on time and made sure I was well caffeinated before proceeding to the main hall for the keynote.

### Keynote - Python and Data: Past, Present and Future by Peter Wang
{: #keynote3}

[Peter Wang](https://www.twitter.com/pwang) is the CTO of Anaconda Inc. which was previously known as Continuum Analytics.
His keynote was a nice treatise on the problems that had plagued Python in the past,
what measures were taken by the community to fix them and what new the community as a looked forward to.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Starting Day 4 with keynote by <a href="https://twitter.com/pwang?ref_src=twsrc%5Etfw">@pwang</a> <br>Head to Main Audi on the ground floor now.<a href="https://twitter.com/hashtag/pyconindia?src=hash&amp;ref_src=twsrc%5Etfw">#pyconindia</a> <a href="https://t.co/FoZn39081X">pic.twitter.com/FoZn39081X</a></p>&mdash; PyCon India (@pyconindia) <a href="https://twitter.com/pyconindia/status/927028008417767424?ref_src=twsrc%5Etfw">November 5, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

He discussed why his company built [Conda](https://conda.io), why they _had_ to improve the python packaging ecosystem itself in order to better perform their job of delivering quality software.
He also talked about [Bokeh](https://bokeh.pydata.org/en/latest/), an Open Source visualization library for Python which his company is building in order to better serve the needs of today.

------

### Spinning local DNS server sourcing responses over HTTPS to combat Man-in-the-middle attack - Arnav Kumar
{: #dns-over-http}

[Talk Proposal](https://in.pycon.org/cfp/2017/proposals/spinning-local-dns-server-sourcing-responses-over-https-to-combat-man-in-the-middle-attack~eVnoe/)

I decided to attend this talk because I remembered reading a blog post where someone had hacked up a solution to make HTTP work over DNS.
This was implementing the reverse where it was running DNS over HTTPS so that the DNS records wouldn't be tampered with.
It was a nifty hack, that had only one drawback where you had to hardcode the IP addresses of the HTTP server that you were using to query the records.

PS. I later found out about DNScrypt which achieves the same goals without bringing HTTP into the mix.

------

### How import works in Python - Sasidhar Donaparthi
{: #how-import-works}

[Talk Proposal](https://in.pycon.org/cfp/2017/proposals/how-import-works-in-python~dypzb/)

Ever since I'd used flask and it's extensions I'd known that Python's import machinery was hackable.
But I hadn't gotten the time to actually look into it's workings.
This talk gave a me a nice opportunity to understand how it worked.

About halfway through the talk I could see the similarities between webpack loaders and the python import mechanism.
I sort of plan to implement a JSON loader in python such that one can directly import json files into python without having to manually call all the file handling logic.

I also discussed this with the speaker during an offline interaction but he mentioned that you cannot actually change the source code, you can only point/redirect/block the interpreter to a different piece of python code.
I still want to try it out just to understand where exactly it blocks me.

------

### Panel Discussion on Women in Open Source
{: #panel2}

While I hadn't given it much thought in the beginning, women are clearly under-represented in the Open Source software community.
This panel was held to discuss the reason why it is, the challenges faced by women who are in the community and what efforts are currently underway.

The panel consisted of:
* Anwesha Das - [@anweshasrkr](https://twitter.com/anweshasrkr), 
* Vaishali Thakkar - [@kernel\_girl](https://twitter.com/kernel_girl), 
* Elizabeth Ferrao - [@MusingMurmurs](https://twitter.com/MusingMurmurs), 
* Shivani Bhardwaj - [@tuxish](https://twitter.com/tuxish), 
* Priyal Trivedi - [@priyal1404](https://twitter.com/priyal1404) 

all of whom are actively involved in the technology community in some way or the other.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr"><a href="https://twitter.com/hashtag/PyConIndia?src=hash&amp;ref_src=twsrc%5Etfw">#PyConIndia</a> &#39;women in <a href="https://twitter.com/hashtag/opensource?src=hash&amp;ref_src=twsrc%5Etfw">#opensource</a>&#39; panel discussion <a href="https://twitter.com/kernel_girl?ref_src=twsrc%5Etfw">@kernel_girl</a> <a href="https://twitter.com/anweshasrkr?ref_src=twsrc%5Etfw">@anweshasrkr</a> <a href="https://t.co/3Qs3jaLjOf">pic.twitter.com/3Qs3jaLjOf</a></p>&mdash; chandan kumar (@chkumar246) <a href="https://twitter.com/chkumar246/status/927067626706210816?ref_src=twsrc%5Etfw">November 5, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

The various efforts that were discussed were: 
* Women Who Code (<https://www.womenwhocode.com/>)
* Rails Girls Summer of Code (<https://railsgirlssummerofcode.org/>)
* PyLadies (<http://www.pyladies.com/>)
* DjangoGirls (<https://djangogirls.org/>)
* LinuxChix (<https://www.linuxchix.org/>)

------

### Django on Steroids - Building Applications at Web Scale - Sanket Sourav
{: #django-steroids}

[Talk Proposal](https://in.pycon.org/cfp/2017/proposals/django-on-steroids-building-applications-at-web-scale~ejLBb/)

This was a talk on how to build your django application in such a way from day one, so that you don't have scaling pains down the line.

Contrary to most suggested approaches, the speaker had some interesting approaches like consolidating all his models inside a single app instead of splitting them across multiple apps.
He also discussed how a lot of things that django comes built in with need to be swapped out over time so that they may scale much better.
This included the templating engine, the orm and some other things.

The talk was a bit anecdotal as the author recounted a lot of instances from their production deployment of django and how it evolved.

------

### Clean Architecture Applications in Python - Subhash Bhushan
{: #clean-arch}

[Talk Proposal](https://in.pycon.org/cfp/2017/proposals/clean-architecture-applications-in-python~bqDka/)

The speaker was an industry veteran in software design and worked at Sapient Nitro.
The general architecture that he was going to discuss was the clean architecture.

I'd never heard of this design pattern before, so I decided to attend this talk.

After going through his talk I realized that I'd already implemented this pattern in multiple places before.
Infact it is the kinds of pattern that Java and it's ecosystem of frameworks like Spring et al encourage you to build.

As the speaker continued he mentioned that the _clean_ approach may not be suited for smaller projects or those that have a definite lifetime.
The overheard of implementing the layers of indirection introduced by the clean architecture may also make things harder to grasp for new people. 

------

## After Effect
{: #after-effects}

While there are countless experiences that I have collected from the conference, I felt the need to write down some things that I did as a direct result of having attended the conference:

* set up ZNC on a Digital Ocean droplet using docker-machine so that I can hang out on #dgplug without missing messages
* registered myself as a tutor on Python Express ( <https://pythonexpress.in/profile/satyanash/>)
* planning to attempt building a json loader using pure python imports
* attended a Kubernetes Bangalore meetup hosted by Suraj, Suraj et al
* subscribed to the inpycon, pycon pune mailing lists
* volunteering for PyCon India 2018, expected to be held in Bengaluru

I think it was one of the best conferences I've attended till date as I've also successfully managed to complete a blog post recording almost everything I did at the conference.

![PyCon India 2017 - New Delhi](/img/pycon_india_2017_billboard6.jpg 'PyCon India 2017 - New Delhi')

------

## 1st Nov 2017 - Day 0 (Appendix)
{: #day0}

This was the day I reached New Delhi.
I was staying at my uncle's guest house in Lajpat Nagar.
We rendezvoused at the Nizamuddin Railway station and proceeded to the guest house in the same cab.

Once I got to the guest house, I freshened up and decided to check out Chandni Chowk and what it was all about.
Took a metro directly from Lajpat Nagar to Chandni Chowk and climbed out to be greeted by an extremely crowded street which left me with little doubt that there'd be a lot to explore here.

First I made my way to the Paratha wali galli and gorged on three parathas which was supposed to be my lunch.
I tried a potato paratha which was to be my benchmark, a nimbu paratha and a greenpea paratha.
Once I was done with it, I moved on to a lassi shop nearby and got myself a beer glass of lassi, and carried it as I walked along Nayi Sarak.

From there I proceeded to the old book stores on Nai Sarak and tried to look for a place where I could browse old books that might have something interesting for me, but I didn't find any.

Then I checked the map and realized that Lal Kila ( or the Red Fort) was really close by and decided to check it out.
I went and bought a ticket for Rs.35 and walked in.

I hadn't expected it to be so big and sprawling from the inside.
It has a bunch of gardens and mughal era buildings and even british era buildings that were constructed much later.

First thing that you see on entering are the red fort shops which are basically selling show pieces which I had no interest in looking at so I skimmed right through.
The next building was a museum which housed a lot of artifacts recovered from the mughal era, this included swords, shields armour, pots and manuscripts among other things.

Then I proceeded to another museum which was Mumtaj Mahal and was supposed to be the quarters of the queen.
They had a few interesting documents inside the museum, the translations of which were worth reading.
There were also a few military correspondence documents which had a very lore-y feeling to them.
I later learned that the mahal looked slightly different than when it was originally occupied by the queen because it was repurposed to function as a jail later on by the British.

I then decided to walk around the Hayatt gardens and rested a bit by the well.
I also happened to make friends with a squirrel who clearly wanted food from me.
Fortunately I had a few peanuts handy and was able to keep it hanging around for a while.
This in my recollection was the first ( and possibly last) time I actually touched a squirrel.
It reminded me of the mythical story of how the Indian squirrels got the twin stripes on their backs when Ram caressed their fur after seeing them help build his bridge to Lanka.

![Squirrel - New Delhi](/img/pycon_squirrel.jpg 'Squirrel - New Delhi')

After I had rested enough, I walked out of the fort and back onto Chandni Chowk to taste some more street food.
I had a plate full of Jalebi Rabri which clearly exceeded my daily sugar quota. But it tasted great.
I also proceeded to try the Dahi Bhalla from a stall nearby which looked to be the reason for most of the crowd around it.

After walking around some more, I decided to leave and metroed directly to Hauz Khas to meet a friend who was working on his startup at IIT Delhi.
Had a nice interaction with him before Ubering back to the guest house at around 2200.
