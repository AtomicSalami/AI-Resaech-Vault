## Transformer model architecture
![[Pasted image 20250809095947.png]]

## History of Transformer
Before transformers [Recurrent Neural Networks (RNN)](obsidian://open?vault=ZorDann&file=remote%2F01-Study%2F03-AI-ML%20Related%2FRNN.md) were used for various tasks. However, RNNs had several problems, here are just a few of them:
* Slow computation for long sequences 
	* Since every token was fed into the RNN sequentially, for `n` number of tokens, the RNN should go through `n` number of for loops.
* [Vanishing or exploding gradients](obsidian://open?vault=ZorDann&file=remote%2F01-Study%2F03-AI-ML%20Related%2FUnstable%20Gradient%20Problem.md) problem