---
layout: post
title: Numerical Accuracy
---

```Matlab
function [ b ] = mapToBucket1( Min, Max, num, x )
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
