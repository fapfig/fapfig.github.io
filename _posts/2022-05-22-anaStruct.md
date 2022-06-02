---
layout: post
title: Solving 2D Frames and Trusses using Python
categories: [Engineering, Python]
---

In this post, I will show you how to analyse 2D frames and Trusses using the python library anaStruct.

[anaStruct](https://github.com/ritchie46/anaStruct) is a python library for the analysis of 2D Frames and trusses. For more information please visit the [anaStruct’s documentation](https://anastruct.readthedocs.io/en/latest/).

Before you run the examples below you need to install the library. For this, type in the terminal or in your Jupyter notebook the following::

`pip install anastruct`

Then, you can import the necessary libraries.

```python
import math
import numpy as np
import matplotlib.pyplot as plt
from anastruct.fem.system import SystemElements
```

## Standerd Elements

Standard elements have bending and axial stiffness and therefore will implement shear force, bending moment, axial force, extension, and deflection.

### Example 1

```python
ss = SystemElements()

# Add beams to the system.
ss.add_element(location=[[0, 0], [3, 4]])
ss.add_element(location=[[3, 4], [8, 4]])

# Add supports.
ss.add_support_hinged(node_id=1)
ss.add_support_fixed(node_id=3)

# Add loads.
ss.q_load(element_id=2, q=-10)

# Solve
ss.solve()

# Get visual results.
ss.show_structure()
ss.show_reaction_force()
ss.show_axial_force()
ss.show_shear_force()
ss.show_bending_moment()
ss.show_displacement()
```

![png](\assets\2022-05-22-anaStruct\output_4_0.png)

![png](\assets\2022-05-22-anaStruct\output_4_1.png)

![png](\assets\2022-05-22-anaStruct\output_4_2.png)

![png](\assets\2022-05-22-anaStruct\output_4_3.png)

![png](\assets\2022-05-22-anaStruct\output_4_4.png)

![png](\assets\2022-05-22-anaStruct\output_4_5.png)

```python
ss = SystemElements(EA=15000, EI=5000)

# Add beams to the system.
ss.add_element(location=[0, 5])
ss.add_element(location=[[0, 5], [5, 5]])
ss.add_element(location=[[5, 5], [5, 0]])

# Add a fixed support at node 1.
ss.add_support_fixed(node_id=1)

# Add a rotational spring support at node 4.
ss.add_support_spring(node_id=4, translation=3, k=4000)

# Add loads.
ss.point_load(Fx=30, node_id=2)
ss.q_load(q=-10, element_id=2)

# Solve
ss.solve()

# Get visual results.
ss.show_structure()
ss.show_reaction_force()
ss.show_axial_force()
ss.show_shear_force()
ss.show_bending_moment()
ss.show_displacement()
```

![png](\assets\2022-05-22-anaStruct\output_5_0.png)

![png](\assets\2022-05-22-anaStruct\output_5_1.png)

![png](\assets\2022-05-22-anaStruct\output_5_2.png)

![png](\assets\2022-05-22-anaStruct\output_5_3.png)

![png](\assets\2022-05-22-anaStruct\output_5_4.png)

![png](\assets\2022-05-22-anaStruct\output_5_5.png)

## Truss Elements

Truss elements don’t have bending stiffness and will therefore not implement shear force, bending moment and deflection. It does model axial force and extension.

### Example 1

```python
ss = SystemElements(EA=5000)
ss.add_truss_element(location=[[0, 0], [0, 5]])
ss.add_truss_element(location=[[0, 5], [5, 5]])
ss.add_truss_element(location=[[5, 5], [5, 0]])
ss.add_truss_element(location=[[0, 0], [5, 5]], EA=5000 * math.sqrt(2))

ss.add_support_hinged(node_id=1)
ss.add_support_hinged(node_id=4)

ss.point_load(Fx=10, node_id=2)

ss.show_structure()

ss.solve()

ss.show_reaction_force()
ss.show_axial_force()
ss.show_displacement(factor=10)
```

![png](\assets\2022-05-22-anaStruct\output_8_0.png)

![png](\assets\2022-05-22-anaStruct\output_8_1.png)

![png](\assets\2022-05-22-anaStruct\output_8_2.png)

![png](\assets\2022-05-22-anaStruct\output_8_3.png)

### Example 2

```python
ss = SystemElements()
element_type = 'truss'

# create triangles
x = np.arange(1, 10) * np.pi
y = np.cos(x)
y -= y.min()
ss.add_element_grid(x, y, element_type=element_type)

# add top girder
ss.add_element_grid(x[1:-1][::2], np.ones(x.shape) * y.max(), element_type=element_type)

# add bottom girder
ss.add_element_grid(x[::2], np.ones(x.shape) * y.min(), element_type=element_type)

# supports
ss.add_support_hinged(1)
ss.add_support_roll(-1, 2)

# loads
ss.point_load(node_id=np.arange(2, 9, 2), Fy=-100)

ss.solve()
ss.show_structure()

ss.show_reaction_force()
ss.show_axial_force()
ss.show_displacement(factor=1)
```

![png](\assets\2022-05-22-anaStruct\output_10_0.png)

![png](\assets\2022-05-22-anaStruct\output_10_1.png)

![png](\assets\2022-05-22-anaStruct\output_10_2.png)

![png](\assets\2022-05-22-anaStruct\output_10_3.png)
