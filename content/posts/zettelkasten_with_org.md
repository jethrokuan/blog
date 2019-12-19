+++
title = "Org-mode Workflow Part 3: Zettelkasten with Org-mode"
author = ["Jethro Kuan"]
lastmod = 2019-12-19T18:06:24+08:00
draft = false
math = true
+++

_(Previous Post: [Org-mode Workflow Part 2: Processing the Inbox]({{< relref "processing_inbox" >}}))_

Many of my tasks are articles, and online lectures that I need to go
through for independent research. When going through these material, I
like to record down notes for later reference.

> If you can't explain something to a first year student, then you
> haven't really understood. -- Richard P. Feynman


## Background {#background}

I'm going to provide some history at how I arrived here, feel free to
skip ahead if you're not interested.

I've had a habit of note-taking since my secondary school days, which
is more than a decade ago. I'd condensed and rephrase whatever the
teachers taught into shorter material. This strategy had been
sufficient, up until just a year ago when I was first exposed to
research. Lectures and tutorials often had a fixed curriculum.
Academic material was taught in a linear fashion, and it was fine to
follow the order in which the material was taught. Research (and
thinking) is, however, highly non-linear. Much of academic process
comes from forming links between ideas that come from vastly different
fields. I was frustrated at being ineffective at research, and knew I
had to change how I managed things. I did some (ineffective) research,
and asked my senior Cedric who authors [Commoncog](https://commoncog.com/blog/), hoping he'd have
some suggestions. He'd suggested the P.A.R.A. method in [Tiago Forte's
Building a Second Brain](https://www.fortelabs.co/). There's even [a guest post showing how to do
it in org-mode](https://tasshin.com/blog/implementing-a-second-brain-in-emacs-and-org-mode/), but I was hoping for something simpler that would
allow me to quickly get up and running.

At around the same time, [Roam Research](https://roamresearch.com/) started gaining some traction,
and [some good reviews](https://twitter.com/adam%5Fkeesling/status/1196864424725774336) on Twitter. Roam Research sold itself as a tool
for networked thought, and this explicitly resolved my issue of my
notes being too linear. It did so by providing 2 features:

1.  Ease in creating new entries
2.  Automatic back-linking (what notes are linked to this one?)

This was also at a time when [Zettelkasten came under my radar](https://www.lesswrong.com/posts/NfdHG6oHBJ8Qxc26s/the-zettelkasten-method-1), which
seemed to be the predominant way people were using Roam Research. I
thought it'd be easy to bring the ideas from Roam Research into my
org-mode note-taking workflow, so I set out to build something
similar. To my surprise, this only took about an hour of Googling and
tweaking.


## Why take notes in Org-mode? {#why-take-notes-in-org-mode}

While Org-mode is just a simple plain-text format specification, Emacs
provides fantastic facilities that make it incredibly powerful. Here
is a small list of its features:

-   Write and preview LaTeX from within the file (including Beamer).
    I've written entire literature reviews and progress reports in
    Org-mode.
-   Simple bibliographic management with [org-ref](https://github.com/jkitchin/org-ref)
-   Literate Programming with [org-babel](https://orgmode.org/worg/org-contrib/babel/intro.html). Run snippets of code from
    within the org file
-   HTML, ODT, PDF export
-   Excel-like table functionality


## A Taxonomy of Notes {#a-taxonomy-of-notes}

Before I mentioned that much of my notes came from articles, academic
papers, and books. I found the need to clearly separate my own thoughts and
opinions from an author's, and carefully attribute the source of these
ideas. Hence, I created 3 separate sections for my notes:

papers
: summaries of academic papers I've read

books
: summaries of the books I've read

root
: concepts, and personal thoughts

These are all kept in individual `.org` files so my notes directory
looks like:

```text
- books/
  - book1.org
  - book2.org
- papers/
  - paper1.org
  - paper2.org
- concept1.org
- thought1.org
- ...
```

Each of these notes are kept relatively small, and may link to each
other, just as in Roam. I use the brilliant [org-ref](https://github.com/jkitchin/org-ref) to cite all my
sources, so I can always return to the source in doubt, and also give
proper attribution.


## The Knowledge Base Overview {#the-knowledge-base-overview}

I use [Deft](https://jblevins.org/projects/deft/), which is a mode for quickly browsing and filtering
plain-text files. As shown previously, here's how it looks like:

{{< figure src="/ox-hugo/screenshot2019-12-13_15-56-56_.png" caption="Figure 1: Knowledge Base with Deft" >}}


## Creating New Notes {#creating-new-notes}

Suppose I was watching a lecture video, and came across a concept (in
this example, "experience replay"). I open the main page, and perform
a full-text search across all notes:

{{< figure src="/ox-hugo/deft_search.gif" caption="Figure 2: Full-text search with Deft" >}}

Here, I see that experience replay occurred in 2 of my notes: in
the seminal paper introducing it, and in a overall concept note for
deep reinforcement learning. Pressing `<enter>` on each line brings me
to the exact line where the term occurs. This is really helpful for
recall.

Suppose I wanted to expand on _experience replay_, and provide more
detail. I would create a new concept note, also bound to a hotkey:

{{< figure src="/ox-hugo/deft_create.gif" caption="Figure 3: Creating a new note with Deft" >}}

I have Emacs scripted such that it processes the file name into a
suitable title (no points for guessing how).


## Linking Notes Together {#linking-notes-together}

Linking is a step that's manual, but purposefully so. It forces us to
think about what kind of links there are between notes, which is
difficult and usually the most fruitful kind of thinking. If one
exports these directional links, it's possible to discover surprising
lines of thought.

(Random thought: one could possibly do some form of topic-modelling or
tf-idf similarity scoring between notes to help in this respect, but
that sounds expensive... incremental topic-modelling?)

Since every note is an org file, linking between notes are essentially
file links, and this was simple to implement:

{{< figure src="/ox-hugo/screenshot2019-12-19_18-02-25_.png" caption="Figure 4: All files in the notes directory are candidates!" >}}

To go one step further, one could link to a non-existent note, and
it'd create the link to a new note, similar to Roam!

{{< figure src="/ox-hugo/deft_link.gif" caption="Figure 5: Linking to a note. Non-existent notes become new notes." >}}


## Back-linking {#back-linking}

Back-linking is the simple task of finding which notes link to the
current note. This is an easy programming task, using existing tools
like `grep`:

{{< figure src="/ox-hugo/backlink.gif" caption="Figure 6: Rudimentary back-linking in Emacs" >}}

However, I don't actually use this often.


## Where the Benefits Come From {#where-the-benefits-come-from}

With the change to this system, I've been able to keep my notes small
and digestible. I've also been able to do the kind of non-linear
thinking that is required in academic research. I no longer have to
think had about where some information should go, and my thoughts can
flow freely into my second brain. My knowledge repository now
[generates positive interest rate](https://twitter.com/vgr/status/1203741612007931904).

I've also been able to freely share my knowledge with others. My notes
are plain-text and version-controlled, automatically published to
[braidump.jethro.dev](https://braindump.jethro.dev/) via Netlify and Hugo.


## Conclusion {#conclusion}

This concludes the series on my org-mode workflow. Hope you enjoyed
it, and I'm looking forward to see it further evolve.
