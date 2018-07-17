---
layout: post
title: Google Foobar
---

Recently, when my friend was briwsing on the internet and searching for some JavaScript related questions he was posted with a link to the foobar challenge by google. This link acts as a recruiting tool for google. This Google [foobar](https://foobar.withgoogle.com/){:target="_blank"} site allows access to questions only for people with a invite. The link may turn up when using [google.com](https://www.google.com/){:target="_blank"} (may be if you were searching something interesting according to google) or it can be accessed via an invite from a friend(if he/she reaches a certain level in the challenge). In this blog post I will write about the challenge, the problems that were posed for me in challenge and my approach a dn solution.  
  
The foobar challenge consisted of 5 levels. Upon completion of a set number of challenges in each level, the user would advance to the next level. The first round consists of a single question(48 hours/question), followed by 2 in the second round(72 hours/question), 3 in the third(96 hours/question), 2 in the fourth(15 days/question) and 1 in the fifth(24 days/question).  

#### Round 1  
  
**Question**  
```
Re-ID
=====

There's some unrest in the minion ranks: minions with ID numbers like "1", "42", and other "good" numbers have been lording it over the poor minions who are stuck with more boring IDs. To quell the unrest, Commander Lambda has tasked you with reassigning everyone new, random IDs based on her Completely Foolproof Scheme. 

She's concatenated the prime numbers in a single long string: "2357111317192329...". Now every minion must draw a number from a hat. That number is the starting index in that string of primes, and the minion's new ID number will be the next five digits in the string. So if a minion draws "3", their ID number will be "71113". 

Help the Commander assign these IDs by writing a function answer(n) which takes in the starting index n of Lambda's string of all primes, and returns the next five digits in the string. Commander Lambda has a lot of minions, so the value of n will always be between 0 and 10000.

Languages
=========

To provide a Python solution, edit solution.py
To provide a Java solution, edit solution.java

Test cases
==========

Inputs:
    (int) n = 0
Output:
    (string) "23571"

Inputs:
    (int) n = 3
Output:
    (string) "71113"

Use verify [file] to test your solution and see how it does. When you are finished editing your code, use submit [file] to submit your answer. If your solution passes the test cases, it will be removed from your home folder.

```