+++
title = "Machine Learning with guild.ai"
author = ["Jethro Kuan"]
lastmod = 2019-12-27T23:57:31+08:00
draft = false
math = true
+++

Since I've been writing on the topic of workflows and tooling, I
thought I'd give one of my favourite packages, [guild.ai](https://guild.ai/), a shout-out,
and well-deserved exposure.

Guild.ai is designed for managing machine learning experiments. It
provides ways to track experiment runs, make runs reproducible, and
compare runs with different hyperparameters, all in ways that are
non-intrusive. Those who know me know I care a lot about my tools, and
this is one of those tools that really spark joy. It's no surprise
that the author of this package, [Garrett Smith](https://github.com/gar1t), comes from a systems
engineering background. Garrett is also highly responsive on Slack,
actively listening to the users, and provides support.


## The Competition {#the-competition}

While there is [no shortage of machine learning tooling](https://medium.com/@hadyelsahar/how-do-you-manage-your-machine-learning-experiments-ab87508348ac), guild.ai takes
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

Guild.ai cleanly uses default Python functionality, allowing one to
get started without any modification to training scripts. This also
makes guild.ai a nice, non-committal choice.I use command-line
arguments from `argparse` as configuration flags. Guild.ai also has
first-class support for Tensorboard, which is a popular and powerful
choice.


## Experiment Tracking with Guild.ai {#experiment-tracking-with-guild-dot-ai}

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

It even supports the Tensorflow HParam view, which is designed for
comparing runs with differing hyperparameters.

Guild.ai supports a SQL-like filtering interface to allow the user to
choose which runs to load and compare.


## Hyperparameter Search {#hyperparameter-search}

Guild.ai supports multiple methods for hyperparameter search:

1.  Grid search
2.  Random search
3.  Bayesian Optimization

This can be specified easily via the CLI:

```bash
guild run train.py x=[-0.5,-0.4,-0.3,-0.2,-0.1]
```

Hyperparameter search and reproducibility is especially important in
Reinforcement Learning, and guild.ai has made this extremely simple.


## Deployment {#deployment}

Since I'm using guild.ai within a research project, I'm not using
these features. But Guild.ai supports [packaging](https://guild.ai/docs/packages/), allowing for model
collaboration, sharing and reuse.


## Conclusion {#conclusion}

I'm pleased with guild.ai as is, and the author is actively working on
bringing improvements to the tool. I highly recommend machine learning
practitioners to give it a whirl.
