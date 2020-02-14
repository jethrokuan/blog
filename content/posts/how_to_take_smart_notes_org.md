+++
title = "How To Take Smart Notes With Org-mode"
author = ["Jethro Kuan"]
date = 2020-02-14T00:00:00+08:00
lastmod = 2020-02-15T02:36:16+08:00
tags = ["emacs"]
draft = false
math = true
+++

While writing the documentation for Org-roam, it occurred to me that I
have a lot to say that doesn't truly belong in the documentation. I
wrote Org-roam because Org-mode simply didn't have the utilities to
enable the kind of note-taking workflow I wanted. I don't want to be
prescriptive about how note-taking should be done, but Org-roam is
open enough to enable many note-taking styles, some of which (I feel)
will be inferior to others. This post is also in part for users to
understand that there are several feature requests that I may consider
anti-features, such as renaming notes, and having nested folder
structures.

This is the workflow I use. Here I explain what I think note-taking
should be, and why it should be this way. I implore you (especially
users of Org-roam) to read this through. As usual, let me know what
you think by [mail](mailto:jethrokuan95@gmail.com).

The ideas here are definitely not my own: much of it comes from How
To Take Smart Notes by Sonke Ahrens.


## Note-taking Is Not Just a Precursor to Writing {#note-taking-is-not-just-a-precursor-to-writing}

> Notes aren't a record of my thinking process. They are my thinking
> process. -- Richard Feynman

In higher education, students are expected to produce papers. What I
say doesn't just apply to students or aspiring writers: the ability to
turn thoughts to writing is essential for anyone who wants to improve
their learning or writing. One can imagine the process of writing to
be broken down into the following steps:

1.  Find topic/research question
2.  Research/find literature
3.  Read and take notes
4.  Draw conclusions / outline text
5.  Write

But what about all those lectures and seminars you attend? Books and
papers you read? Conversations with friends, colleagues, professors?
Surely these must factor into our eventual work somehow. How do you
know what's a good research question, if you haven't read a lot? How
do you derive new ideas and insights, without accounting for the
current knowledge?

Indeed, the preparation for writing begins much earlier, with
note-taking! What if we follow Feynman's advice, and make note-taking
the thinking process?

Suppose you had an awesome second brain, that could surface content up
to you where you wanted it. You have a bunch of unrefined ideas
sitting around, thoughts you had speaking with friends, or from
reading something on the web. Link them up together, and you have a
paper. Instead of beginning with the research question, and going top
down, we begin with the notes, and build and refine ideas from the
bottom up. This also breaks writing down into small, reasonable steps
(one note at a time).

This is the driving principle behind the Zettelkasten method, and it
brings me to my main point:

> The primary purpose of note-taking shouldn't be for storing ideas, but
> for developing them. The question we want to ask ourselves when we
> write a note should be: **"In what context do I want to see this note
> again?"**

A corollary to that statement is that notes can really go anywhere you
want. They just have to surface where you want them to.

How do we do all these in Org-mode? This is where Org-roam comes in.


## How I Take Notes {#how-i-take-notes}

I take 2 kinds of notes: fleeting notes, and project-related notes.

