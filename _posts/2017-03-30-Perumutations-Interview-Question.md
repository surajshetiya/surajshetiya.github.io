---
layout: post
title: Permutation Google Interview Question
---

This question was asked in a google interview. I was not in the interview though, my friend asked me this question from [career cup](https://www.careercup.com/question?id=5761279915458560).  
  
## Question  
In school a student gets rewarded if he has an attendance record without being absent for more than once or being late for 3 times continuously.

Given a student's attendance record represented by a string with 3 possible characters 'L'(Late), 'A'(Absent), 'O' (On time), check whether the student qualifies for the reward.

For ex,  
@INPUT (String) "OLLOAOLLO"  
@RETURN (Boolean) True  
  
@INPUT (String) "OLLAOOOLLO"
@RETURN (Boolean) False
The student does not qualify for reward because "LLA" means he was late for 3 times in a row.

Follow up question, if known the length of the attendance string is n, how many possible ways there is to attend school and make sure you get the reward.  
  
This post would be a easy read if you can read this wikipedia [link](https://en.wikipedia.org/wiki/Inclusion%E2%80%93exclusion_principle) about Principle of inclusion and exclusion.
  
## Answer  
The first part of the question is straight forward and can be done in any programming language. The follow up questions seems to be interesting and is a combinatorics question.  
  
Let us first analyse the corner cases. If the student is absent twice or more times, then he would not qualify. And hence, we can have only either one or 0 Absents in the students attendence record.  
  
If the student has less than 2 absents then we can treat an absent as a late day(see test case 2 in the examples above). So, we now have two literals in the input string L - Late and O - On Time.  
  
  
Let us take the case where we have no As for simplicity for now and later try analysing for the case where there is a A. Let us first arrange these Ls and Os in a large string and then try removing the cases where there are 3 Ls in a row.  
  
Arrange l Ls and o Os in a string = $$\frac{(l+o)!}{l!o!}$$  
  
Let us now try to remove 3 Ls from it. The method to do it is to combine the 3Ls into one unit and apply the same permutations again. So, we now have $$o+l-3+1$$ units i.e. $$o+l-2$$ units. Using these mnay items we get, $$\frac{(o+l-2)!}{(l-3)!o!}$$.  
  
But by combining these into one unit and obtaining the number of Ls and Os in order we still have missed one case.  
...{LLL}L...  
...L{LLL}...  
  
The two above cases seem to generate the same case twice and we seem to have reduced the case where there are 4 Ls in a single stretch twice, while we should in fact have reduced once. In a similar manner, we seem to have reduced the pattern where there were 5 Ls in a single stretch 3 times.

 
...{LLL}LL...  
...L{LLL}L...  
...LL{LLL}...  

A similar, logic follows for other larger numbers as well i.e. removed list - 3 - once, 4 - twice, 5 - thrice, 6 - four times, ...  
  
We need to account for this extra removal and try adding these units back into the system. Let us first try adding 4 Ls in a row into the system by making 4 Ls in a single unit. By using similar formulae as above, we get $$\frac{(o+l-3)!}{(l-4)!o!}$$. Note that in this formula we account for 4 - once, 5 Ls twice, 6 Ls thrice,...  
  
By adding this to the original formula, we obtain 5 Ls removed thrice from the formula above while added twice in this formula which makes it removed once. In a similar manner 6 Ls removed 4 times by above formula while 6 Ls added 3 times by thisformula, thus removing it once.

And hence, the final formula is as below.
  
$$ \frac{(l+o)!}{l!o!} - \frac{(o+l-2)!}{(l-3)!o!} + $\frac{(o+l-3)!}{(l-4)!o!}$$  
  
Let us verify the above formula with a simple example.
Let us assume that the student came late to class 4 times and was on time once. 4 Ls and 1 P. The only case when this can be *true* is LLPLL.  
$$ \frac{5!}{4!1!} - \frac{3!}{1!1!} + \frac{2!}{0!1!}$$ = 5 - 6 + 2 = 1
  
Thus this formula works fine for the case where there is no A(bsent). But what if the student was indeed absent on one of the days.
