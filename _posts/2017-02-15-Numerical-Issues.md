---
layout: post
title: Numerical Issues
---

Numerical issues that go undetected lead to unexpected issues. This is one of those tales of a bug that was lurking in the code and went undetected for long.

I was tryin to fit a histogram to a set of data points. The bins of the [histogram](https://en.wikipedia.org/wiki/Histogram) were defined as below.

S - Smallest  
L - Largest  
$$
G = \frac{L-S}{N-3}
$$

* Bin 0, covering interval (-infinity, S-G/2).
* Bin 1, covering interval [S-G/2, S+G/2).
* Bin 2, covering interval [S+G/2, S+G+G/2).
* Bin 3, covering interval [S+G+G/2, S+2G+G/2).
...
* Bin N-2, covering interval [S+(N-4)G+G/2, S+(N-3)G+G/2). This interval is the same as [L-G/2, L+G/2).
* Bin N-1, covering interval [S+(N-3)G+G/2, +infinity). This interval is the same as [L+G/2, +infinity).

``` matlab
function [ b ] = mapToBucket( Min, Max, num, x )
    G = max(( Max - Min ) / (num-3), 0.0001);
    if( x < Min - (G/2) )
    	b = 1;
    % elseif( x >= Max + (G/2))
    % The above expression does not work when Max = Min in which case the
    % last bucket would be 0.0001 added from first bucket end point onwards
    elseif( x >= Min + G*(num-3) + (G/2))
    	b = num;
    else
    	b = 2 + floor(( x - Min + (G/2)) / G);
    end
end
```

``` matlab
function [ b ] = mapToBucket( Min, Max, num, x )
    G = max(( Max - Min ) / (num-3), 0.0001);
    if( x < Min - (G/2) )
    	b = 1;
    elseif( x >= Min + G*(num-3) + (G/2))
    	b = num;
    else
        values = repmat( Min + G/2, 1, num - 2) + (0:G:(num-3)*G);
        newmat = (2:num-1) .* (x < values);
        b = min(newmat(newmat ~= 0));
    end
end
```

