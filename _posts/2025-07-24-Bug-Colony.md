---
layout: posts
title:  "Bug colony alert!"
date:  24-07-2025 
tags: hardware
categories: Projects
---

We all complain about bugs in our code, but have you ever seen them in real life? For this project, the digital bug becomes analog! After my internship and master thesis, I wanted to give a small thank-you present to my office mates and supervisors. 

![image]({{ site.url }}{{ site.baseurl }}/assets/images/colony-alert.jpeg)

This present was actually a mini-CTF. I crocheted little bugs using [this](https://www.etsy.com/listing/1014810705/scarab-beetle-amigurumi-crochet-pattern?ls=r&ref=related-3&content_source=4a450a3ca2942274ec83c1716e7293d3%253A7cc3147007296ca04b648f358148d5ea85fd2ab2&logging_key=4a450a3ca2942274ec83c1716e7293d3%3A7cc3147007296ca04b648f358148d5ea85fd2ab2) pattern, and glued them on a small base. At the bottom of a base, I put an NFC sticker.

![image]({{ site.url }}{{ site.baseurl }}/assets/images/nfc-bottom.jpeg)

You can use any app on your phone to read and write such NFC stickers. But to make the CTF a little bit harder, I encoded the message hidden in the sticker. 

To solve the CTF, follow the steps in the spoiler!

<details>
<summary><b>Click to show/hide CTF spoilers</b></summary>
<ul>
<li>Step 1: install any app or use the internal one to read out the NFC sticker </li>

<li>Step 2: Copy the encoded text message </li>

<li>Step 3: Use a tool such as <a href="https://gchq.github.io/CyberChef/">Cyberchef</a> to automatically decode. The message is Base64 encoded. </li>

<li>Step 4: Read the decrypted message! </li>
</ul>
</details>

<br/>
I thought this would be a fun gift for anyone interested in Cyberspace. These bugs are more fun compared to software bugs ;)

![image]({{ site.url }}{{ site.baseurl }}/assets/images/bug.jpeg)