---
layout: post
title:  "AI: Learning the Decision Boundary"
date:   2024-11-06 12:46:02 +0200
categories: ai
---

Instead of using regular statistics to detect the decision boundary, we can try to learn the function iteratively. This is where <i>neural networks</i> come in handy. By using deep neural networks, we are repeating our statistical analysis iteratively depending on our data.

For example, suppose we have a coffee which is medium bitter and has a lighter colour. When the function is learning, it might misclassify this coffee as tea. Based on this new datapoint, we have to correct the decision boundary. This process - called <i>gradient descent</i> - is repeated many times, until the most optimum decision boundary is found. This means that most datapoints are classified correctly.

![image](./assets/images/Decisionboundary.png) 

Finding a deep neural network with the best decision boundary is therefore an <i>optimisation problem</i>. This can be calculated mathematically (from high school mathematics, you might recall finding global and local minima/maxima using the derivatives). However, it can be the case that there exist multiple minima. Finding the global minimum is one of the challenges in learning such a function.

![image](./assets/images/Optimum.png) 


<b>Keywords</b>
<ul>
<li>Neural network - a technique inspired on the human brain designed for finding patterns in data</li>
<li>Gradient descent - a technique for finding the optimum of a function interatively</li>
<li>Optimisation problem - the problem of finding the best solution from all feasible solutions</li>
</ul>