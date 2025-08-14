## Main Concept
The **chain rule** is a rule in calculus for finding the derivative of a function that is made up of other functions, for example:

$$
{y}=f(g(x))
$$
In this case, `x` goes into function `g`, and then the result of that function `g` goes into the function `f`.

## The chain rule
The chain rule says:

$$
\frac{dy}{dx} = \frac{dy}{dg} \cdot \frac{dg}{dx}
$$
which means that to find the total rate of change, multiply the rates of change along the path. In simpler words:
$\frac{dy}{dx}$ - describes the change of `y` in respect to `x`, and this change occurs within 2 consequent functions `g` and `f`. The rate of change within the function `g` is calculated by $\frac{dy}{dg}$, in other words - how much did the `y` changed in respect to the `g` change. And, since we know, that the input to the function `g` is some output value of `f(x)`, then the change of `g` output can be calculated as $\frac{dg}{dx}$. 
In other words, we kind of unwrapping the total change in respect to all other changes which contributed to it. 

## Simple math example 
Let $g(x)=x^2$, $f(u)=3u$, and $y=f(g(x))$

### Step 1 - Separate functions:
$$
u = g(x) = x^2
$$
$$
y = f(u) = 3u
$$

### Step 2 - Differentiate $f(u) = 3u$
We treat `u` as the variable. 
Definition of derivative:
$$
\frac{dy}{du}=\lim_{\Delta u \to 0} \frac{f(u + \Delta u) - f(u)}{\Delta u} 
$$
Plug `f(u)` = `3u` in:
$$
\frac{dy}{du}=\lim_{\Delta u \to 0} \frac{3(u+\Delta u) - 3u}{\Delta u} = \lim_{\Delta u \to 0} \frac{3u+3 \Delta u - 3u}{\Delta u} = \lim_{\Delta u \to 0} \frac{3 \Delta u}{\Delta u} = 3
$$

### Step 3 - Differentiate $g(x)=x^2$
Here `x` is also a variable
Lets plug $g(x)=x^2$ into the derivative definition:
$$
\frac{du}{dx} = \lim_{\Delta x \to 0} \frac{(x + \Delta x)^2 - x^2}{\Delta x} = \lim_{\Delta x \to 0} \frac{x^2 + 2x \Delta x + (\Delta x)^2 - x^2}{\Delta x}
$$
$$
= \lim_{\Delta x \to 0} \frac{2x \Delta x + (\Delta x)^2}{\Delta x} = \lim_{\Delta x \to 0}(2x + \Delta x)
$$

And since $\Delta x \to 0$, we get:
$$
\frac{du}{dx} = \lim_{\Delta x \to 0}(2x + 0) = 2x
$$
So, the slope of $x^2$ at any `x` is `2x`.

### Step 4 - Apply Chain Rule
$$
\frac{dy}{dx} = \frac{dy}{du} \cdot \frac{du}{dx} = 3 \cdot 2x = 6x
$$

If $y=3(x^2)$ directly into the derivative definition we would get the same result $6x$.
