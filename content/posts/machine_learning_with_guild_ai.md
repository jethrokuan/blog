+++
title = "Machine Learning with Guild AI"
author = ["Jethro Kuan"]
date = 2019-12-31T00:00:00+08:00
lastmod = 2020-07-17T00:50:30+08:00
tags = ["ml"]
draft = false
math = true
+++

Since I've been writing on the topic of workflows and tooling, I
thought I'd give one of my favourite packages, [Guild AI](https://guild.ai/), a shout-out,
and well-deserved exposure.

Guild AI is designed for managing machine learning experiments. It
provides ways to track experiment runs, make runs reproducible, and
compare runs with different hyperparameters, all in ways that are
non-intrusive. Those who know me know I care a lot about my tools, and
this is one of those tools that really spark joy. It's no surprise
that the author of this package, [Garrett Smith](https://github.com/gar1t), comes from a systems
engineering background. Garrett is also highly responsive on Slack
and the community site [my.guild.ai](https://my.guild.ai),
actively listening to the users, and provides support.


## The Competition {#the-competition}

While there is [no shortage of machine learning tooling](https://medium.com/@hadyelsahar/how-do-you-manage-your-machine-learning-experiments-ab87508348ac), Guild AI takes
a minimal and un-intrusive approach towards instrumenting the training
scripts. Take [Sacred](https://github.com/IDSIA/sacred/) for example. It requires instrumenting the Python
training script with decorators:

```python

from sacred import Experiment
ex = Experiment('iris_rbf_svm')

@ex.config
def cfg():
  C = 1.0
  gamma = 0.7

@ex.automain
def run(C, gamma):
  iris = datasets.load_iris()
  # ...
```

Scalar logging for Sacred is also a custom module within Sacred, and
visualizing these scalars is done through custom frontends like
Omniboard.

Guild AI cleanly uses default Python functionality, allowing one to
get started without any modification to training scripts. This also
makes Guild a nice, non-committal choice. I use command-line
arguments from `argparse` as configuration flags. Guild also has
first-class support for TensorBoard, which is a popular and powerful
choice.


## Experiment Tracking with Guild AI {#experiment-tracking-with-guild-ai}

Each run of the training script is tracked, by running them through
the intuitive guild CLI. The run processes are tracked by Guild.

{{< figure src="/ox-hugo/screenshot2019-12-27_23-38-54_.png" caption="Figure 1: `guild runs` shows experiments I've run" >}}

Guild even ships with a beautiful web interface that allows you to
view run files (model checkpoints, logs etc.), accessible via `guild view`.


## Comparing Runs {#comparing-runs}

I use `guild tensorboard -C` to load Tensorboard for all my completed
runs (`-C`).

```bash
jethro@server1-CLeAR: ~/projects/snnrl$ guild tensorboard -C
Preparing runs for TensorBoard
TensorBoard 2.1.0 at http://server1-CLeAR:52675 (Press CTRL+C to quit)
```

{{< figure src="/ox-hugo/screenshot2019-12-27_23-44-20_.png" caption="Figure 2: Tensorboard scalars across multiple runs" >}}

It even supports the TensorFlow HParam view, which is designed for
comparing runs with differing hyperparameters.

Guild AI supports a SQL-like filtering interface to allow the user to
choose which runs to load and compare.


## Hyperparameter Search {#hyperparameter-search}

Guild AI supports multiple methods for hyperparameter search:

1.  Grid search
2.  Random search
3.  Bayesian Optimization

This can be specified easily via the CLI:

```bash
guild run train.py x=[-0.5,-0.4,-0.3,-0.2,-0.1]
```

Hyperparameter search and reproducibility is especially important in
Reinforcement Learning, and Guild has made this extremely simple.


## Deployment {#deployment}

Since I'm using Guild AI within a research project, I'm not using
these features. But Guild supports [packaging](https://my.guild.ai/docs/packages/), allowing for model
collaboration, sharing and reuse.


## Conclusion {#conclusion}

I'm pleased with Guild AI as is, and the author is actively working on
bringing improvements to the tool. I highly recommend machine learning
practitioners to give it a whirl.
