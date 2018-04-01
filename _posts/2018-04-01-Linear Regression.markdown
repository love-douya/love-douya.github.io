---
layout: post
title:  "Linear Regression"
date:   2018-4-1 15:28:00
categories: Algorithm Machine Learing
tags: Algorithm Machine Learning Linear Regression
mathjax: true
---

* content
{:toc}

## Step 0
The parameters t1 t2 are set to 0

## Step 1
Calculate the hypothesis for each data point

## Step 2
Calculate the cost function

$$
E(\theta_0, \theta_1) = \frac{1}{2m}\sum_{i = 1}^m\left(h_i(x) - y_i\right)^2
$$



## step 3
Calculate the partial derivatives of the cost function with respect to parameters

$$
\frac{\partial E(\theta_0, \theta_1)}{\partial \theta_0} = \frac{1}{m}\sum_{i=1}^m\left(h_i(x) - y_i\right)
$$
