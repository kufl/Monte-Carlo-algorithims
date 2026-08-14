# Direct Sampling: Children on the Beach.

Imagine a bunch of children playing a game on the Monte Carlo beach, throwing pebbles into a square with a circle enclosed. 

Now, picture a unit circle with r = 1; the randomness of the pebbles hitting either shape allows for the estimation of pi.
The **idea** is to randomly sample points in a square that bounds a circle and count how many fall inside the quarter circle, where the ratio of $\frac{n_\text{hits}}{n_\text{trials}} = \frac{A_\text{circle}}{A_\text{square}} = \frac{\pi}{4}$ can be used to estimate pi.

```math
\text{Unit circle: } r = 1
```
```math
A_\text{circle} = \pi (1)^2 = \pi 
```
```math
A_\text{square} = (1 \times 2)^2 = 4
```
```math
\text{Hence, } \pi \approx 4 \frac{n_\text{hits}}{n_\text{trials}}
```

Using Python scripts, we can simulate the direct sampling Monte Carlo method without observing the game on Monte Carlo Beach.
