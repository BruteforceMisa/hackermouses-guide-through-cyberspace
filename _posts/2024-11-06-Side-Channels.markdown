---
layout: post
title:  "Hardware: Side Channels"
date:   2024-11-06 11:08:02 +0200
categories: hardware
---

<i>Side channels</i> are channels on which information is leaked through the physical properties of the device. These side channels can occur in a more technical setting, but also in a general setting. Examples of general side channels are such as the sound of your keyboard when you are typing in your password, or even the muscles in your hand when you are typing in your pincode when paying. When zooming into the physical components of a device, side channels such as optical emissions, timing delays, electromagnetic emanation and power consumption are observed. For this post, we will zoom in on the power consumption. 

In the previous blog post, it was highlighted that a bit consumes more power when it has the value "1" compared to the value "0". <i> Power traces </i> belonging to this CPU executing code can be obtained by using a oscilloscope, and these traces reflect the values of the bits. By analysis these power traces, it is possible to deduct what the CPU is executing without direct access to the program. Therefore, <i>sensitive information</i> can be obtained by analysing the current flowing through the device. Examples of such sensitive information are passwords or keys of encryption algorithms.

This attack is based on the leakage of information, rather than a mistake in the program or algorithm. Therefore, it is possible to attack mathematically secure cryptograhic algorithms using side channels. 

![image](./assets/images/sidechannel.png) 

<b>Keywords</b>
<ul>
<li>Side channels - channels on which information is leaked through the physical properties of a device </li>
<li>Power traces - the power consumption data of a device when this device is executing a program </li>
<li>Sensitive information - information which should not be publicly known. This can be a key or a password, but also a value derived from such a key</li>

</ul>