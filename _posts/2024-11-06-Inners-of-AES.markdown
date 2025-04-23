---
layout: post
title:  "AES: the Inner Workings"
date:   2024-11-06 12:29:02 +0200
categories: encryption  
---

In this post, we are going to zoom in on the inner workings of one AES block. AES operates in <i>rounds</i>, which are usually 10, 12 or 14 rounds (matching with AES-128, AES-192 and AES-256). The output of each round is xor’ed with a <i>subkey</i>, which is derived from the main key using the key scheduler. How the key scheduler exactly works, is out of the scope for this blog.
AES consists of four main operations: AddRoundKey, SubBytes, ShiftRows & MixColumns. These functions are repeated for the number of rounds. A visualisation of these functions is shown below.

![image](/assets/images/AESinners.png) 

AddRoundKey is the function where the subkey is added to our data. SubBytes is a function where each byte of our data is mapped to another value. ShiftRows and Mixcolumns are functions where our data is shuffled to add dependencies within the encryption for security. The output of one block of AES-128 after 10 rounds, is the ciphertext of this block. As said in the previous posts, depending on the size of the plaintext, this block may be executed multiple times.

In the next post, we will zoom in on the SubBytes function.


<b>Keywords</b>
<ul>
<li>Round - one set of the four main operations done by AES </li>
<li>Subkey - the key used in the AddRoundKey function of AES. This subkey is derived from the main key using the key scheduler  </li>
</ul>