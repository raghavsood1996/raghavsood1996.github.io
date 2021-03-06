---
layout: post
title: Learning to Use Adaptive Motion Primitives in Search Based Planning for Navigation
subtitle: IROS 2020
bigimg: /img/car.jpg
gh-repo: raghavsood1996/learn_adaptive_primitves
gh-badge: [star, fork, follow]
tags: [Motion Planning, Deep Learning, Research]
comments: true
---
<div style="text-align:justify">
Heuristic-based graph search algorithms like A* are frequently used to solve motion planning problems in many domains. For most practical applications, it is infeasible and unnecessary to pre-compute the graph representing the whole search space. Instead, these algorithms generate the graph incrementally by applying a fixed set of actions (frequently called *motion primitives*) to find the successors of every node that they need to evaluate. In many domains, it is possible to define actions (called *adaptive* motion primitives) that are not pre-computed but generated on the fly. The generation and validation of these adaptive motion primitives is usually quite expensive compared to pre-computed motion primitives. However, they have been shown to drastically speed up search if used judiciously. In prior work, ad hoc techniques like fixed thresholds have been used to limit unsuccessful evaluations of these actions. In this paper, we propose a learning-based approach to make more intelligent decisions about when to evaluate them. We do a thorough empirical evaluation of our model on a 3 degree-of-freedom (dof) motion planning problem for navigation using the Reeds-Shepp path as an adaptive motion primitive. Our experiments show that using our approach in conjunction with search algorithms leads to over 2x speedup in planning time.

</div>

Please find the full text of paper [here](https://www.researchgate.net/publication/343215060_Learning_to_Use_Adaptive_Motion_Primitives_in_Search-Based_Planning_for_Navigation).