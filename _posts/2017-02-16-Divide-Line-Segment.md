---
layout: post
title: Divide a Line Segment
---

This problem is from a competition where we were only allowed to use tools such as scale and compass and asked to divide a line segment into many parts. The number of parts the line ahs to be split into can be any number. In this blog post we would use 5 as the number of parts we divide a line segment into but the technique used in this blog can be applied to any number.  

Let us look at the theory behind how this technique works.

![Theory]({{site.baseurl}}/images/div_line_segment/div_line_seg_theory.png "Theory")  

The diagram above shows two line segments AB and CM, which are parallel to each other. Let us look at triangles NCG and NAO. The line segment NA cuts the parallel lines at C and A respectively. So the angle $$\widehat{NCG}$$ is equal to the angle $$\widehat{NAO}$$ ( take a look [here](https://en.wikipedia.org/wiki/Parallel_(geometry)) for more explanation). Similarly, looking at line NO we can conclude that $$\widehat{NGC}$$ is equal to $$\widehat{NOA}$$. $$\widehat{ANO}$$ and $$\widehat{CNG}$$ are the same angle and so are equal. This shows that the two triangles NCG and NAO are similar.  

Let us make use the rule of equality of ratio of sides in these two similar triangles,  
$$\frac{CG}{AO}$$ = $$\frac{NG}{NO}$$

The above logic of similar triangles also applies to triangles NGI and NOP. And we can use the rule of ratio of sides in these triangles too.  
$$\frac{GI}{OP}$$ = $$\frac{NG}{NO}$$

We know that $$\frac{NG}{NO}$$ is the same fraction in both these equations. Hence, we can conclude that $$\frac{GI}{OP}$$ is equal to $$\frac{CG}{AO}$$.  
The equation can be rewritten as  
$$\frac{GI}{CG}$$ =  $$\frac{OP}{AO}$$

We can conclude using the same logic that the below set of triangles are similar.

* NCG and NAO
* NGI and NOP
* NIL and NPQ
* NLM and NQB

And hence we can conclude from these similar triangles that this logic holds through out all these triangles.  
If we started off with equal line segements(CG = GI = IL = LM), then we would end up with equal line segments in the parallel line too i.e. we would end up with (AO = OP = PQ = QB).  

If we were to construct a parallel line to the given and then divide the parallel line into *n* number of line segments and then get the vertex of triangle common to all the triangles, then we can get the location of all the other *n-2* points on the given line. Let us see an illustration how this can be achieved.

## Tools required

* Scale
* Compass
* Pencil

## Steps

### Step 1 : Draw a parallel line
![Step 1a]({{site.baseurl}}/images/div_line_segment/div_line_seg_step_1a.png "Step 1a")  
To draw a parallel line to our given line(shown in picture above), we need to draw a perpendicular line from our given line. Let us first start with 2 equidistant points from point A.

We draw a circle from point A which cuts the line AB at 2 equidistant points(C and D) from point A. 
![Step 1b]({{site.baseurl}}/images/div_line_segment/div_line_seg_step_1b.png "Step 1b")  

From B and C let us now draw a perpendicular bisector that bisects the line BC at A, thus giving us a perpendicular to our line AB.
![Step 1c]({{site.baseurl}}/images/div_line_segment/div_line_seg_step_1c.png "Step 1c")  

Connect the two points and draw the line EF forming the perpendicular bisector.
![Step 1d]({{site.baseurl}}/images/div_line_segment/div_line_seg_step_1d.png "Step 1d")  

Now the idea is to draw a perpendicular to line EF at E. So, we perform the first 3 steps again to obtain a perpendicular bisector.
Draw a circle with center at E, thus obtaining points G and H.
![Step 1e]({{site.baseurl}}/images/div_line_segment/div_line_seg_step_1e.png "Step 1e")  

From G and H draw a perpendicular bisector.
![Step 1f]({{site.baseurl}}/images/div_line_segment/div_line_seg_step_1f.png "Step 1f")  

Connect the points of the perpendicular bisector I and J and extend the parallel line ahead.
![Step 1g]({{site.baseurl}}/images/div_line_segment/div_line_seg_step_1g.png "Step 1g")  

### Step 2: Divide the parallel line into *n* equal line segments

Dividing the parallel line to *n* equal segments of **any length** would be a key step in this process. We can choose any length to form the *n* equal line segements. For simplicity I decided to choose the length to be equal to EJ, as we already have a circle around E cutting the line at J. If you choose a different length, then you will need to draw a different circle around E which will cut the line EJ at the new point that we need for further constructions.
![Step 1g]({{site.baseurl}}/images/div_line_segment/div_line_seg_step_1g.png "Step 1g")  

From the new point that you just obtained, measure the length l and draw a circle to obtain another point on the line. Keep repeating this process till you obtain your *n* points. In the diagram below, we obtained the points K, L and M by drawing these circles.
![Step 2a]({{site.baseurl}}/images/div_line_segment/div_line_seg_step_2a.png "Step 2a")  

### Step 3: Form the triangle

We now obtain the apex(the vertex N in the theory example) of the triangle by using the points B and M. Connect the points B and M and extend these till it cuts the line AE.
![Step 3a]({{site.baseurl}}/images/div_line_segment/div_line_seg_step_3a.png "Step 3a")  

From the apex N draw lines through J, K and L to cut the line AB at O, P and Q.
![Step 3b]({{site.baseurl}}/images/div_line_segment/div_line_seg_step_3b.png "Step 3b")  
![Step 3c]({{site.baseurl}}/images/div_line_segment/div_line_seg_step_3c.png "Step 3c")  

A close up of the points A, O, P, Q and B is shown below.  
![Step 3d]({{site.baseurl}}/images/div_line_segment/div_line_seg_step_3d.png "Step 3d")  

To check if these points divide the line segment AB equally into 5 segments, we draw circles around O, P and Q with radius as their neighbouring points to verify that the lengths actually do match.
![Step 3e]({{site.baseurl}}/images/div_line_segment/div_line_seg_step_3e.png "Step 3e")  

The complete construction below  
![Final]({{site.baseurl}}/images/div_line_segment/div_line_seg_final.png "Final")  

*Note*: One corner case that has not neen mentioned here is that the lines AE and BM in step 3 may not intersect in one unique case. This happens when the length of line segment AB is equal to the length of the line segment EM. In this case, we can make use of the lenght of any of the line segments from the parallel line(EJ = JK = KL = LM) to divide the actual line into equal segments.