Fleeting notes are notes that are taken as a reminder of what's in my
head. I take fleeting notes in my daily notes, an idea borrowed from
[Roam Research](https://www.roamresearch.com/). I couple these fleeting notes with my journal, so I use
[org-journal](https://github.com/bastibe/org-journal) to do so:

{{< figure src="/ox-hugo/fleeting_notes.gif" >}}

Fleeting notes get refined into their own note (own file), and are
removed from the daily page. These notes are given file-tags, more on
this later.


### Project Notes {#project-notes}

Project notes are basically everything else, although I encourage you
to read up about the [PARA method](https://praxis.fortelabs.co/the-p-a-r-a-method-a-universal-system-for-organizing-digital-information-75a9da8bfb37/) as these do serve as useful
file-tags. Here are some examples of items that get their own project
note:

-   a talk (e.g. [Emacs Should Be Emacs Lisp - Tom Tromey](https://braindump.jethro.dev/talks/emacs%5Fshould%5Fbe%5Femacs%5Flisp/))
-   a book (e.g. [Are We Smart Enough to Know How Smart Animals Are?](https://braindump.jethro.dev/books/are%5Fwe%5Fsmart%5Fenough%5Fto%5Fknow%5Fhow%5Fsmart%5Fanimals%5Fare/))
-   a paper (e.g. [Are We Really Making Much Progress? A Worrying
    Analysis of Recent Neural Reco...](https://braindump.jethro.dev/papers/dacrema19%5Fprogress%5Fneural%5Frec/))
-   any topic or thought I've refined from my fleeting notes

Let's go through a working example of how I do this. I'm picking a
random link from my TODOs in my agenda, for it happens to be this
Hacker News thread: [Ask HN: How do you learn complex, dense technical
information? | Hacker News](https://news.ycombinator.com/item?id=22325975)

At this time I call `org-roam-find-file`, and type in the title of the
note I want: _"HN : Learning Complex Information"_:

{{< figure src="/ox-hugo/org-roam-find-file.gif" >}}

This creates a note with a random filename (not important to my
workflow). Throughout the note-taking process, I ask myself the
question (which I bold again to emphasise): **"In what context do I want
to see this note again?"**

And then I begin to insert links to files using `org-roam-insert`. It
doesn't matter if the file doesn't yet exist, Org-roam creates the
files for you. I do this by adding tags at the start of the file:

{{< figure src="/ox-hugo/org-roam-insert-filetag.gif" >}}

Now if I whenever I want to revisit anything about learning, I can
head to the `Learning` page and look at the back-links buffer. And it
seems I already have material from the [Learning How To Learn](https://www.coursera.org/learn/learning-how-to-learn/) course,
and [an article about how to do hard things](https://www.drmaciver.com/2019/05/how-to-do-hard-things/).

{{< figure src="/ox-hugo/screenshot2020-02-15_02-02-29_.png" >}}

Making these kind of manual connections help reinforce learning. Going
through the HN thread, I see various items mentioned, which I link to
in my notes. Again, here I create file links liberally, even though I
may not yet have content in them.

For example, here I:

-   see a note of the three-pass technique. I create a new link with
    `org-roam-insert` for `Three Pass Technique`, and add the paper to
    my to-do list (I've already read this, but I should revisit for post
    note-taking me's sake)
-   I see some talk on spaced repetition. I already have a note for
    this, which I link to. Now when I visit spaced repetition file, I
    can see the debate in this HN thread.

Here's what the note ended up looking like. Terrible example
(wasn't really an insightful thread), but I'm in too deep now.

{{< figure src="/ox-hugo/screenshot2020-02-15_02-22-12_.png" >}}

All links are internal links to files within Org-roam. Doing this
continuously builds up a dense network of notes.


## How to Use These Notes {#how-to-use-these-notes}

Nat Eliason produced a [fantastic video showcasing how he used these
notes to outline an article quickly](https://www.youtube.com/watch?v=RvWic15iXjk). This is showcases essentially
what I discussed earlier about putting together ideas from notes to
produce a written work. If I haven't convinced you that this
note-taking style is extremely empowering, this 15 minute video will.

This article was also written in about an hour, in similar style. I
first looked at all my notes from relevant tags:

-   <https://braindump.jethro.dev/zettels/writing%5Fwith%5Fzettekasten/>
-   <https://braindump.jethro.dev/zettels/how%5Fto%5Ftake%5Fsmart%5Fnotes/>
-   <https://braindump.jethro.dev/zettels/zettelkasten/>
-   <https://braindump.jethro.dev/zettels/writing%5Fwith%5Fzettekasten/>
-   <https://braindump.jethro.dev/zettels/roam%5Fresearch/>

I simply took a couple of key points and pieced them together!


## Concluding Remark {#concluding-remark}

All of this had been enabled by simply exploiting bidirectional
linking to its fullest extent. What I demonstrated only scratches the
surface. There are many amazing Org packages that make note-taking
powerful (see [Ecosystem - Org-Roam](https://org-roam.readthedocs.io/en/develop/ecosystem/)).

I hope I made it clear that the note-taking technique came first, and
Org-roam was built to enable that. I outlined the principles behind my
note-taking workflow, and why Org-roam is the way it is.
