---
layout: post
title: Divide a Line Segment
---

This problem is from a competition where we were only allowed to use tools such as scale and compass and asked to divide a line segment into many parts. The number of parts the line ahs to be split into can be any number. In this blog post we would use 5 as the number of parts we divide a line segment into but the technique used in this blog can be applied to any number.  

Let us look at the theory behind how this technique works.

![Theory]({{site.baseurl}}/images/div_line_seg_theory.png "Theory")  

The diagram above shows two line segments AB and CM, which are parallel to each other. Let us look at triangles NCG and NAO. The line segment NA cuts the parallel lines at C and A respectively. So the angle $$\widehat{NCG}$$ is equal to the angle $$\widehat{NAO}$$ ( take a look [here](https://en.wikipedia.org/wiki/Parallel_(geometry) for more explanationa). Similarly, looking at line NO we can conclude that $$\widehat{NGC}$$ is equal to $$widehat{NOA}$$. $$\widehat{ANO}$$ and $$\widehat{CNG}$$ are the same angle and so are equal. This shows that the two triangles NCG and NAO are similar.  

Let us make use the rule of equality of ratio of sides in these two similar triangles,  
$$\frac{CG}{AO}$$ = $$\frac{NG}{NO}$$

The above logic of similar traingles also applies to triangles NGI and NOP. And we can use the rule of ratio of sides in these triangles too.  
$$\frac{GI}{OP}$$ = $$\frac{NG}{NO}$$

We know that $$\frac{NG}{NO}$$ is the same fraction in both these equations. Hence, we can conclude that $$\frac{GI}{OP}$$ is equal to $$\frac{CG}{AO}$$.  
The equation can be rewritten as  
$$\frac{GI}{CG}$$ =  $$\frac{OP}{AO}$$

We can conclude using the same logic that the below set of triangles are similar.

* NCG and NAO
* NGI and NOP
* NIL and NPQ
* NLM and NQB

And hence we can conclude from these similar triangles that this logic holds through out all these traiangles.  
If we started off with equal line segements(CG = GI = IL = LM), then we would end up with equal line segments in the parallel line too i.e. we would end up with (AO = OP = PQ = QB).


