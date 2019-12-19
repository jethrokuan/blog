+++
title = "Org-mode Workflow Part 1: Capturing in the Inbox"
author = ["Jethro Kuan"]
date = 2019-12-14T00:00:00+08:00
lastmod = 2019-12-19T15:25:35+08:00
draft = false
math = true
+++

_(Previous Post: [Org-mode Workflow: A Preview]({{< relref "org_mode_workflow_preview" >}}))_

Have you ever sat down with nothing but a pen and a piece of paper,
writing down everything you need to do? Recall how you felt right
after. Did you feel more in control? Isn't it strange that you feel
better looking at the long list of work, knowing that your little
exercise accomplished nothing on the list? What pushed you to do this
little exercise?

The list made you feel more in control because it freed yourself from
having to remember to do these things. With every task on paper, you
can utilize the full capacity of your brain to do the actual hard work
of accomplishing tasks.

> Your brain is for having ideas, not storing them -- David Allen

Filling up the inbox is equivalent of doing this exercise,
systematically and consistently. The inbox is where everything begins.
Every article, thought and assignment starts from the inbox. Because
the inbox is so crucial to the workflow, the process of adding and
processing items is as frictionless as possible. The inbox is all
about trust. Trust that you everything you will need to think about is
captured somewhere. This allows you to give your 100% for the current
task.

Tasks pile up quickly, and arrive whenever they please, more often
than not while we are in the middle of something. The inbox is
designed such that I am able to file these tasks away in a snap, and
keep my attention on the current task.

Filling up the inbox should be fun! If you feel dread when you do
this, you're probably doing this wrong.


## Capturing Items Manually {#capturing-items-manually}

Org-mode ships with a feature called [org-capture](https://orgmode.org/manual/Capture.html), which allows for
quick storage of notes, from anywhere. I use this to quickly add
anything to my inbox.

{{< figure src="/ox-hugo/manual_capture.gif" caption="Figure 1: Capturing items manually" >}}


## Capturing Articles {#capturing-articles}

Org-mode has a neat feature called [org-protocol](https://orgmode.org/worg/org-contrib/org-protocol.html), which ties in
neatly with org-capture. Here, I use a Javascript bookmarklet to
automatically add webpages and PDFs to my inbox.

{{< figure src="/ox-hugo/article_capture.gif" caption="Figure 2: Capturing articles with a bookmarklet" >}}


## Capturing Email {#capturing-email}

I use an email system called [notmuch](https://notmuchmail.org/). I have 3 important email
accounts to keep up with, so I use [isync](http://isync.sourceforge.net/) to periodically fetch my
email and save them for offline use, and the Emacs notmuch interface
gives me access to mail from all accounts at the same time:

{{< figure src="/ox-hugo/screenshot2019-12-13_19-40-48_.png" caption="Figure 3: The notmuch main interface" >}}

{{< figure src="/ox-hugo/screenshot2019-12-13_19-41-22_.png" caption="Figure 4: notmuch sample mail view" >}}

Capturing an email is also a key away. It creates an entry in my inbox
with a link to the email.

{{< figure src="/ox-hugo/email_capture.gif" caption="Figure 5: Email Capture" >}}


## What's Next? {#what-s-next}

I've shown that org-mode provides great tooling to capture items. With
this, we have completed probably the most impactful step in the
workflow. In the [next part of the series]({{< relref "processing_inbox" >}}), I will explain how I process
these items.
