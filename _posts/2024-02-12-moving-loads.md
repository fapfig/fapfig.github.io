---
layout: post
title: Beam Subjected to Moving Concentrated Loads
categories: [Engineering, Structures, Bridges]
author: Fabio P. Figueiredo
---

We know that the absolute maximum moment, for the beam shown in Figure 1, will occur under one of the concentrated loads. However, its location along the beam must be known to determine the specific load under which it will occur. In this post, we will determine the location analytically.

[![section](\assets\2024-02-12-moving-loads\beam.svg)](\assets\2024-02-12-moving-loads\beam.svg){:.glightbox}
_Figure 1. Simply supported beam subjected to three moving concentrated loads._

Firstly, we need to calculate the reaction at the support A. For this, take the moment at A:

$$
\sum_{}^{}M_{A} = 0
\\
R_{B} \cdot L = P_R \cdot \left(  \frac{L}{2} -  \left( x' - x\right) \right)
\\
R_{B}  =\frac{ P_R}{L} \cdot \left(  \frac{L}{2} -  \left( x' - x\right) \right) \tag{1}
$$

Thus, the bending moment under $M_3$ is:

$$
M_3 = R_{B} \cdot \left( \frac{L}{2}-x \right)
\\
M_3 = \frac{ P_R}{L} \cdot \left(  \frac{L}{2} -  \left( x' - x\right) \right) \cdot \left( \frac{L}{2}-x \right)
\\
M_3 = \frac{ P_R}{L} \cdot \left(  \frac{L^2}{4} -\frac{L}{2}x' + \frac{L}{2}x  -\frac{L}{2}x + x'x - xx  \right)
\\
M_3 = P_R \cdot \left(  \frac{L}{4} -\frac{x'}{2} + \cancel{\frac{x}{2}}  -\cancel{\frac{x}{2}} + \frac{x'x}{L} - \frac{x^2}{L}  \right)
\\
M_3 = P_R \cdot \left(  \frac{L}{4} -\frac{x'}{2} + \frac{x'x}{L} - \frac{x^2}{L}  \right)  \tag{2}
$$

The distance $x$ for which $M_3$ is maximum can be determined by differentiating Eq, (2):

$$
\frac{d M_3 }{dx} = 0
\\
P_R \cdot \left(  \frac{L}{4} -\frac{x'}{2} + \frac{x'x}{L} - \frac{x^2}{L}  \right)
\\
P_R \cdot \left( \frac{x'}{L} - \frac{2x}{L}  \right) = 0
\\
\left( \frac{x'}{L} - \frac{2x}{L}  \right) = 0
\\
\frac{x'}{\cancel{L}} = \frac{2x}{\cancel{L}}
$$

Therefore:

$$
\boxed{x = \frac{x'}{2}} \tag{3}
$$

Eq. (3) concludes that the absolute maximum moment in a simply supported beam occurs under one of the concentrated loads when the load under which the moment occurs and the resultant of the system of loads are equidistant from the center of the beam.
