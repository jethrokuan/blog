+++
title = "Self-tracking in Plain Text"
author = ["Jethro Kuan"]
date = 2020-10-09T00:00:00+08:00
lastmod = 2020-10-10T14:28:56+08:00
tags = ["tools"]
draft = false
math = true
+++

I recently decided to start doing more self-tracking. In my [Org-mode workflow]({{< relref "org_mode_workflow_preview" >}})
series, I gave a brief overview of how I did task management, but what I failed
to mention then was that Org provides clocking capabilities, so I sort-of knew
where I was spending my time. However, I wanted to track things that are
unrelated to tasks. For instance, I wanted to track my mood at different times
of the day, or what I ate. I also wanted to track numeric quantities: how much
water did I drink? How far did I run? How long did I sleep?

In short, I wanted to create log entries for my life, from which I can later do
aggregate analyses on (is my sleep adversely affected by the food I eat?). To my
surprise, I could not find a simple tool that fit my needs. The tools I found
were either:

1.  Too specific: these are apps specifically designed to track a certain action
    (e.g. water intake apps, fitness apps). I needed a consistent interface for
    tracking anything.
2.  Binary: Org-mode's support for habit-tracking is limited to binary actions
    (e.g. did I exercise today?) Anything more complex [required significant
    tooling](https://www.philnewton.net/blog/diet-tracking-with-emacs/). Creating log entries need to be low friction.

This motivated me to build a simple proof-of-concept logger, [track](https://github.com/jethrokuan/track). It also
provided me an avenue to learn Rust, although in hindsight I didn't make much
progress on that front.


## The Track File Syntax {#the-track-file-syntax}

The track file resembles logs you'd see in any software. It is an append-only
file where each line is a log entry:

```text
[2020-10-09T17:54:01.246515233+08:00] water:300ml
```

In square brackets we have the timestamp of the log entry. The log entry begins
with a category, separated from the log entry value by a colon: here it is
`water`. Categories can be arbitrarily complex. For example, for the exercises I
perform, I "group" them under the same category by giving them the categories
`workout:push-ups` and `workout:pull-ups`.

The log entry value can take on two forms. If the value begins with a digit,
track assumes that we wish to log a numerical quantity. In the log entry above,
the log entry has a quantity of `300`, with units `ml`.

The log entry could also be free-form text. This is for logging other random
things, like mood. An example of such a log entry would be:

```text
[2020-10-09T14:52:46.884145110+08:00] mood:good
```

To enter a new entry, track exposes a simple command-line interface via `track
add`, which takes two indexed arguments, the category, and the entry value.

```bash
track add water 300ml
```


## Querying the Log {#querying-the-log}

`track` supports a simple query interface of the form `track query category
num-days`, where `num-days` defaults to 7 (the past week). It:

1.  Filters for entries that are at most `num-days` back, and whose category
    contains `category`.
2.  Sums numerical quantities if the units match. For example, if there were
    two entries on the same day, one for `water:300ml` and the other
    `water:600ml`, track would report `water:900ml`.

This is what I see running `track query water` on my 5 days of log entries.

```text
~ on  master [!]
❯ track query water 7

05 Oct 2020  water      1400ml
06 Oct 2020  water      1600ml
07 Oct 2020  water      1900ml
08 Oct 2020  water      2000ml
09 Oct 2020  water      1700ml
```


## Entering Entries on the Go {#entering-entries-on-the-go}

All is well when I'm at my computer where I have access to a terminal, but what
about when I'm on the move? Because the log format is so simple, I shipped
`track` with a simple Telegram bot, that allowed me to add entries by sending
the bot an entry:

{{< figure src="/ox-hugo/telegram.png" >}}

I host the Telegram bot on my DigitalOcean instance, and run `sshfs` so that
all my writes go the remote track file as well.


## Closing Thoughts {#closing-thoughts}

Right now I have only been tracking for a short while, so I cannot yet comment
whether it will be useful, but this certainly reduces the friction. I'm hoping
to hook some things up so that automatic entries are created (e.g. amount of
sleep, from my Xiaomi Miband).
