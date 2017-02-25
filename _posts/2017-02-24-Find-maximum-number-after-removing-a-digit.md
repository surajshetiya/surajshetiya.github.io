---
layout: post
title: Finding the maximum number after removing a digit from it
---

This was one of the interview questions at Google back in 2016.

#### The problem statement

Given a number n which has atleast one occurence of a digit repeating itself adacently, find the maximum number that can be obtained by deleting ONE of these adjacent digits.


Let us a take an example to understand the question better. Let us say n is 12**33**2, note that 3 repeats adjacently and can be deleted while even though 2 repeats itself in the number it cannot be deleted because the two 2s are not adjacent. So, there is only one number in this case which is 1232 and that itself is the maximum. Let us consider another example, n = 1122, then there are two different numbers that can have one valid digit removed 122 and 112. And as we see that 122 > 112 the output should be 122.

#### Approach

Let us consider the case where the number has *r* repetitions, then we would have to compute r numbers and then find the maximum ?


What if the digit were x bits long and they had x/2 adjacent digit repititions ? Then we would have to compute x/2 numbers and then compute maximum. This is not optimal even though it solves the actual problem.


Let us try a different approach and see intuitively how it works. Let us consider the number 1122 for example. Let us take a look at the first combination, 1[1]22 = 122, where we delete 1. What if the actual number was 11022 and we decided to delete the same 1 - 1[1]022, then we would end up with 1022 while the maximum number possible would be 1102(obtained after deleting 2). What changed ?


In the first number 1[1]22, 1 < 2 and hence if I were to delete 1 the digit in the 1s place now would be a 2 and hence would definitely be a larger number(*when compared to the first \|n\|-1 digits of the actual number*). But in the second case 1[1]022, deleting 1 would replace 1 with 0 which would infact make the number smaller ?


Note that for the rest of the article when I say smaller or larger then I mean in comparision with the first \|n\|-1 digits of the actual number.




The first step in solving this question is identifying adjacent repetitions of digits which are followed by a larger number. And then what ? If we have multiple such numbers then which one should we delete ?


Let us take an example and find out. n = 113224, then the two numbers are 13224 and 11324, note that the first number is larger than the second and hence we know that deleting the first occurence is the correct choice. But why ? Intuitively speaking, as we have choice of digits that we can delete, we should choose the one which has highest significance. That is the first occurance. Is this all to the problem ?


We seem to have missed another case, what if we dont find an increasing sequence at all, for example n=110443762, then what should be correct answer ? We have already seen that deleting a digit that is followed by a smaller number makes the number smaller than the rest. But we know that all possible deletions that can happen would make the resulting number smaller. So which one to choose ? Intuitively, we should be deleting the one with the least significant bit i.e. last occurence. This follows the exact same logic to why the first number should be chosen when it is increasing instead of the rest.


Code for the same in matlab is as below.


```matlab
function [ op ] = max_delete_num(y)
    assert(all(y>='0') && all(y<='9'), 'Numbers should be between 0 and 9');

    % Find out the locations of the repetition.
    repeats = [y,'a']==['a',y];

    assert(any(repeats), 'Should have atleast 1 repeating number');

    % Get the index of the location where it is increasing.
    index = arrayfun(@(x) x*(y(x)<y(x+1)), find(repeats(1:end-2)));

    % If there any such locations then form new number and return it.
    if(any(index))
        i = find(index);
        op = [y(1:index(i(1))-1), y(index(i(1))+1:end)];
    else
        % Find indexes of the repeats.
        repeat = find(repeats);
        last_repeat = repeat(end);

        % Delete the last occurence from the number.
        op = [y(1:last_repeat-1), y(last_repeat+1:end)];
    end
end
```
