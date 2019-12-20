+++
title = "Org-mode Workflow: A Preview"
author = ["Jethro Kuan"]
date = 2019-12-13T00:00:00+08:00
lastmod = 2019-12-20T15:10:26+08:00
draft = false
math = true
+++

This is going to be a multi-part series on Emacs and org-mode. This is
also going to be a really long series, so before we begin I want to
give you an idea of what to expect. What I'm about to present is a
workflow I've tweaked over several years. It is a workflow that has
constantly evolved to adapt to my varying needs. At the time of
writing, I have completed 3478 todo items, and written over 29000
lines in my personal knowledge base.

This is **not** going to be a tutorial about Emacs or Org-mode. Many
years of trying to get people to use Emacs has taught me that teaching
this is extremely difficult, especially for those with no intrinsic
motivation. Those that have indeed picked it up have observed me use
Emacs from afar, and deemed it worthy of their time. Emacs has an
incredibly steep learning curve, but what you get in return is a tool
that will pay dividends over the remainder of your lifetime. Know that
the setup I have is not complex: it's no more than 500 lines of Emacs
Lisp. I wish this were more applicable to non-Emacs users, but
Org-mode is one-of-a-kind, and much of this would be impossible
without it. I hope this series will inspire you to pick up Emacs and
org-mode.

1.  [Part 1: Capturing Into The Inbox]({{< relref "capturing_inbox" >}})
2.  [Part 2: Processing The Inbox]({{< relref "processing_inbox" >}})
3.  [Part 3: Zettelkasten with Org-mode]({{< relref "zettelkasten_with_org" >}})


## Who am I? {#who-am-i}

To help put my workflow into context, let me tell you a little about
who I am. I'm an undergraduate studying Computer Science, and my
day-to-day involves keeping up with tech, and research across various
fields, such as neuroscience, robotics, and machine learning.


## Inspirations {#inspirations}

The workflow I've created is a culmination of [Getting Things Done](http://martin.zinkevich.org/rules%5Fof%5Fml/rules%5Fof%5Fml.pdf), and
[Zettelkasten](https://zettelkasten.de/). The former is used to manage daily tasks, while the
latter is for personal knowledge management. For more information
about these 2 systems, I recommend reading these two books:

-   [Getting Things Done: The Art of Stress-Free Productivity](https://www.goodreads.com/book/show/1633.Getting%5FThings%5FDone)
-   [How to Take Smart Notes: One Simple Technique to Boost Writing,
    Learning and Thinking](https://www.goodreads.com/book/show/34507927-how-to-take-smart-notes)


## The Big Picture, and a Sneak Peek {#the-big-picture-and-a-sneak-peek}

{{< figure src="/ox-hugo/screenshot2019-12-13_15-35-03_.png" caption="Figure 1: A high-level overview of the workflow" >}}

Despite appearing complicated, the workflow is in truth extremely
simple. All it does is exploit some of the key ideas in GTD and
Zettelkasten, using org-mode as the glue software. In fact, it is an
extreme simplification that has become evidently necessary in this
world of information overload, using a systematic approach to remain
in control.

First, I capture all of my thoughts, to-dos, to-reads into an inbox.
Capturing can happen at any point in time, but this is a crucial step
to ensure that I can continue to focus on the current task. When I'm
not working on anything, I refile (think categorize) these items
into 3 parts:

-   If the task can be completed within 2 minutes, it is done
    immediately and checked off the list
-   If the task, mail, article or paper belongs under a specific
    project, I file the task accordingly, grouping related items together
-   If it is a standalone task, such as running an errand or making a
    purchase, this goes under the `next` category

Here's an example of what things look like in org-mode:

{{< figure src="/ox-hugo/screenshot2019-12-13_15-51-28_.png" caption="Figure 2: The org-agenda view" >}}

I pick a task I wish to work on among the refiled items, and clock in
(more on this later). This gives me some idea of how much time I spend
on each task, and where my time goes to each day.

Depending on the task, I may want to take notes in my personal
knowledge base I call my braindump. A web version of it is [available
here](https://braindump.jethro.dev/), but is not the main mode of consumption. Here's the braindump in
its full, plain-text glory:

{{< figure src="/ox-hugo/screenshot2019-12-13_15-56-56_.png" caption="Figure 3: The braindump, web export available at <https://braindump.jethro.dev/>" >}}

In the [next part of this series]({{< relref "capturing_inbox" >}}) I talk about the inbox, the principles
guiding its design, and how I capture items.
