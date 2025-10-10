---
layout: distill
title: Shopkeeper - RL-Agent learning to Balance Inventory and Cash
description: Q-learning agent went from selling apples to managing a warehouse.
tags: gymnasium RL environment python qlearning
giscus_comments: false
date: 2025-09-29
featured: true
mermaid:
  enabled: true
  zoomable: true
code_diff: true
map: true
chart:
  chartjs: true
  echarts: true
  vega_lite: true
tikzjax: true
typograms: true

authors:
  - name: Firstka Faiz Pangestu
    url: "https://ffpangestu.github.io"
    affiliations:
      name: University of Applied Sciences Darmstadt

bibliography: 2025-09-29-shopkeepers-digital-playground.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: The Opening Day
  - name: Expanding Demand
  - name: Warehouse for Lease
  - name: Helpers for Hire
  - name: Customer Behavior
  - name: Lesson Learned
# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
# _styles: >
#   .fake-img {
#     background: #bbb;
#     border: 1px solid rgba(0, 0, 0, 0.1);
#     box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
#     margin-bottom: 12px;
#   }
#   .fake-img p {
#     font-family: monospace;
#     color: white;
#     text-align: left;
#     margin: 12px 0;
#     text-align: center;
#     font-size: 16px;
#   }
---

In this little project, we take a closer look at the transformation of a **simple shop** into a **warehouse environment**<d-cite key="A_Basic_Ai_2025_github"></d-cite>. Using **OpenAI Gymnasium**<d-cite key="Using_The_Api_2025_farama"></d-cite> as the base of our Reinforcement Learning (RL) environment, we can observe how small design tweaks completely shift the agent’s behavior and strategy.

Our agent relies only on a **simple tabular Q-learning algorithm**<d-cite key="Trying_Different_Actions_2025_farama"></d-cite> .No deep learning, no tricks. The rule of the game is simple:

> **Whatever we do, never increase the product price.**

---

## The Opening Day

A new tiny shop opened in the digital world! The humble shop ran a small apple stand with a **maximum inventory of 10 apples**. At the start, it only had **5 apples** and **€5 cash** in hand.

To make things more interesting, the contract only lasted **20 days** (`step: 20`). The mechanics were straightfoward:

- The shopkeeper (agent) could **either sell or restock** in each step.
- The customer could buy **1–3 apples** per step.
- **Selling price:** €3 per apple
- **Restock cost:** €1 per apple
- **Unfulfilled demand penalty:** –€2 per apple

So, the agent had to balance between keeping stock high enough to meet demand and saving cash to avoid unnecessary restocks.

Now for reward and penalties. Because this was the shopkeeper’s first job, he took customer satisfaction seriously. Whenever he couldn’t meet the customer’s demand, he felt guilty — which translated into penalties in our reward system:

- **Successful sale:** +1
- **Failing to meet demand:** –3

These values shaped how the agent learned what “good” and “bad” decisions looked like over time.

With basic Q-learning parameters, the agent ended the simulation with an **average cash of €169.86**. Not bad for the first time, right?

---

## Expanding Demand

Encouraged by his success, the shopkeeper expanded his apple stand operations. The contract was now extended to a **full year** (`step: 20 → 365`), and new customers began to appear. Feeling confident, the shopkeeper agreed to **accept larger orders** — now the customer could buy the **entire stock**! (`max_demand: 3 → max_inventory`)

The result? This simple rule change completely altered the agent’s behavior. Because failing to meet big orders felt much worse than before, the shopkeeper started to **hoard apples** — saving them up for large buyers instead of selling them all at once.

The new setup led to a dramatic jump in profit. The agent achieved an **average cash of €734.33**, showing that even **small changes in environment dynamics** can have **major effects on RL strategies**.

---

## Warehouse for Lease

Bigger orders called for a **bigger inventory** — and so the next logical step was to **lease an entire warehouse**. The maximum inventory increased dramatically from **10 → 100**. However, this upgrade came with a new challenge: every stored unit now incurred a **storage fee**, charged **every step**. In other words, holding too much stock could quietly drain the cash reserves.

This is where things got **interesting (and messy)**. With the new cost structure, the **reward function failed to converge**. The agent simply couldn’t stabilize its learning process.

Instead of growing profits, the **cash balance collapsed** to **€561.86**! The shopkeeper couldn’t figure out the right balance between:

- keeping enough stock to meet big orders, and
- minimizing storage costs that grew with every apple on the shelf.

Realizing something was wrong, the shopkeeper decided to **train longer** for a whopping **100,000 episodes**. This extended training period helped the agent adapt to the new, more complex environment.

The result? **Average cash improved** to **€847.55**, but the **reward values remained negative**. Even worse, the agent only used **30% of the available inventory**, meaning it was still **leaving a lot of money on the table**.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/0.2.1.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
  The stock balance and cash growth.
</div>

---

## Helpers for Hire

It soon became clear that with a bigger warehouse, the shopkeeper couldn’t manage everything alone. To keep up with demand, he decided to **hire helpers**. These helpers **multiplied the restocking rate**, allowing the warehouse to refill much faster, but they also came with a price: **€1 per helper per step**.

To manage them, the shopkeeper gained **two new actions**:

- **Hire a helper** (up to 5 total)
- **Fire a helper**

The first results were a disaster. The agent went wild, hiring and firing helpers recklessly without considering the overall cash flow. As a result, the **average cash plummeted to –€480**. The warehouse became a financial mess but full of apples.

To encourage smarter management, a **penalty for firing workers (–5)** was introduced. This change nudged the agent to retain helpers longer and think twice before letting them go. Then came another training session, this time for **200,000 episodes**. Finally, it clicked.

The result was remarkable: **Average cash soared to €1,369.** The shopkeeper had finally mastered the art of **balancing workforce, stock, and cost**.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/0.3.4.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
  Maximizing helpers effectiveness.
</div>

---

## Customer Behavior

After a long time in business, the shopkeeper began to **notice something curious**: customer demand wasn’t completely random. It seemed to follow a **pattern**, more like a **normal distribution** than uniform chaos.

To capture this insight, the environment was updated to model demand accordingly:

```python
base = (self._min_demand + self._max_demand) / 2
self.customer = self.np_random.normal(base, 5, self.max_step).astype(int)
self.customer = np.clip(self.customer, self._min_demand, self._max_demand)
```

The results produced the best performance: **€1,540** average cash.

---

## Lesson Learned

After several iterations, experiments, and plenty of failed training runs, the shopkeeper’s journey revealed a few key lessons about reinforcement learning design:

1. **Reward shaping can completely change agent behavior.** Even a small adjustment in rewards or penalties can flip the agent’s entire strategy, From cautious hoarding to aggressive selling. Reward functions should always align closely with the true goals of the environment.

2. **Add complexity carefully.** Each new mechanic (storage costs, helpers, or customer demand) initially _breaks_ the agent. When the environment changes, the learning dynamics must be rebalanced through parameter tuning, normalization, or new reward terms.

3. **Reducing randomness improves learning.** By modeling customer demand using a **normal distribution** instead of uniform randomness, the agent’s decisions became more stable and interpretable. A more predictable environment helps the agent learn patterns instead of chasing noise.
