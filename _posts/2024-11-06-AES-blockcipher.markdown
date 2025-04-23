---
layout: post
title:  "Introduction to AES: a Block Cipher"
date:   2024-11-06 12:27:02 +0200
tags: encryption
categories: infographics
---

AES (Advanced Encryption Standard) is the NIST-standard for encrypting data and is widely used. AES is a <i>block cipher</i>, which means that the data is encrypted per block. For example, AES-128 denotes that each <i>plaintext</i> is split into blocks of 128 bits and uses a 128-bit <i>key</i> for <i>encryption</i>.

For example, suppose we want to encrypt the plaintext “Hello world, how are you?”. For now, we will consider each character to be represented in 1 byte (= 8 bits). To correctly encrypt our plaintext, it will be split into the following sets:

[hello world, how] + [ are you?]

The first block is exactly 16 bytes, but the second block is 7 bytes short. In AES, 7 bytes of padding will be added to match the block size. For now, we will denote padding as “p”. The schematic for encrypting looks as follows:
[hello world, how] + [ are you?ppppppp]

Each AES block has as input the plaintext and the key, and outputs a <i>ciphertext</i>. The key is derived from the password chosen by the user. A schematic of AES encryption is shown below.

![image](https://bruteforcemisa.github.io/hackermouses-guide-through-cyberspace/assets/images/AESBlockcipher.png) 

<b>Keywords</b> 
<ul>
<li>Block cipher - an encryption mechansim where plaintexts are divided in blocks before encrypting</li>
<li>Ciphertext - the text after encryption, which is only decodable for parties having access to the key</li>
<li>Encryption - technique for encoding information in such a way that only authorised parties can obtain the content </li>
<li>Key - the secret value used for encoding & decoding information </li>
<li>Plaintext - the text before encryption, readable for all parties </li>

</ul>