---
layout: distill
title: Shopkeeper's Journey in the Simulated Environment
description: A humble beginning for a humble RL-environment
tags: gymnasium RL-environment python
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
  - name: Opening Day
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

In this little project we will look deeper into the transformation of a simple shop to a warehouse environment. Using Openai Gymnasium as the base of our RL environment we can observe how small tweaks can shift agent strategy. The agent however, will only use simple tabular Q-learning algorithm. The rule is simple: whatever we do, **never increase the product price**.

## The Opening Day

A new tiny shop opened in the digital world! The humble shop ran an apple stand with a maximum inventory of 10 apples. In the beginning, it only had 5 apples and 5€ cash in hand. Each day (Episode) only lasted 20 steps before it closed. The mechanics were straightfoward:

- The shopkeeper (agent) could only either sell or restock for each step
- The customer could buy 1-3 apples per step
- Sell products to customer: €3 per apple
- Restock the inventory: €1 per apple
- If customer demand is not fulfilled: -€2 per apple

With basic Q-learning parameters, the agent earned cash of €164.76. Not bad for the first day of the job right?

---
