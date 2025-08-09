## Vanishing/Exploding gradients problems 
In ML, the **vanishing/exploding** (further unstable) **gradient problem** is the problem of greatly diverging gradient magnitudes between earlier and later layers encountered when training NN with [backpropagation](obsidian://open?vault=ZorDann&file=remote%2F01-Study%2F03-AI-ML%20Related%2FBackpropagation.md). 
In such methods, NN weights are updated proportional to their [partial derivative](obsidian://open?vault=ZorDann&file=remote%2F01-Study%2F00-Math%2FDerivatives.md) of the [loss function](obsidian://open?vault=ZorDann&file=remote%2F01-Study%2F00-Math%2FLoss%20Function.md). As the number of forward propagation steps in a NN increases (for example due to greater NN depth) gradients of earlier weights are calculated with increasingly many multiplications. These multiplications shrink (or significantly increase) the gradient magnitude. 

## Example
### Simple NN structure example

![[Excalidraw/Drawing 2025-08-09 10.28.11.excalidraw]]

As said before, to update the weights and biases of the NN we would calculate the derivative of loss function. It is calculated as follows: 

$$ 
\frac{dy}{dx} = \frac{dy}{df} \cdot \frac{df}{dx}
$$
In this example, the chain is only consists of 2 elements, `dx` and `dy`. Lets imagine, that we have many hundreds of these elements in our chain. Then, when we multiply numbers smaller then 1, it would result in an increasingly small number, and if the number is greater then 1, then it might lead to the increasingly high number. This is what this problem is about. 
Just to make sure you understand, lets a calculation example: 

$$
\frac{dy}{dx}=\frac{dy}{df} \cdot \frac{df}{dy} = 0.5 \cdot 0.4 = 0.2
$$
Now, lets increase the number of elements in the chain:
$$
\frac{dy}{dx}=\frac{dy}{du} \cdot \frac{du}{dv} \cdot \frac{dv}{dw} \cdot \frac{dw}{dx}= 0.5 \cdot 0.4 \cdot 0.7 \cdot 0.2= 0.028
$$

### Gradient effect on NN
The gradient is the **signal that tells each weight how to change** to make the loss smaller.

In weight update form:

$$ {w1} = {w0} - {η} \cdot \frac{dL}{dw} $$

- $\frac{dL}{dw}$​ (**gradient**) → direction & magnitude of change
- ${η}$ (**learning rate**) → scales the step size
- **Result** → new weight values

So:

- **Large gradient** → bigger weight updates
- **Small gradient** → tiny weight updates
- **Zero gradient** → no learning