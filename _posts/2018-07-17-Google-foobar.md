---
layout: post
title: Google Foobar
---

Recently, when my friend was briwsing on the internet and searching for some JavaScript related questions he was posted with a link to the foobar challenge by google. This link acts as a recruiting tool for google. This Google [foobar](https://foobar.withgoogle.com/){:target="_blank"} site allows access to questions only for people with a invite. The link may turn up when using [google.com](https://www.google.com/){:target="_blank"} (may be if you were searching something interesting according to google) or it can be accessed via an invite from a friend(if he/she reaches a certain level in the challenge). In this blog post I will write about the challenge, the problems that were posed for me in challenge and my approach.  
  
The foobar challenge consisted of 5 levels. Upon completion of a set number of challenges in each level, the user would advance to the next level. The first round consists of a single question(48 hours/question), followed by 2 in the second round(72 hours/question), 3 in the third(96 hours/question), 2 in the fourth(15 days/question) and 1 in the fifth(24 days/question).  
  
*NOTE*: The code in this entire blog post is written in python 2.7 as google foobar does not allow for 3.5 yet.  

#### Round 1  
  
**Re-ID**  
```python
"""
Re-ID
=====

There's some unrest in the minion ranks: minions with ID numbers like "1", "42", and other "good" numbers have been lording it over the poor minions who are stuck with more boring IDs. To quell the unrest, Commander Lambda has tasked you with reassigning everyone new, random IDs based on her Completely Foolproof Scheme. 

She's concatenated the prime numbers in a single long string: "2357111317192329...". Now every minion must draw a number from a hat. That number is the starting index in that string of primes, and the minion's new ID number will be the next five digits in the string. So if a minion draws "3", their ID number will be "71113". 

Help the Commander assign these IDs by writing a function answer(n) which takes in the starting index n of Lambda's string of all primes, and returns the next five digits in the string. Commander Lambda has a lot of minions, so the value of n will always be between 0 and 10000.

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

"""
```  
  
**APPROACH**  
This problem is pretty straight forward. I used a straght forward approach of forming the string of primes until the length required was met. The code to the problem in python below.  
  
```python
def isPrime(n):
    if n == 2:
        return True
    if n % 2 == 0:
        return False
    x = 3
    while x * x <= n:
        if n %x == 0 :
            return False
        x += 2
    return True

def answer(n):
    ret_str = "2"
    no = 3
    index = 1
    dig = 1
    den = 10
    while index <= n + 4:
        if isPrime(no):
            index += dig
            ret_str += str(no)
        no += 2
        if int(no / den) != 0:
            den *= 10
            dig += 1
    return ret_str[n:n+5]
```
  





#### Round 2  
  
**Lovely Lucky LAMBs**  
```python
"""
Lovely Lucky LAMBs
==================

Being a henchman isn't all drudgery. Occasionally, when Commander Lambda is feeling generous, she'll hand out Lucky LAMBs (Lambda's All-purpose Money Bucks). Henchmen can use Lucky LAMBs to buy things like a second pair of socks, a pillow for their bunks, or even a third daily meal!

However, actually passing out LAMBs isn't easy. Each henchman squad has a strict seniority ranking which must be respected - or else the henchmen will revolt and you'll all get demoted back to minions again! 

There are 4 key rules which you must follow in order to avoid a revolt:
    1. The most junior henchman (with the least seniority) gets exactly 1 LAMB.  (There will always be at least 1 henchman on a team.)
    2. A henchman will revolt if the person who ranks immediately above them gets more than double the number of LAMBs they do.
    3. A henchman will revolt if the amount of LAMBs given to their next two subordinates combined is more than the number of LAMBs they get.  (Note that the two most junior henchmen won't have two subordinates, so this rule doesn't apply to them.  The 2nd most junior henchman would require at least as many LAMBs as the most junior henchman.)
    4. You can always find more henchmen to pay - the Commander has plenty of employees.  If there are enough LAMBs left over such that another henchman could be added as the most senior while obeying the other rules, you must always add and pay that henchman.

Note that you may not be able to hand out all the LAMBs. A single LAMB cannot be subdivided. That is, all henchmen must get a positive integer number of LAMBs.

Write a function called answer(total_lambs), where total_lambs is the integer number of LAMBs in the handout you are trying to divide. It should return an integer which represents the difference between the minimum and maximum number of henchmen who can share the LAMBs (that is, being as generous as possible to those you pay and as stingy as possible, respectively) while still obeying all of the above rules to avoid a revolt.  For instance, if you had 10 LAMBs and were as generous as possible, you could only pay 3 henchmen (1, 2, and 4 LAMBs, in order of ascending seniority), whereas if you were as stingy as possible, you could pay 4 henchmen (1, 1, 2, and 3 LAMBs). Therefore, answer(10) should return 4-3 = 1.

To keep things interesting, Commander Lambda varies the sizes of the Lucky LAMB payouts. You can expect total_lambs to always be a positive integer less than 1 billion (10 ^ 9).

Test cases
==========

Inputs:
    (int) total_lambs = 10
Output:
    (int) 1

Inputs:
    (int) total_lambs = 143
Output:
    (int) 3

"""
```  
  
**APPROACH**  
  
The question is a bit tricky to understand at first. The question is asking a difference between number of Fibonacci numbers's sum <= *total_lambs* and number of powers of 2's sum <= *total_lambs* (with a catch in the rule number 4). Once you get hold of the question, the approach is very straight forward  
  
* Get the number of Fibonacci numbers that fit in *total_lambs*
* Get the total number of power's of 2 that fits in *total_lambs*
* Return the difference
  
The code in python language is as below.

```python
def answer(total_lambs):
    start = 1
    next_count = 1
    total = 0
    count_generous = 0
    while total + next_count <= total_lambs:
        total += start
        count_generous += 1
        start *= 2
        next_count = int(start/2) + int(start/4)
    fib1 = 1
    fib2 = 1
    total = 0
    count_stingy = 0
    while total + fib1 <= total_lambs:
        total += fib1
        fib1, fib2 = fib2, fib1 + fib2
        count_stingy += 1
    return  count_stingy - count_generous
```  
  
Also, this solution is still not optimized. A further optimization can be done for the Fibonacci series by using the property $$S_n=F_{n+2}−1$$. Finding the nth Fibonacci number can be done in $$O(log(n))$$ time.  
  
  
  


**Please Pass the Coded Messages**  
```python
"""
You need to pass a message to the bunny prisoners, but to avoid detection, the code you agreed to use is... obscure, to say the least. The bunnies are given food on standard-issue prison plates that are stamped with the numbers 0-9 for easier sorting, and you need to combine sets of plates to create the numbers in the code. The signal that a number is part of the code is that it is divisible by 3. You can do smaller numbers like 15 and 45 easily, but bigger numbers like 144 and 414 are a little trickier. Write a program to help yourself quickly create large numbers for use in the code, given a limited number of plates to work with.

You have L, a list containing some digits (0 to 9). Write a function answer(L) which finds the largest number that can be made from some or all of these digits and is divisible by 3. If it is not possible to make such a number, return 0 as the answer. L will contain anywhere from 1 to 9 digits.  The same digit may appear multiple times in the list, but each element in the list may only be used once.

Test cases
==========

Inputs:
    (int list) l = [3, 1, 4, 1]
Output:
    (int) 4311

Inputs:
    (int list) l = [3, 1, 4, 1, 5, 9]
Output:
    (int) 94311
"""
```  
  
Luckily, the question for this problem is straight forward. The intuition behind the solution is that we should as many numbers in the solution as possible. The more the digits the better it is. Also, the numbers should be sorted in descending order. To get to the core of the solution we need to understand the property for divisibility by 3. A number is divisibly by 3 if sum of the digits of the number is divisible by 3. Hence, if we mod the digits by 3, it would fall into 3 categories, namely 0, 1 and 2. All the numbers with a reminder of 0 are themselves divisible by 3 and hence, can be directly used in the answer. As per the reminders of 1 and 2, we can either choose a number that has a reminder as 1 and choose another number that has a reminder as 2(rule 1) and add these to the answer list, or we can choose 3 numbers that have a reminder of 1(rule 2) or 3 numbers that have a reminder of 2(rule 3) and add these to the answer list. We need to choose from the 3 options such that the total number of digits is maximized, Also, while choosing numbers for the 1 and 2 lists if we choose the largest numbers from the list we would be making sure that the resulting number is maximum.  
  
Let us take an example, the array \[3, 1, 4, 1, 5, 9\] would be split apart into 3 groups \[3, 9\] with reminder 0, \[1, 4, 1\] with a reminder of 1 and \[5\] with reminder of 2. We can add all the numbers from the group of 0 to the result list. We are left with 2 groups, [1, 4, 1] with reminder 1 and \[5\] with reminder 2 and we can either add \[4\] (largest element) from group 1 and \[5\] largest element from group 2 or we can add \[1, 4, 1\] (largest 3 elements) from group 1. In this case we can see that adding \[4, 5\] to the result list adds 2 elements while adding \[1, 4, 1\] adds 3 elements to the result list. Hence, we would add \[1, 4, 1\] to the result list and then sort the list in descending order. In general if we had x and y elements in the lists with reminder 1 and 2, than we try to see if x == y in which case we can add all the elements. If not we can see if the count of the remaining elements(assuming we applied rule 1 until we ran out of either 1s or 2s, the remaining elements of this operation) is divisble by 3, if it is than we add all the elements to the list. If not then we check the reminder of the remaining elements, if it is 2 than we can optimize this by forming one less pair during the application of rule 1. Ex, if we have 1, 1, 4, 4 from the reminder 1 list and 2, 5 from reminder 2 list, if we paired the two 4s with 5 and 2 then we would be wasting the two 1s. Insted we can form 1 less pair, by only adding one 4 and one 5 to the result list and than later adding 1, 1, 4 to the result list.  
  
The code for the aboe logic in python is as below.  
```python
def calc_counts(c1, c2):
    if c2 == 0:
        return [3*int(c1/3), 0]
    diff = c1 - c2
    extra = diff % 3
    if extra == 2:
        return [c1, c2-1]
    elif extra == 1:
        return [c1 - 1, c2]
    else:
        return [c1, c2]

def form_array(h, count):
    c1, c2 = count
    ret = h[0][:]
    if c1 == 0 and c2 == 0:
        return ret
    if c1 != 0:
        a1 = h[1][:]
        a1.sort(reverse=True)
        ret.extend(a1[:c1])
    if c2 != 0:
        a2 = h[2][:]
        a2.sort(reverse=True)
        ret.extend(a2[:c2])
    return ret

def answer(l):
    h = {0: [], 1:[], 2: []}
    for i in l:
        h[i%3].append(i)
    count_1 = len(h[1])
    count_2 = len(h[2])
    arr = []
    if count_1 == count_2:
        # all elements
        arr = l
    elif count_1 > count_2:
        count_1, count_2 = calc_counts(count_1, count_2)
        arr = form_array(h, [count_1, count_2])
    else:
        count_2, count_1 = calc_counts(count_2, count_1)
        arr = form_array(h, [count_1, count_2])
    arr.sort(reverse=True)
    ret = ''.join(list(map(str, arr)))
    if len(ret) == 0:
        return 0
    return int(ret)
```