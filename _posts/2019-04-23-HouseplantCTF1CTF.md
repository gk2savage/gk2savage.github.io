---
title:     "Houseplant CTF 2020"
tags: [ctf,jeopardy,easy]
categories: CTF
---

![](/img/houseplantctf2020/hpctf.png)

Houseplant CTF is a Capture The Flag event made by RiceTeaCatPanda developers.

CTF Link: [https://houseplant.riceteacatpanda.wtf/](https://houseplant.riceteacatpanda.wtf/home)

Flag Format: rtcp{.\*}

This was a fun beginner-friendly Jeopardy based Capture the Flag event. Me(@gk2savage) and my [TEAM](https://ctftime.org/team/80844) had very much fun playing it and spent some solid hours on this.

I have only posted writeups of the challenges that i did myself so you won't find every challenge solved here. Obviously I played it for prizes lol 🤣

![](/img/houseplantctf2020/misc1.png)

🍚 wholesome ctf intensifies 🍚

Beginners
---------

Beginner 1
----------

![](/img/houseplantctf2020/b1.png)

Solution:

"cnRjcHt5b3VyZV92ZXJ5X3dlbGNvbWV9" is a Base64 String so decode it with Base64 decoder.

**

Flag : rtcp{youre\_very\_welcome}

**

Beginner 2
----------

![](/img/houseplantctf2020/b2.png)

Solution:

"72 74 63 70 7b 62 6f 62 5f 79 6f 75 5f 73 75 63 6b 5f 61 74 5f 62 65 69 6e 67 5f 65 6e 63 6f 75 72 61 67 69 6e 67 7d"

Convert this Hex to ASCII with "HEX to ASCII" decoder.

**

Flag : rtcp{bob\_you\_suck\_at\_being\_encouraging}

**

Beginner 3
----------

![](/img/houseplantctf2020/b3.png)

Solution:

"162 164 143 160 173 163 165 145 137 155 145 137 151 137 144 151 144 156 164 137 153 156 157 167 137 167 150 141 164 137 157 143 164 141 154 137 167 141 163 137 157 153 141 171 77 41 175"

Convert this Octal String to ASCII

**

Flag : rtcp{sue\_me\_i\_didnt\_know\_what\_octal\_was\_okay?!}

**

Beginner 4
----------

![](/img/houseplantctf2020/b4.png)

Solution:

"egpc{lnyy\_orggre\_cnegvpvcngr}"

This is a Caesar Cipher with 13 Shift or also known as "ROT13"

**

Flag : rtcp{yall\_better\_participate}

**

Beginner 5
----------

![](/img/houseplantctf2020/b5.png)

Solution:

"-- .- -. -.-- ..--.- -... . . .--. ... ..--.- .- -. -.. ..--.- -... --- --- .--. ..."

This is a Morse Code. Decode it with an Online Decoder.

**

Flag : rtcp{many\_beeps\_and\_boops}

**

Beginner 6
----------

![](/img/houseplantctf2020/b6.png)

Solution:

"26 26 26 26 26 26 26 26 19 12 5 5 16 9 14 7 9 14 16 8 25 19 9 3 19"

This is an A1Z26 Cipher which is very simple direct substitution cipher, where each alphabet letter is replaced by its number in the alphabet.

**

Flag : rtcp{zzzzzzzzsleepinginphysics}

**

Beginner 7
----------

![](/img/houseplantctf2020/b7.png)

Solution:

"igxk{fmovhh\_gsvb\_ziv\_nvzm}"

This is an Atbash cipher which is a substitution cipher with a specific key where the letters of the alphabet are reversed. i.e. all 'A's are replaced with 'Z's, all 'B's are replaced with 'Y's, and so on.

**

Flag : rtcp{unless\_they\_are\_mean}

**

Beginner 8
----------

![](/img/houseplantctf2020/b8.png)

Solution:

"00110 01110 00100 00000 10011 00101 01110 01110 00011 00011 01110 01101 10011 10010 10011 00000 10001 10101 00100"

This is a Bacon cipher which is a biliteral substitution alphabet which replace a character with a group of 5 formed with two letters, generally A and B.

So we convert all the 0's to A's and 1's to B's. And then we will decode this Bacon Cipher.

"AABBA ABBBA AABAA AAAAA BAABB AABAB ABBBA ABBBA AAABB AAABB ABBBA ABBAB BAABB BAABA BAABB AAAAA BAAAB BABAB AABAA"

**

Flag : rtcp{GOEATFOODDONTSTARVE}

**

Beginner 9
----------

![](/img/houseplantctf2020/b9.png)

Solution:

This time we get a file named "Beginner 10.txt". It actually consists of all the challenges we done before.

As the hint says, we go to cyberchef to cook our recipe to decode this.

![](/img/houseplantctf2020/b90.png)**

Flag : rtcp{nineornone}

**

Crypto
------

CH₃COOH
-------

![](/img/houseplantctf2020/c1.png)

Solution:

This is a Vigenère cipher which can be decoded with a key. As the hint suggests, the key is short so we can try bruteforcing it with an online decoder.

![](/img/houseplantctf2020/c10.png)

We get the key "tony" for the cipher. Decode it to get the flag.

**

Flag : rtcp{vinegar\_on\_my\_fish\_and\_chips\_please}

**

"fences are cool unless they're taller than you" - tida
-------------------------------------------------------

![](/img/houseplantctf2020/c2.png)

Solution:

As the name suggest, This is a Rail Fence Cipher (also called zigzag cipher) which is a form of transposition cipher

With Rails: 3 and Offset: 3, we can get our flag.

![](/img/houseplantctf2020/c20.png)**

Flag : rtcp{ask\_tida\_about\_rice\_washing}

**

Broken Yolks
------------

![](/img/houseplantctf2020/c3.png)

Solution:

"smdrcboirlreaefd"

This ciphertext is scrambled. Upon trying online decoders, found that words that are related to the question and made sense for it were "descrambler", "descrambled", "scrambled", "fried" etc.

Tried different flags until finally found the one.

**

Flag : rtcp{scrambled\_or\_fried}

**

Sizzle
------

![](/img/houseplantctf2020/4.png)

Solution:

Download the "encoded.txt" and you will find Morse Code written in it. But if we try to decode it, we get nothing meaningful.

As the challenge suggests, it looks like a Bacon Cipher as all the morse codes are in group of 5. So we change all the "."s to "A"s and "-"s to "B"s

If we try decoding it with a bacon cipher now, we will get the flag.

![](/img/houseplantctf2020/c40.png)

We will wrap the flag with rtcp{}, use all lowercase, and separate words with underscores.

**

Flag : rtcp{bacon\_but\_grilled\_and\_morsified}

**

Parasite
--------

![](/img/houseplantctf2020/c5.png)

Solution:

This was a lovely challenge. As you can see in the description, some letters are capitalised. We get "SKATS" from it, and searching it we get that SKATS stands for Standard Korean Alphabet Transliteration System.

Also the name "Parasite" comes from Oscar-winning 2019 South Korean black comedy thriller film and the challenge has resemblance to the plot of the story. NICE:)

![](/img/houseplantctf2020/c50.png)

First we convert the Morse Code to ASCII. The ASCII is then converted to Hangul with the SKATS table relating the corresponding parts.

![](/img/houseplantctf2020/c52.png)

Convert the Hangul to English with Google Translater. You may have to remove some Hangul letters from the end as they don't convert into English unless they make sense.

It also signifies the fact that those last Hangul letters are symbolising 'Parasite' as they don't let you see the flag until you remove them.

"ㅎㅡㅣㅁㅏㅇㅇㅡㄴㅈㅣㄴㅈㅓㅇㅎㅏㄴㄱㅣㅅㅐㅇㅊㅜㅇㅇ" is converted to "Hope is a true parasite"

![](/img/houseplantctf2020/c51.png)**

Flag : rtcp{Hope\_is\_a\_true\_parasite}

**

Rainbow Vomit
-------------

![](/img/houseplantctf2020/c6.png)

Solution:

Download the "output.png" and as the hints tell us, this is "Hexahue" invented by Josh Cramer.

![](/img/houseplantctf2020/c60.png)

To manually do the challenge is very time-consuming, but upon closer inspection, all the 6 (2x3) blocks represent an alphabet, number or commas.

In the end line, we can see that lot of hexahue blocks are stacked together meaning our flag might be at the end. Only trying the last line, we get "s one rtcp should,fl5g4,b3,st1cky,or,n0t" which is the flag.

![](/img/houseplantctf2020/c61.png)**

Flag : rtcp{should,fl5g4,b3,st1cky,or,n0t}

**

Forensics
---------

Neko Hero
---------

![](/img/houseplantctf2020/f1.png)

Solution:

Download the "advertisement.png" file and check it.

![](/img/houseplantctf2020/f10.png)

Open the image with "stegsolve.jar" and check "Green Plane 0". You will find the another hidden image with flag.

![](/img/houseplantctf2020/f11.png)**

Flag : rtcp{s4ve\_@LL\_7h3m\_c4tG1Rl$}

**

Misc
----

Rules
-----

![](/img/houseplantctf2020/m1.png)

Solution:

It says "Please read the rules." so that's we are going to do.

![](/img/houseplantctf2020/m10.png)**

Flag : rtcp{this\_is\_not\_a\_flag\_i\_think}

**

Spilled Milk
------------

![](/img/houseplantctf2020/m2.png)

Solution:

Download the "spilled\_milk.png" file and check it.

It is a total white image until you check it with "stegsolve.jar".

![](/img/houseplantctf2020/m21.png)**

Flag : rtcp{Th4nk$\_f0r\_h3LP1nG!}

**

Zip-a-Dee-Doo-Dah
-----------------

![](/img/houseplantctf2020/m3.png)

Solution:

Download the passwords file given in hint.

  [SecLists/Passwords/xato-net-10-million-passwords-100.txt](https://github.com/danielmiessler/SecLists/blob/master/Passwords/xato-net-10-million-passwords-100.txt)

The file "1819.gz" is zipped too many times and we need to make a script for it. Also upon somewhat manual extraction and experimentation, i found that:

1\. The file is zipped continously in .tar , .gz and .zip format.

2\. Only .zip files has password on it, which need to be cracked with the above password wordlist.

So I made a little handy "bash" script for it. (pass is the wordlist above)

![](/img/houseplantctf2020/m30.png)

It automates the process of unzipping and cracking passwords and gives "0.gz" which has flag.txt

**

Flag : rtcp{z1pPeD\_4\_c0uPl3\_t00\_M4Ny\_t1m3s\_a1b8c687}

**

Survey
------

![](/img/houseplantctf2020/m4.png)

Solution:

Well, Even the "Survey" was a little challenge on it's own. After you fill the Survey, you will get this.

![](/img/houseplantctf2020/m40.png)

This is actually a Base85 Encoding. Decoding it will give us this

![](/img/houseplantctf2020/m41.png)

"Jade" is a bot on the Discord Server of Houseplant CTF. DMing the Bot with the given string "rice\_tea\_cat\_panda" will give us the flag.

![](/img/houseplantctf2020/m42.png)**

Flag : rtcp{awaken\_winged\_sun\_dragon\_of\_ra}

**

OSINT
-----

The Drummer who Gave all his Daughters the Same Name
----------------------------------------------------

![](/img/houseplantctf2020/o1.png)

Solution:

Search Online for Anna Kournikova Virus and read about the virus analysis.

Value stored in the first registry key created by the virus Anna Kournikova is " Worm made with Vbswg 1.50b"

![](/img/houseplantctf2020/o10.png)**

Flag : Worm made with Vbswg 1.50b

**

What a Sight to See!
--------------------

![](/img/houseplantctf2020/o2.png)

Solution:

\[Google Search Operator\] site: Limit results to those from a specific website.

**

Flag : site:

**

Groovin and Cubin
-----------------

![](/img/houseplantctf2020/o3.png)

Solution:

Download "vibin.zip" and unzip it. You will get an image "vibin.jpg"

Nothing hidden in image, So we try "exiftool" to see it's metadata.

![](/img/houseplantctf2020/o30.png)

Search for "Groobi Doobie Shoobie Corp" online and we get a [twitter](https://twitter.com/GShoobie) account for @GShoobie

![](/img/houseplantctf2020/o31.png)

Go down and check the first tweet and you will see this.

![](/img/houseplantctf2020/o32.png)

So we head to [Instagram](https://www.instagram.com/groovyshoobie/) for @groovyshoobie

![](/img/houseplantctf2020/o33.png)**

Flag : rtcp{eXiF\_c0Mm3nT5\_4r3nT\_n3cEss4rY}

**
