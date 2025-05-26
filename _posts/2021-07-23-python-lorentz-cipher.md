---
layout: post
title: Python Lorentz Cipher
date: 2021-07-23 19:34:46.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- cipher
- cryptography
- lorentz
- python
- ww2
author:
  display_name: deparkes
permalink: "/2021/07/23/python-lorentz-cipher/"
---
The Lorentz cipher was a code used by Germany in the second world war. In this post I wanted to explore the general ideas behind it and see if I could implement a simple Python Lorentz Cipher. I'm not trying to create an exact simulation of the Lorentz cipher here. For a python lorentz cipher simulation suggest you check out <a href="https://github.com/RealGrep/lorenz-cipher-sim">this project on github</a> or if you would like to see a more graphical simulation, <a href="https://lorenz.virtualcolossus.co.uk/LorenzSZ/">this project.</a>
If you want to learn more about the actual Lorentz cipher and how it was used I suggest <a href="http://practicalcryptography.com/ciphers/mechanical-era/lorenz/">here</a> or <a href="https://www.cryptomuseum.com/crypto/lorenz/sz40/index.htm">here</a>:
<a href="https://gist.github.com/deparkes/768754e9902d2444c6c40df988c5fb3c">Go to the Github Gist of the code for this post</a>
<h2>Lorentz Cipher Basics</h2>
The Lorentz cipher was based on an idea developed based on the '<a href="https://cryptomuseum.com/crypto/vernam.htm">Vernam Cipher</a>' . The Vernam Cipher approach can in theory be completely secure if a number of conditions are met. One of the more challenging conditions is the pre-sharing of a number of punch tapes containing truly random digits within which to encrpyt and decrypt the message. A common way to get around this challenge was to use a pseudorandom number generator to produce a <a href="https://en.wikipedia.org/wiki/Keystream">keystream</a> to be combined with the message text to produce the encrypted text. This is the approach taken by the Lorentz cipher.

In modern terminology it is known as an example of a <a href="https://en.wikipedia.org/wiki/Stream_cipher">stream cipher.</a>
The general idea behind a stream cipher is that each character in the plain text message 'stream' is combined with a pseudorandom character from a cipher digit stream.

<h3>The Baudot-Murray code</h3>
The Lorentz cipher system was actually an extension to a <a href="https://en.wikipedia.org/wiki/Teleprinter">teleprinter</a> machine. The teleprinter would convert characters on a type writer with a 5 bit code. The coding scheme typically used in teletype machines was the <a href="https://en.wikipedia.org/wiki/Baudot_code#Murray_code">Baudot-Murray</a> or <a href="https://www.cryptomuseum.com/ref/ita2/index.htm">ITA-2</a> code.

This is a way of encoding characters using 5-bits. It is similar to the <a href="https://computer.howstuffworks.com/bytes1.htm">8-bit byte</a> used in modern computing, but needs to use a shift system to access more than the 32 characters available. Given that there are 26 letters in the English alphabet, 32 characters does not leave much to play with.

Although in reality messages would have actually included characters using the shift codes, for the sake of simplicity I have just used the unshfited codes. The last five codes in the following dictionary are for: NULL, carriage return, linefeed, shift-on, shift-off. The '0b' at the start of each string is for python's <a href="https://stackoverflow.com/questions/46002161/what-does-the-0b-mean-at-the-begining-of-the-byte-0b1100010">binary representation</a>.

```python
baudot = { 'a': '0b00011',
           'b': '0b11001',
           'c': '0b01110',
           'd': '0b01001',
           'e': '0b00001',
           'f': '0b01101',
           'g': '0b11010',
           'h': '0b10100',
           'i': '0b00110',
           'j': '0b01011',
           'k': '0b01111',
           'l': '0b10010',
           'm': '0b11100',
           'n': '0b01100',
           'o': '0b11000',
           'p': '0b10110',
           'q': '0b10111',
           'r': '0b01010',
           's': '0b00101',
           't': '0b10000',
           'u': '0b00111',
           'v': '0b11110',
           'w': '0b10011',
           'x': '0b11101',
           'y': '0b10101',
           'z': '0b10001',
           ' ': '0b00100',
           'N': '0b00000',
           'C': '0b01000',
           'L': '0b00010',
           'F': '0b11011',
           'T': '0b11111'}
```

