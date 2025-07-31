---
name: Recamán's sequence viz
tools: [python, fun]
order: 6
image: ../assets/figs/recaman_circle_65cb.png
description: "Python-generated visualization of Recamán’s sequence, inspired by a Numberphile video. Arcs, loops, and a surprisingly elegant pattern from a simple rule: subtract n if you can, add it if you can’t."
---

# Recamán's sequence viz
- [Jupyter Notebook: Recamán's sequence](https://github.com/nataquinones/ludus/blob/master/recamans/recaman.ipynb)

I’ve always liked cool visualizations, and this one really caught my eye in a [Numberphile video about Recamán’s sequence](https://www.youtube.com/watch?v=FGC5TdIiT9U). The [sequence itself](http://oeis.org/wiki/Recam%C3%A1n%27s_sequence) is simple but surprisingly beautiful: starting at 0, at each step n, try to **subtract n** from the current number. If the result is positive and hasn’t appeared before, use it, if not, **add n** instead. The result is a bouncy, non-repeating sequence full of visual rhythm.

In the video, Edmund Harriss draws the sequence as a series of connected semicircles, each number in the sequence arcs to the next, alternating up and down. In this notebook, I recreate that diagram programmatically using Python. It’s a fun way to explore how simple rules can lead to unexpectedly elegant patterns.


<img src="../assets/figs/recaman_circle_65cb.png" width="100%"/>