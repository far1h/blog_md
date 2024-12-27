---
title: Natural Language Processing Notes
---
# Final Exam

## FCNN

> each node in is connected to each node in the other layer

> can result in overfitting

> assumes independency
### 3 Components
- Input
- Hidden Layers
- Output
## Time Series Model

> assume a given input will affect the layer after the input and also is affected by the node beforehand

### Examples
- LSTM (Long Short Term Memory)
	- base and bidirectional

> problem is that it connects to nodes directly before and directly after making it hard to understand semantics of pronouns

> there are techniques to mitigate this but can be complex with more calculations (propagation) and errors (refer pronouns to the subject closer to the pronoun rather than the actual reference)
## Attention Model

> keep information of the weights so that they can be carried into the target model or target path

> uses a stacking method for weights

## Transformer

> encoder (source) decoder (target) model
> where we encode the cumulative weights and convert into target words

> stacking encoders and decoders

> goal of encoder is to generate attention layer
> goal of decoder is masking and generating attention layer

> masking is try to hide each word within the sentence to genertae a prediction 

> generating attention layer means to carry information as a supplement to the next decoder layer
### Encoder Applications

> BERT: encoder fit to classification model

### Decoder Applications

> GPT: generate text

![[Pasted image 20241227101853.png]]

![[Pasted image 20241227101901.png]]