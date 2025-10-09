---
layout: distill
title: Shopkeeper's Journey in the Simulated Environment
description: A humble beginning for a humble RL-environment
tags: gymnasium RL environment python qlearning
giscus_comments: false
date: 2025-09-29
featured: true

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

In this little project, we take a closer look at the transformation of a **simple shop** into a **warehouse environment**.  
Using **OpenAI Gymnasium** as the base of our Reinforcement Learning (RL) environment, we can observe how small design tweaks completely shift the agent’s behavior and strategy.

Our agent relies only on a **simple tabular Q-learning algorithm** — no deep learning, no tricks.  
The rule of the game is simple:

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

---