For a more comprehensive handling of Baudot in python, I suggest looking into <a href="https://python-baudot.readthedocs.io/en/latest/">this project.</a>
<h3>The message</h3>
This is just typed into the type writer-style interface of the teleprinter. The message characters are converted into the the corresponding Baudot-Murray codes. In this simple python version it is done by looping through the message characters and finding the corresponding dictionary values.

```python
Original message:
my secret message
Original Baudot:
11100
10101
00100
00101
00001
01110
01010
00001
10000
00100
11100
00001
00101
00101
00011
11010
00001
```


<h3>The keystream</h3>
In the Lorentz cipher this was generated by a complicated arrangement of dials. In this simple python lorentz cipher we can just use python's <a href="https://docs.python.org/3/library/random.html">random</a> library to <a href="https://stackoverflow.com/questions/2823316/generate-a-random-letter-in-python">generate a random selection of letters</a>. It is worth keeping in mind of course that just in the same way that the the original Lorentz system only used a psuedorandom keystream, so is the python random library only <a href="https://en.wikipedia.org/wiki/Pseudorandomness">pseudorandom</a>.

```python
random_choice_characters = list(baudot.keys())
key_string = ''.join(random.choice(random_choice_characters) for x in range(len(message)))
```

From the original 'my secret message', one run of the code give the corresponding key stream:

```python
Key stream:
CrwbFLFtoiibksNai
```

<h3>Exclusive OR (XOR)</h3>
An essential part of the Lorentz cipher process is carrying out an <a href="https://www.cryptomuseum.com/crypto/vernam.htm">XOR operation</a> on the message and key streams.
In python we can carry out a bit-wise exclusive OR operation with the ^ operator. A binary number in python is indicated by putting '0b' before the numbers.

```python
x = 0b01
y = 0b10
print(bin(x^y))
```

This gives the result '0b11'. We need to explicitly use the '<a href="https://stackoverflow.com/questions/1523465/binary-numbers-in-python#1523581">bin</a>' command otherwise python converts the response to a decimal '3'.
The Lorentz cipher uses 5-bit character codes and we can represent those more completely using string formatting to <a href="https://stackoverflow.com/questions/16926130/convert-to-binary-and-keep-leading-zeros-in-python">zero pad</a> the text and remove the '0b'.
For example if we wanted to

```python
i = 0b00001
print(f"{i:#07b}"[2:7])
```

yields '00001'.
<h3>The Broadcast</h3>
The encrypted message that we will actually broadcast is found by doing an XOR (Exclusive OR) operation on both the plaintext message and the key stream.

```python
broadcast = []
for i, letter in enumerate(message):
    broadcast.append(int(baudot[letter], 2) ^ int(baudot[key_string[i]], 2))
print('\nBroadcast signal: ')
[print(f"{i:#07b}"[2:7]) for i in broadcast]
```

Which for one run of the code gave:

```python
Broadcast signal:
10100
11111
10111
11100
11010
01100
10001
10001
01000
00010
11010
11000
01010
00000
00011
11001
00111
```

<h3>Decoding The Message</h3>
One of the properties of the XOR operation is that it is reversible.
As we receive the letter code and need to find the corresponding letter we need to do a <a href="https://stackoverflow.com/questions/8023306/get-key-by-value-in-dictionary">reverse lookup in the dictionary</a> - i.e. find the <em>key</em> corresponding to a particular <em>value</em>.

```python
received_message = []
for i in broadcast:
    received_message.append(list(baudot.keys())[list(baudot.values()).index(f"{i:#07b}")])
print('\nMessage Received: ')
print(''.join(received_message))
```

The received message is clearly very different from the original:

```
Message Received:
hTqmgnzzCLgorNabu
```

And then to decrypt the message we re-apply the XOR operation:

```python
decrypted_message = []
# Decrypt signal
# Need to XOR with original key_string again
for i, letter in enumerate(received_message):
    decrpyted_code = int(baudot[letter], 2) ^ int(baudot[key_string[i]], 2)
    decrypted_message.append(list(baudot.keys())[list(baudot.values()).index(f"{decrpyted_code:#07b}")])
print('\nMessage Decrypted: ')
print(''.join(decrypted_message))
```

Which gets us back to the original message:

```
Message Decrypted:
my secret message
```

<h3>Going further</h3>
This has been a very simple Python Lorentz Cipher exploration and there are doubtless ways that it could be taken further. One obvious way would be to more accurately represent how the Lorentz Cipher pseudorandom generation worked. Alternatively you could attempt to crack the resulting encrypted message with something like a simple <a href="https://cryptii.com/pipes/caesar-cipher">Caesar cipher</a>.
