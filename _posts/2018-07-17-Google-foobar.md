---
layout: post
title: Google Foobar
---

Recently, when my friend was briwsing on the internet and searching for some JavaScript related questions he was posted with a link to the foobar challenge by google. This link acts as a recruiting tool for google. This Google [foobar](https://foobar.withgoogle.com/){:target="_blank"} site allows access to questions only for people with a invite. The link may turn up when using [google.com](https://www.google.com/){:target="_blank"} (may be if you were searching something interesting according to google) or it can be accessed via an invite from a friend(if he/she reaches a certain level in the challenge). In this blog post I will write about the challenge, the problems that were posed for me in challenge and my approach.  
  
The foobar challenge consisted of 5 levels. Upon completion of a set number of challenges in each level, the user would advance to the next level. The first round consists of a single question(48 hours/question), followed by 2 in the second round(72 hours/question), 3 in the third(96 hours/question), 2 in the fourth(15 days/question) and 1 in the fifth(24 days/question).  
  
*NOTE*: The code in this entire blog post is written in python 2.7 as google foobar does not allow for 3.5 yet.  

#### Round 1  
<br/>
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
<br/>
**APPROACH**  
<br/>
This problem is pretty straight forward. I used a straght forward approach of forming the string of primes until the length required was met. The code to the problem in python below.  
<br/>
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
  <br/>
  <br/>
  <br/>
  <br/>
  <br/>

#### Round 2  
  
**Lovely Lucky LAMBs**  
<br/>
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
<br/>
**APPROACH**  
<br/>
The question is a bit tricky to understand at first. The question is asking a difference between number of Fibonacci numbers's sum <= *total_lambs* and number of powers of 2's sum <= *total_lambs* (with a catch in the rule number 4). Once you get hold of the question, the approach is very straight forward  
  
* Get the number of Fibonacci numbers that fit in *total_lambs*
* Get the total number of power's of 2 that fits in *total_lambs*
* Return the difference  
<br/><br/>
The code in python language is as below.  
<br/>
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
<br/>
Also, this solution is still not optimized. A further optimization can be done for the Fibonacci series by using the property $$S_n=F_{n+2}−1$$. Finding the nth Fibonacci number can be done in $$O(log(n))$$ time.  
  <br/>
  <br/>
  <br/>
  <br/>
  <br/>

**Please Pass the Coded Messages**  
<br/>
```python
"""
Please Pass the Coded Messages
==============================

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
<br/>
**APPROACH**
<br/>
Luckily, the question for this problem is straight forward. The intuition behind the solution is that we should as many numbers in the solution as possible. The more the digits the larger it is. Also, the numbers should be sorted in descending order. To get to the core of the solution we need to understand the property for divisibility by 3. A number is divisibly by 3 if sum of the digits of the number is divisible by 3. Hence, if we modulo the digits by 3, it would fall into 3 categories, namely 0, 1 and 2. All the numbers with a reminder of 0 are themselves divisible by 3 and hence, can be directly used in the answer. As per the reminders of 1 and 2, we can either choose a number that has a reminder as 1 and choose another number that has a reminder as 2(rule 1) and add these to the answer list, or we can choose 3 numbers that have a reminder of 1(rule 2) or 3 numbers that have a reminder of 2(rule 3) and add these to the answer list. We need to choose from the 3 options such that the total number of digits is maximized, Also, while choosing numbers for the 1 and 2 lists if we choose the largest numbers from the list we would be making sure that the resulting number is maximum.  
<br/>
Let us take an example, the array \[3, 1, 4, 1, 5, 9\] would be split apart into 3 groups \[3, 9\] with reminder 0, \[1, 4, 1\] with a reminder of 1 and \[5\] with reminder of 2. We can add all the numbers from the group of 0 to the result list. We are left with 2 groups, \[1, 4, 1\] with reminder 1 and \[5\] with reminder 2 and we can either add \[4\] (largest element) from group 1 and \[5\] largest element from group 2 or we can add \[1, 4, 1\] (largest 3 elements) from group 1. In this case we can see that adding \[4, 5\] to the result list adds 2 elements while adding \[1, 4, 1\] adds 3 elements to the result list. Hence, we would add \[1, 4, 1\] to the result list and then sort the list in descending order. In general if we had x and y elements in the lists with reminder 1 and 2, than we try to see if x == y in which case we can add all the elements. If not we can see if the count of the remaining elements(assuming we applied rule 1 until we ran out of either 1s or 2s, the remaining elements of this operation) is divisble by 3, if it is than we add all the elements to the list. If not then we check the reminder of the remaining elements, if it is 2 than we can optimize this by forming one less pair during the application of rule 1 and if it is 1 than we would need to leave out one element from the remaining elements. Ex, if we have 1, 1, 4, 4 from the reminder 1 list and 2, 5 from reminder 2 list, if we paired the two 4s with 5 and 2 then we would be wasting the two 1s. Insted we can form 1 less pair, by only adding one 4 and one 5 to the result list and than later adding 1, 1, 4 to the result list.  
<br/>
The code for the aboe logic in python is as below. 
<br/> 
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
  <br/>
  <br/>
  <br/>
  <br/>
  <br/>

#### Round 3  
<br/>
**Queue To Do**  
<br/>
```python
"""
Queue To Do
===========

You're almost ready to make your move to destroy the LAMBCHOP doomsday device, but the security checkpoints that guard the underlying systems of the LAMBCHOP are going to be a problem. You were able to take one down without tripping any alarms, which is great! Except that as Commander Lambda's assistant, you've learned that the checkpoints are about to come under automated review, which means that your sabotage will be discovered and your cover blown - unless you can trick the automated review system.

To trick the system, you'll need to write a program to return the same security checksum that the guards would have after they would have checked all the workers through. Fortunately, Commander Lambda's desire for efficiency won't allow for hours-long lines, so the checkpoint guards have found ways to quicken the pass-through rate. Instead of checking each and every worker coming through, the guards instead go over everyone in line while noting their security IDs, then allow the line to fill back up. Once they've done that they go over the line again, this time leaving off the last worker. They continue doing this, leaving off one more worker from the line each time but recording the security IDs of those they do check, until they skip the entire line, at which point they XOR the IDs of all the workers they noted into a checksum and then take off for lunch. Fortunately, the workers' orderly nature causes them to always line up in numerical order without any gaps.

For example, if the first worker in line has ID 0 and the security checkpoint line holds three workers, the process would look like this:
0 1 2 /
3 4 / 5
6 / 7 8
where the guards' XOR (^) checksum is 0^1^2^3^4^6 == 2.

Likewise, if the first worker has ID 17 and the checkpoint holds four workers, the process would look like:
17 18 19 20 /
21 22 23 / 24
25 26 / 27 28
29 / 30 31 32
which produces the checksum 17^18^19^20^21^22^23^25^26^29 == 14.

All worker IDs (including the first worker) are between 0 and 2000000000 inclusive, and the checkpoint line will always be at least 1 worker long.

With this information, write a function answer(start, length) that will cover for the missing security checkpoint by outputting the same checksum the guards would normally submit before lunch. You have just enough time to find out the ID of the first worker to be checked (start) and the length of the line (length) before the automatic review occurs, so your program must generate the proper checksum with just those two values.

Test cases
==========

Inputs:
    (int) start = 0
    (int) length = 3
Output:
    (int) 2

Inputs:
    (int) start = 17
    (int) length = 4
Output:
    (int) 14

"""
```
<br/>
**APPROACH**
<br/>
This problem is a simple one. The XOR of the numbers from 1 to n numbers follows a fixed pattern. If n modulo 4 is 0 then the XOR from 1 to n is 0 then the answer is 0, if it is 1 then the answer 1, if it is 2 then it is n + 1 and if it is 3 then the answer is 0. Let us call the method to perform this as XOR. We can exploit this property and find the XORs at appropriate position in each row.  
<br/>
For ex,  
<br/>
17 18 19 20 /  
21 22 23 / 24  
25 26 / 27 28  
29 / 30 31 32  
<br/>
For row 1 we can calculate XOR(17-1) = XOR(16), and then perfrom xor operation with XOR(20). We can continue this process along each row and then combine the results by performing xor. The code for the approach above is below implemented in python language.  
<br/>
```python
def XOR(n):
    val = n % 4
    if val == 0:
        return n
    if val == 1:
        return 1
    if val == 2:
        return n + 1
    return 0

def answer(start, length):
    if length == 1:
        return start
    val = XOR(start + 2*(length-1))
    if start > 1:
        val = val ^ XOR(start - 1)
    for i in range(length-2):
        elems = length - 2 - i
        init = start + length*(2 + i) - 1
        val = val ^ XOR(init + elems) ^ XOR(init)
    return val
```  
  <br/>
  <br/>
  <br/>
  <br/>
  <br/>

**Bomb, Baby!**  
<br/>
```python
"""
Bomb, Baby!
===========

You're so close to destroying the LAMBCHOP doomsday device you can taste it! But in order to do so, you need to deploy special self-replicating bombs designed for you by the brightest scientists on Bunny Planet. There are two types: Mach bombs (M) and Facula bombs (F). The bombs, once released into the LAMBCHOP's inner workings, will automatically deploy to all the strategic points you've identified and destroy them at the same time. 

But there's a few catches. First, the bombs self-replicate via one of two distinct processes: 
Every Mach bomb retrieves a sync unit from a Facula bomb; for every Mach bomb, a Facula bomb is created;
Every Facula bomb spontaneously creates a Mach bomb.

For example, if you had 3 Mach bombs and 2 Facula bombs, they could either produce 3 Mach bombs and 5 Facula bombs, or 5 Mach bombs and 2 Facula bombs. The replication process can be changed each cycle. 

Second, you need to ensure that you have exactly the right number of Mach and Facula bombs to destroy the LAMBCHOP device. Too few, and the device might survive. Too many, and you might overload the mass capacitors and create a singularity at the heart of the space station - not good! 

And finally, you were only able to smuggle one of each type of bomb - one Mach, one Facula - aboard the ship when you arrived, so that's all you have to start with. (Thus it may be impossible to deploy the bombs to destroy the LAMBCHOP, but that's not going to stop you from trying!) 

You need to know how many replication cycles (generations) it will take to generate the correct amount of bombs to destroy the LAMBCHOP. Write a function answer(M, F) where M and F are the number of Mach and Facula bombs needed. Return the fewest number of generations (as a string) that need to pass before you'll have the exact number of bombs necessary to destroy the LAMBCHOP, or the string "impossible" if this can't be done! M and F will be string representations of positive integers no larger than 10^50. For example, if M = "2" and F = "1", one generation would need to pass, so the answer would be "1". However, if M = "2" and F = "4", it would not be possible.

Test cases
==========

Inputs:
    (string) M = "2"
    (string) F = "1"
Output:
    (string) "1"

Inputs:
    (string) M = "4"
    (string) F = "7"
Output:
    (string) "4"
"""
```  
<br/>
**APPROACH**  
<br/>
This problem upon initial inspection seems to belong to be a direct application of BFS. But then when I took a look at the constraints it seemed to be impossible to ever find a solution using the approach as M and F could be in the range of $$10^50$$.  
<br/>
The solution to this problem lies in the final state (M, F) instead of (1, 1) inital state. The simple intuition that if M is larger than F implies that F was added to M in the previous step helps in solving the problem. Also, note that doing simple subtraction would also not be feasible to compute, for ex. $$(M, F) = (10^50, 1)$$ would take a huge amount of time to compute. Hence, we can use a modulo operator and the total number of steps can be computed by /. That if we were asked (M ,F) as (11, 29) then we can use module operator to obtain (11, 29 % 11) = (11, 7) as the next stage with *int*(29/11) = 2 number of steps added to the result.  
<br/>
The code for this approach is coded as below.  
<br/>
```python
def answer(M, F):
    m, f = long(M), long(F)
    total = 0
    while not (m == 1 and f == 1):
        if f <= 0 or m <= 0:
            return "impossible"
        if f == 1:
            return str(total + m - 1)
        else:
            total += long(m/f)
            m, f = f, m % f
    return str(total)
```
  <br/>
  <br/>
  <br/>
  <br/>
  <br/>

**Doomsday Fuel**
<br/>
```python
"""
Doomsday Fuel
=============

Making fuel for the LAMBCHOP's reactor core is a tricky process because of the exotic matter involved. It starts as raw ore, then during processing, begins randomly changing between forms, eventually reaching a stable form. There may be multiple stable forms that a sample could ultimately reach, not all of which are useful as fuel. 

Commander Lambda has tasked you to help the scientists increase fuel creation efficiency by predicting the end state of a given ore sample. You have carefully studied the different structures that the ore can take and which transitions it undergoes. It appears that, while random, the probability of each structure transforming is fixed. That is, each time the ore is in 1 state, it has the same probabilities of entering the next state (which might be the same state).  You have recorded the observed transitions in a matrix. The others in the lab have hypothesized more exotic forms that the ore can become, but you haven't seen all of them.

Write a function answer(m) that takes an array of array of nonnegative ints representing how many times that state has gone to the next state and return an array of ints for each terminal state giving the exact probabilities of each terminal state, represented as the numerator for each state, then the denominator for all of them at the end and in simplest form. The matrix is at most 10 by 10. It is guaranteed that no matter which state the ore is in, there is a path from that state to a terminal state. That is, the processing will always eventually end in a stable state. The ore starts in state 0. The denominator will fit within a signed 32-bit integer during the calculation, as long as the fraction is simplified regularly. 

For example, consider the matrix m:
[
  [0,1,0,0,0,1],  # s0, the initial state, goes to s1 and s5 with equal probability
  [4,0,0,3,2,0],  # s1 can become s0, s3, or s4, but with different probabilities
  [0,0,0,0,0,0],  # s2 is terminal, and unreachable (never observed in practice)
  [0,0,0,0,0,0],  # s3 is terminal
  [0,0,0,0,0,0],  # s4 is terminal
  [0,0,0,0,0,0],  # s5 is terminal
]
So, we can consider different paths to terminal states, such as:
s0 -> s1 -> s3
s0 -> s1 -> s0 -> s1 -> s0 -> s1 -> s4
s0 -> s1 -> s0 -> s5
Tracing the probabilities of each, we find that
s2 has probability 0
s3 has probability 3/14
s4 has probability 1/7
s5 has probability 9/14
So, putting that together, and making a common denominator, gives an answer in the form of
[s2.numerator, s3.numerator, s4.numerator, s5.numerator, denominator] which is
[0, 3, 2, 9, 14].

Test cases
==========

Inputs:
    (int) m = [[0, 2, 1, 0, 0], [0, 0, 0, 3, 4], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0]]
Output:
    (int list) [7, 6, 8, 21]

Inputs:
    (int) m = [[0, 1, 0, 0, 0, 1], [4, 0, 0, 3, 2, 0], [0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0]]
Output:
    (int list) [0, 3, 2, 9, 14]
"""
```  
<br/>
**APPROACH**  
<br/>
The problem described is a [Absorbing MArkov Chain](https://en.wikipedia.org/wiki/Absorbing_Markov_chain){:target="_blank"}. The main challenge involved in this is the [Matrix Inverse using Gaussian elimination](https://en.wikipedia.org/wiki/Invertible_matrix#Gaussian_elimination){:target="_blank"}. It is a straight forward implementation once the theory behind it is understood.  
<br/>
The code for the above problem in python is as below.  
<br/>
```python
from fractions import Fraction

def gcd(x, y):
    def gcd1(x, y):
        if y == 0:
            return x
        return gcd1(y, x%y)
    return gcd1(abs(x), abs(y))

def simplify(x, y):
    g = gcd(x, y)
    return Fraction(long(x/g), long(y/g))

def lcm(x, y):
    return long(x*y/gcd(x,y))

def transform(mat):
    sum_list = list(map(sum, mat))
    bool_indices = list(map(lambda x: x == 0, sum_list))
    indices = set([i for i, x in enumerate(bool_indices) if x])
    new_mat = []
    for i in range(len(mat)):
        new_mat.append(list(map(lambda x: Fraction(0, 1) if(sum_list[i] == 0) else simplify(x, sum_list[i]), mat[i])))
    transform_mat = []
    zeros_mat = []
    for i in range(len(new_mat)):
        if i not in indices:
            transform_mat.append(new_mat[i])
        else:
            zeros_mat.append(new_mat[i])
    transform_mat.extend(zeros_mat)
    tmat = []
    for i in range(len(transform_mat)):
        tmat.append([])
        extend_mat = []
        for j in range(len(transform_mat)):
            if j not in indices:
                tmat[i].append(transform_mat[i][j])
            else:
                extend_mat.append(transform_mat[i][j])
        tmat[i].extend(extend_mat)
    return [tmat, len(zeros_mat)]

def copy_mat(mat):
    cmat = []
    for i in range(len(mat)):
        cmat.append([])
        for j in range(len(mat[i])):
            cmat[i].append(Fraction(mat[i][j].numerator, mat[i][j].denominator))
    return cmat

def gauss_elmination(m, values):
    mat = copy_mat(m)
    for i in range(len(mat)):
        index = -1
        for j in range(i, len(mat)):
            if mat[j][i].numerator != 0:
                index = j
                break
        if index == -1:
            raise ValueError('Gauss elimination failed!')
        mat[i], mat[index] = mat[index], mat[j]
        values[i], values[index] = values[index], values[i]
        for j in range(i+1, len(mat)):
            if mat[j][i].numerator == 0:
                continue
            ratio = -mat[j][i]/mat[i][i]
            for k in range(i, len(mat)):
                mat[j][k] += ratio * mat[i][k]
            values[j] += ratio * values[i]
    res = [0 for i in range(len(mat))]
    for i in range(len(mat)):
        index = len(mat) -1 -i
        end = len(mat) - 1
        while end > index:
            values[index] -= mat[index][end] * res[end]
            end -= 1
        res[index] = values[index]/mat[index][index]
    return res

def transpose(mat):
    tmat = []
    for i in range(len(mat)):
        for j in range(len(mat)):
            if i == 0:
                tmat.append([])
            tmat[j].append(mat[i][j])
    return tmat

def inverse(mat):
    tmat = transpose(mat)
    mat_inv = []
    for i in range(len(tmat)):
        values = [Fraction(int(i==j), 1) for j in range(len(mat))]
        mat_inv.append(gauss_elmination(tmat, values))
    return mat_inv

def mat_mult(mat1, mat2):
    res = []
    for i in range(len(mat1)):
        res.append([])
        for j in range(len(mat2[0])):
            res[i].append(Fraction(0, 1))
            for k in range(len(mat1[0])):
                res[i][j] += mat1[i][k] * mat2[k][j]
    return res

def splitQR(mat, lengthR):
    lengthQ = len(mat) - lengthR
    Q = []
    R = []
    for i in range(lengthQ):
        Q.append([int(i==j)-mat[i][j] for j in range(lengthQ)])
        R.append(mat[i][lengthQ:])
    return [Q, R]

def answer(mat):
    res = transform(mat)
    if res[1] == len(mat):
        return [1, 1]
    Q, R = splitQR(*res)
    inv = inverse(Q)
    res = mat_mult(inv, R)
    row = res[0]
    l = 1
    for item in row:
        l = lcm(l, item.denominator)
    res = list(map(lambda x: long(x.numerator*l/x.denominator), row))
    res.append(l)
    return res
```  
<br/>
<br/>
<br/>
<br/>
<br/>

#### Round 4  

**Free the Bunny Prisoners**  
<br/> 
```python
"""
Free the Bunny Prisoners
========================

You need to free the bunny prisoners before Commander Lambda's space station explodes! Unfortunately, the commander was very careful with her highest-value prisoners - they're all held in separate, maximum-security cells. The cells are opened by putting keys into each console, then pressing the open button on each console simultaneously. When the open button is pressed, each key opens its corresponding lock on the cell. So, the union of the keys in all of the consoles must be all of the keys. The scheme may require multiple copies of one key given to different minions.

The consoles are far enough apart that a separate minion is needed for each one. Fortunately, you have already freed some bunnies to aid you - and even better, you were able to steal the keys while you were working as Commander Lambda's assistant. The problem is, you don't know which keys to use at which consoles. The consoles are programmed to know which keys each minion had, to prevent someone from just stealing all of the keys and using them blindly. There are signs by the consoles saying how many minions had some keys for the set of consoles. You suspect that Commander Lambda has a systematic way to decide which keys to give to each minion such that they could use the consoles.

You need to figure out the scheme that Commander Lambda used to distribute the keys. You know how many minions had keys, and how many consoles are by each cell.  You know that Command Lambda wouldn't issue more keys than necessary (beyond what the key distribution scheme requires), and that you need as many bunnies with keys as there are consoles to open the cell.

Given the number of bunnies available and the number of locks required to open a cell, write a function answer(num_buns, num_required) which returns a specification of how to distribute the keys such that any num_required bunnies can open the locks, but no group of (num_required - 1) bunnies can.

Each lock is numbered starting from 0. The keys are numbered the same as the lock they open (so for a duplicate key, the number will repeat, since it opens the same lock). For a given bunny, the keys they get is represented as a sorted list of the numbers for the keys. To cover all of the bunnies, the final answer is represented by a sorted list of each individual bunny's list of keys.  Find the lexicographically least such key distribution - that is, the first bunny should have keys sequentially starting from 0.

num_buns will always be between 1 and 9, and num_required will always be between 0 and 9 (both inclusive).  For example, if you had 3 bunnies and required only 1 of them to open the cell, you would give each bunny the same key such that any of the 3 of them would be able to open it, like so:
[
  [0],
  [0],
  [0],
]
If you had 2 bunnies and required both of them to open the cell, they would receive different keys (otherwise they wouldn't both actually be required), and your answer would be as follows:
[
  [0],
  [1],
]
Finally, if you had 3 bunnies and required 2 of them to open the cell, then any 2 of the 3 bunnies should have all of the keys necessary to open the cell, but no single bunny would be able to do it.  Thus, the answer would be:
[
  [0, 1],
  [0, 2],
  [1, 2],
]

Test cases
==========

Inputs:
    (int) num_buns = 2
    (int) num_required = 1
Output:
    (int) [[0], [0]]

Inputs:
    (int) num_buns = 5
    (int) num_required = 3
Output:
    (int) [[0, 1, 2, 3, 4, 5], [0, 1, 2, 6, 7, 8], [0, 3, 4, 6, 7, 9], [1, 3, 5, 6, 8, 9], [2, 4, 5, 7, 8, 9]]

Inputs:
    (int) num_buns = 4
    (int) num_required = 4
Output:
    (int) [[0], [1], [2], [3]]
"""
```
<br/>
**APPROACH**  
<br/>
This problem is a based on combinatorics. To make to notation clear, let us consider that there are *b* bunnies and *r* are required. Let us now consider this simple situation, let us say we have chosen *r-1* bunnies at random, and we were to choose 1 more bunny to get the complete set of keys to open the prison door. We know that these *r-1* bunnies cannot open the door in itself and hence the remaining *b-r+1* bunnies must have a key that these *r-1* bunnies don't. We can exploit this fact to solve the problem. We need to generate all combinations of size *b-r+1* bunnies and add a unique key to each of these bunnies. The code for this in python is as below.  
<br/>
```python
from itertools import combinations

def answer(num_buns, num_required):
    buns = [[] for i in range(num_buns)]
    if num_required == 0:
        return buns
    start = 0
    for c in combinations(buns, num_buns - num_required + 1):
        for item in c:
            item.append(start)
        start += 1
    return buns
```  
  <br/>
  <br/>
  <br/>
  <br/>
  <br/>

**Escape Pods**
<br/>
```python
"""
Escape Pods
===========

You've blown up the LAMBCHOP doomsday device and broken the bunnies out of Lambda's prison - and now you need to escape from the space station as quickly and as orderly as possible! The bunnies have all gathered in various locations throughout the station, and need to make their way towards the seemingly endless amount of escape pods positioned in other parts of the station. You need to get the numerous bunnies through the various rooms to the escape pods. Unfortunately, the corridors between the rooms can only fit so many bunnies at a time. What's more, many of the corridors were resized to accommodate the LAMBCHOP, so they vary in how many bunnies can move through them at a time. 

Given the starting room numbers of the groups of bunnies, the room numbers of the escape pods, and how many bunnies can fit through at a time in each direction of every corridor in between, figure out how many bunnies can safely make it to the escape pods at a time at peak.

Write a function answer(entrances, exits, path) that takes an array of integers denoting where the groups of gathered bunnies are, an array of integers denoting where the escape pods are located, and an array of an array of integers of the corridors, returning the total number of bunnies that can get through at each time step as an int. The entrances and exits are disjoint and thus will never overlap. The path element path[A][B] = C describes that the corridor going from A to B can fit C bunnies at each time step.  There are at most 50 rooms connected by the corridors and at most 2000000 bunnies that will fit at a time.

For example, if you have:
entrances = [0, 1]
exits = [4, 5]
path = [
  [0, 0, 4, 6, 0, 0],  # Room 0: Bunnies
  [0, 0, 5, 2, 0, 0],  # Room 1: Bunnies
  [0, 0, 0, 0, 4, 4],  # Room 2: Intermediate room
  [0, 0, 0, 0, 6, 6],  # Room 3: Intermediate room
  [0, 0, 0, 0, 0, 0],  # Room 4: Escape pods
  [0, 0, 0, 0, 0, 0],  # Room 5: Escape pods
]

Then in each time step, the following might happen:
0 sends 4/4 bunnies to 2 and 6/6 bunnies to 3
1 sends 4/5 bunnies to 2 and 2/2 bunnies to 3
2 sends 4/4 bunnies to 4 and 4/4 bunnies to 5
3 sends 4/6 bunnies to 4 and 4/6 bunnies to 5

So, in total, 16 bunnies could make it to the escape pods at 4 and 5 at each time step.  (Note that in this example, room 3 could have sent any variation of 8 bunnies to 4 and 5, such as 2/6 and 6/6, but the final answer remains the same.)

Test cases
==========

Inputs:
    (int list) entrances = [0]
    (int list) exits = [3]
    (int) path = [[0, 7, 0, 0], [0, 0, 6, 0], [0, 0, 0, 8], [9, 0, 0, 0]]
Output:
    (int) 6

Inputs:
    (int list) entrances = [0, 1]
    (int list) exits = [4, 5]
    (int) path = [[0, 0, 4, 6, 0, 0], [0, 0, 5, 2, 0, 0], [0, 0, 0, 0, 4, 4], [0, 0, 0, 0, 6, 6], [0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0]]
Output:
    (int) 16
"""
```
<br/>
**APPROACH**  
<br/>
This problem states the [Network Flow](https://en.wikipedia.org/wiki/Flow_network){:target="_blank"} and [Dinic's algorithm](https://en.wikipedia.org/wiki/Dinic%27s_algorithm){:taget="_blank"} solves the problem. The python code that solves the problem is as below.  
<br/>
```python
def bfs(matrix, source, destination):
    visited = [-1 for i in range(len(matrix))]
    visited[source] = source
    queue = [source]
    while len(queue) > 0:
        top = queue.pop(0)
        for i in range(len(matrix)):
            if (matrix[top][i][1] - matrix[top][i][0]) != 0 and visited[i] == -1:
                if i == destination:
                    # Get route
                    visited[destination] = top
                    path = [destination]
                    temp = destination
                    while temp != source:
                        temp = visited[temp]
                        path.append(temp)
                    path.reverse()
                    # Get flow value and update augmented graph
                    temp = 1
                    total = float("inf")
                    cur = source
                    while temp != len(path):
                        entry = matrix[cur][path[temp]]
                        diff = abs(entry[1]) - entry[0]
                        total = min(total, diff)
                        cur = path[temp]
                        temp += 1
                    temp = 1
                    cur = source
                    while temp != len(path):
                        entry = matrix[cur][path[temp]]
                        if entry[1] < 0: # Already augmented need to flip
                            entry[1] += total
                        else:
                            entry[0] += total
                        entry = matrix[path[temp]][cur]
                        if entry[1] <= 0: # Already augmented need to flip
                            entry[1] -= total
                        else:
                            entry[0] += total
                        cur = path[temp]
                        temp += 1
                    return True
                else:
                    visited[i] = top
                    queue.append(i)
    return False

def answer(entrances, exits, path):
    max_val = sum(list(map(sum, path)))
    aug = []
    for i in range(len(path)):
        aug.append([])
        for j in range(len(path[i])):
            aug[i].append([0, path[i][j]])
        aug[i].append([0, 0])
        if i in exits:
            aug[i].append([0, max_val])
        else:
            aug[i].append([0, 0])
    aug.append([])
    aug.append([])
    for i in range(len(path[0]) + 2):
        if i in entrances:
            aug[-2].append([0, max_val])
        else:
            aug[-2].append([0, 0])
        aug[-1].append([0, 0])
    while bfs(aug, len(aug)-2, len(aug)-1):
        pass
    total = 0
    for i in range(len(aug)):
        total += aug[-2][i][0]
    return total
```
<br/>
<br/>
<br/>
<br/>
<br/>

#### Round 5   
<br/> 
**Dodge the Lasers!**  
<br/> 
```python
"""
Dodge the Lasers!
=================

Oh no! You've managed to escape Commander Lambdas collapsing space station in an escape pod with the rescued bunny prisoners - but Commander Lambda isnt about to let you get away that easily. She's sent her elite fighter pilot squadron after you - and they've opened fire!

Fortunately, you know something important about the ships trying to shoot you down. Back when you were still Commander Lambdas assistant, she asked you to help program the aiming mechanisms for the starfighters. They undergo rigorous testing procedures, but you were still able to slip in a subtle bug. The software works as a time step simulation: if it is tracking a target that is accelerating away at 45 degrees, the software will consider the targets acceleration to be equal to the square root of 2, adding the calculated result to the targets end velocity at each timestep. However, thanks to your bug, instead of storing the result with proper precision, it will be truncated to an integer before adding the new velocity to your current position.  This means that instead of having your correct position, the targeting software will erringly report your position as sum(i=1..n, floor(i*sqrt(2))) - not far enough off to fail Commander Lambdas testing, but enough that it might just save your life.

If you can quickly calculate the target of the starfighters' laser beams to know how far off they'll be, you can trick them into shooting an asteroid, releasing dust, and concealing the rest of your escape.  Write a function answer(str_n) which, given the string representation of an integer n, returns the sum of (floor(1*sqrt(2)) + floor(2*sqrt(2)) + ... + floor(n*sqrt(2))) as a string. That is, for every number i in the range 1 to n, it adds up all of the integer portions of i*sqrt(2).

For example, if str_n was "5", the answer would be calculated as
floor(1*sqrt(2)) +
floor(2*sqrt(2)) +
floor(3*sqrt(2)) +
floor(4*sqrt(2)) +
floor(5*sqrt(2))
= 1+2+4+5+7 = 19
so the function would return "19".

str_n will be a positive integer between 1 and 10^100, inclusive. Since n can be very large (up to 101 digits!), using just sqrt(2) and a loop won't work. Sometimes, it's easier to take a step back and concentrate not on what you have in front of you, but on what you don't.

Test cases
==========

Inputs:
    (string) str_n = "5"
Output:
    (string) "19"

Inputs:
    (string) str_n = "77"
Output:
    (string) "4208"
"""
```
<br/>
**APPROACH**
<br/>
Let us first take a look at the problem. Given x, find the sum below,
<br/>
$$\lfloor{\sqrt{2}}\rfloor + \lfloor{2\sqrt{2}}\rfloor + \lfloor{3\sqrt{2}}\rfloor + ... + \lfloor{x\sqrt{2}}\rfloor $$
<br/>
Firstly, as the question states $$10^{100}$$ is too large to compute by a iterative approach. We need to find some sort of equation for the sum in order to solve it.
<br/>
Let SUM denote the sum of the above series to x terms. Separating the fractional and non fractional parts and summing it up yields  <br/>
$$x*(x+1)/2 + \lfloor{\sqrt{2}-1}\rfloor + \lfloor{2(\sqrt{2}-1)}\rfloor + \lfloor{3(\sqrt{2}-1)}\rfloor + ... + \lfloor{x(\sqrt{2}-1)}\rfloor$$<br/><br/>
If we only look at the fractional series, it looks like  <br/>
$$\lfloor{\sqrt{2}-1}\rfloor + \lfloor{2(\sqrt{2}-1)}\rfloor + \lfloor{3(\sqrt{2}-1)}\rfloor + ... + \lfloor{x(\sqrt{2}-1)}\rfloor$$  
<br/>
<br/>
and terms of the series look like 0 + 0 + 1 + 1 + 2 + ... We can see that the terms of the series is monotonically increasing(always growing). The frequency with which the terms increase in this series is <br/><br/>
$$\frac{1}{\sqrt2-1}$$, which upon simplification leads to $$\sqrt2+1$$<br/><br/>
Each term of this series indicates the location at which the jump occurs,
<br/><br/>$$\lceil{\sqrt{2}+1}\rceil, \lceil{2(\sqrt{2}+1)}\rceil, \lceil{3(\sqrt{2}+1)}\rceil, ... , \lceil{\lfloor{x(\sqrt{2}-1)}\rfloor(\sqrt{2}+1)}\rceil$$<br/><br/>
i.e. index 3(jump from 0-> 1), 5(1->2), 8(2->3), etc.<br/>
Let us look at an example below for x = 5
<br/>
0 0 **1** 1 **2** 2 2 **3** <- Floor fractional parts  
1 2 **3** 4 **5** 6 7 **8** <- Indexes  
0 0 **1** 1 1 1 1 1 <- Contribution from index 3  
0 0 0 0 **1** 1 1 1 <- Contribution from index 5  
0 0 0 0 0 0 0 **1** <- Contribution from index 8  
<br/><br/>
From the above logic we can see that the sum of the fractional parts can be written as <br/>
$$x\lfloor{x(\sqrt{2}-1)}\rfloor - \lfloor{\sqrt{2}+1}\rfloor - \lfloor{2(\sqrt{2}+1)}\rfloor - \lfloor{3(\sqrt{2}+1)}\rfloor - ... - \lfloor{\lfloor{x(\sqrt{2}-1)}\rfloor(\sqrt{2}+1)}\rfloor$$, note that we use floor here instead of ceil as we need to include the 1 present at the index as well. We can further rewrite the above equation for SUM as below<br/><br/>
$$SUM(x) = x*(x+1)/2 + x\lfloor{x(\sqrt{2}-1)}\rfloor - \lfloor{\sqrt{2}+1}\rfloor - \lfloor{2(\sqrt{2}+1)}\rfloor - \lfloor{3(\sqrt{2}+1)}\rfloor - ... - \lfloor{\lfloor{x(\sqrt{2}-1)}\rfloor(\sqrt{2}+1)}\rfloor$$<br/>
<br/>
Rearranging each of the $$\sqrt(2)+1$$ terms by separating the 1 and $$\sqrt(2)$$ we get <br/><br/>
$$SUM(x) = x*(x+1)/2 + x\lfloor{x(\sqrt{2}-1)}\rfloor - (1 + 2 + 3 + ... + \lfloor{x(\sqrt{2}-1)}\rfloor) - (\lfloor{\sqrt{2}}\rfloor + \lfloor{2(\sqrt{2})}\rfloor + \lfloor{3(\sqrt{2})}\rfloor + ... + \lfloor{\lfloor{x(\sqrt{2}-1)}\rfloor(\sqrt{2})}\rfloor)$$<br/><br/>
This would look obvious upon further inspection that the term on the right hand side is $$SUM(\lfloor{x(\sqrt{2}-1)}\rfloor)$$<br/><br/>
$$SUM(x) = x*(x+1)/2 + x\lfloor{x(\sqrt{2}-1)}\rfloor - \frac{\lfloor{x(\sqrt{2}-1)}\rfloor(\lfloor{x(\sqrt{2}-1)}\rfloor + 1)}{2} - SUM(\lfloor{x(\sqrt{2}-1)}\rfloor)$$ <br/><br/>
The code for the above equation in python is as below.<br/>
```python
def floor_root_2(x):
    sqrt_2 = long("41421356237309504880168872420969807856967187537694807317667973799073247846210703885038753432764157273501384623091229702492483605585073721264412149709993583141322266592750559275579995050115278206")
    ten_power = long("100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000")
    ret = long((x*(x+1))/2)
    if x <= 10:
        for i in range(x):
            ret += long((sqrt_2*(i+1))/ten_power)
        return ret
    total = long((sqrt_2 * x) / ten_power)
    ret += (x * total ) - long((total * (total + 1))/2) - floor_root_2(total)
    return ret
    
def answer(str_n):
    return str(floor_root_2(long(str_n)))
```
<br/>