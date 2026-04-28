# Computer Vision in Trading System Research

This case study describes how I experimented with computer vision inside a trading system research workflow, and how that process led me to a much stronger development pipeline.

The main objective was not to "predict the market with AI," but to solve a practical research problem: some trade situations looked visually different to me, yet I could not describe that difference well enough through rule-based features alone.

## Goal

To detect complex candlestick formations that were difficult to formalize with structured features, and later use them as trade filters.

## Starting Point

By the time I decided to try computer vision in trading research, I had already been working on one specific trading strategy for about **9 months**.

The initial version of the trading system itself was built relatively quickly, in roughly **3-4 weeks**. The much longer part of the process came afterward: for around **8 months**, I was trying to filter trades and improve the system enough to make it more suitable for live trading.

In its original form, the system was already profitable on the **2023-2025** segment, but on the longer **2015-2022** period it was roughly flat. That was an important lesson by itself: a strategy can look promising in a recent period and still fail to show enough consistency across a broader sample.

At that stage, I was also much less experienced as a researcher. I did not yet fully understand how to validate a strategy properly, and I did not have a mature research infrastructure in place.

## Phase 1 - Building Research Infrastructure First

Before computer vision became the focus, one important step happened first: I realized that every trade needed to be treated as a research object.

That meant building infrastructure to log structured information for each trade:

* trade-level features
* market structure conditions
* session-related context
* risk-reward characteristics
* trade outcomes

This changed the way I worked.

Instead of reviewing trades only visually, I could now export a dataset and ask a much more useful question:

**Can these signals be improved through filtering, segmentation, and quantitative comparison?**

That became one of the foundations of my current research process.

## Phase 2 - Trying to Improve the Strategy with Features

Once the feature infrastructure was in place, I spent a long time trying to improve the strategy through structured variables.

I created and tested many filters based on the information I was able to code explicitly. Some of them were useful. Some helped me identify stronger subsets. But eventually I ran into a limit.

The core issue was simple:

**the features I had coded did not fully describe the visual context of the setup.**

There were trade situations that looked meaningfully different to me when I reviewed charts manually, but I could not explain that difference precisely enough in words or convert it into reliable rule-based logic.

That was the point where the idea of using computer vision became practical.

It was not driven by hype. It was driven by a concrete research bottleneck.

At that stage, I had already spent around **8 months** working on the same strategy, and I gave myself a clear condition:

> If this direction still does not produce something meaningful, I move on to the next strategy.

## Phase 3 - Preparing the Infrastructure for Computer Vision

To test the idea properly, I first had to prepare the data pipeline.

I built infrastructure to collect chart images for each trading situation. This was an important step because it connected the visual representation of the setup to the underlying trade record.

Now each trade could be represented in two ways:

1. as a row of structured features,
2. as a chart image showing the price context.

This was the moment when the research workflow became much more flexible. I was no longer limited to tabular features only.

## Phase 4 - First Computer Vision Attempt: Profit vs Loss

My first approach was straightforward.

I trained a pretrained **ResNet18** model with a binary objective: **profit vs loss**.

The idea was simple: show the model chart images and ask whether it could distinguish winning trades from losing trades.

This approach did **not** lead to the kind of result I needed.

The problem was not just model quality. The deeper problem was the framing of the task itself.

I was treating the entire signal set as one common pool, even though the setups inside it were not truly homogeneous. In other words, I was asking the model to learn a broad and noisy classification problem from a signal family that likely contained multiple different subtypes.

That was a major turning point.

I realized that using computer vision "all together" on the full signal set was too broad. The better idea was to split the signals into **subgroups** and try to detect visually coherent clusters instead.

## Phase 5 - Switching from Global Classification to Subgroup Detection

After that, I changed the objective.

Instead of trying to classify all trades as profit vs loss in one step, I started looking for **visually similar subsets**.

The new idea was:

* first identify a subgroup of setups that looked similar,
* then test whether a model could detect that subgroup,
* and only after that evaluate whether the subgroup was actually useful from a trading perspective.

This worked much better.

I collected the first visually coherent cluster manually and trained the model to detect it.

This was my first real success with computer vision in trading research:

**one subgroup was indeed detectable by the model.**

That result mattered a lot. It showed that computer vision could extract something meaningful from chart images when the task was framed properly.

## Phase 6 - The Unexpected Result

There was one more important twist.

When I selected the first cluster for training, I originally believed it was a **potentially bad cluster** from a trader's perspective. Visually, it looked like a subset I would probably want to filter out.

But after testing it, I found the opposite:

**the cluster turned out to be profitable.**

This created a strong internal contradiction.

My visual trading intuition said one thing, but the actual data said something else.

That contradiction became one of the most valuable moments in the entire project.

## Phase 7 - From Computer Vision to Hand Labeling and Manual Validation

This unexpected result pushed me toward a much more serious question:

**Can I actually predict which setups are strong and which are weak before the trade, or am I only seeing patterns after the outcome is known?**

That question led me to hand labeling and manual validation.

I began reviewing chart screenshots and assigning labels based on what I believed would happen next, without relying on the final trade outcome.

This process revealed something important:

**the signal inside this trading system was much more chaotic than I had assumed.**

In many cases, my labels as a trader did not match the eventual market result. I could not reliably predict whether a given trade would succeed or fail.

That was a critical discovery.

It meant that the problem was not only about missing features or missing model capacity. The deeper issue was that the underlying signal itself lacked the level of predictability I had originally assumed.

## What This Project Changed in My Research Process

This project was valuable not because it produced a final deployable model, but because it changed the way I evaluate trading ideas.

It helped shape my current research pipeline:

1. **Build the strategy baseline** and test it across a meaningful historical period.
2. **Log trade-level features** so each trade can be studied systematically.
3. **Try structured filtering first** before moving to more complex modeling.
4. If structured features fail to capture important context, consider whether **visual information** contains additional signal.
5. Avoid broad labels like profit vs loss when the signal family is too mixed; instead, search for **subgroups and clusters**.
6. Use **hand labeling and manual validation** to check whether the setup is actually predictable before investing more time into modeling.
7. Be ready to reject the strategy entirely if the signal itself turns out to be too chaotic.

## Conclusion

This computer vision experiment did not lead to a production-ready trading model.

However, it gave me something more important at that stage: a much better understanding of how to research trading systems properly.

It showed me that:

* computer vision can be useful in trading research when the task is framed correctly,
* structured features and visual models should complement each other rather than compete,
* subgroup detection can be more meaningful than broad outcome classification,
* and most importantly, manual validation can reveal when a signal is fundamentally too chaotic to justify further development.

In practice, this project helped me do two things:

* improve my research infrastructure,
* and kill a trading system that was not predictable enough to deserve more time.

That was one of the projects that pushed me toward the research process I use now.
