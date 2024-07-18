---
title: "McLaurin inequality"
draft: false
tags:
  - 
---
 
## Question
Let $x, y, z$ be positive real numbers such that $x+y+z=1$ and $xy+yz+xz=\frac{1}{3}$.

What is the value of $\frac{4x}{y+1} + \frac{16y}{z+1} + \frac{64z}{x+1}$?

[Asked on Quora](https://www.quora.com/Let-x-y-z-be-positive-real-numbers-such-that-x-y-z-1-and-xy-yz-xz-frac-1-3-What-is-the-value-of-frac-4x-y-1-frac-16y-z-1-frac-64z-x-1)

## Answer
We can directly compute the values of x, y, and z from the first two equations using [Maclaurin’s inequality](https://en.wikipedia.org/wiki/Maclaurin%27s_inequality). It is a refinement of the arithmetic-geometric mean inequality and says that for positive x, y, z we have

$$\frac{x+y+z}{3} \geq \sqrt{\frac{xy+yz+xz}{3}} \geq \sqrt[3]{xyz}$$

with equality only if $x=y=z$. But since

$$\frac{1}{3} = \frac{x+y+z}{3} \geq \sqrt{\frac{xy+yz+xz}{3}} = \sqrt{\frac{1}{9}} = \frac{1}{3},$$

we must have equality giving $x=y=z=\frac{1}{3}$. Now we only have to plug in the values to obtain

$$\frac{4x}{y+1} + \frac{16y}{z+1} + \frac{64z}{x+1} = \frac{\frac{84}{3}}{\frac{4}{3}} = 21$$

Here, Terence Tao published a [blog post](https://terrytao.wordpress.com/2023/10/10/a-maclaurin-type-inequality/) (and research paper) related to Maclaurin’s inequality.
