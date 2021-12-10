# SkimLit

The purpose of this notebook is to build an NLP model to make reading medical abstracts easier.

The paper we're replicating (the source of the dataset we'll be using) is avaiable is: [PubMed 200k RCT: a Dataset for Sequenctial Sentence Classification in Medical Abstracts](https://arxiv.org/abs/1710.06071)

And reading through the paper above, we see that the model architecture that they use to achieve their best results is available here [Neural networks for joint sentence classification in medical paper abstracts.](https://arxiv.org/pdf/1612.05251.pdf)

This notebook was inspired by [Daniel Bourke's version](https://github.com/mrdbourke/tensorflow-deep-learning/blob/main/09_SkimLit_nlp_milestone_project_2.ipynb)

The model will divide an abstract into the following five categories
* METHODS
* RESULTS
* CONCLUSIONS
* BACKGROUND
* OBJECTIVE

<a href="https://github.com/SeanMiranda/SkimLit">
  <img src="img/skmit overview.png" alt="Logo">
</a>


## Building a tribrid embedding model

We use the below architecture taken from the paper [Neural Networks for Joint Sentence Classification in Medical Paper Abstracts](https://arxiv.org/pdf/1612.05251.pdf)

<p align="center">
<a href="https://github.com/SeanMiranda/SkimLit">
  <img src="img/model architecture.PNG" alt="Logo">
</a>
 </p>


1. Create a token-level model (tokenizes sentences and passes it through a universal sentence encoder)
2. Create a character-level model (tokenizes characters and passes it through an embedding layer and bidirectional LSTM)
3. Create a "line_number" model (takes in one-hot-encoded "line_number" tensor and passes it through a non-linear layer)
4. Create a "total_lines" model (takes in one-hot-encoded "total_lines" tensor and passes it through a non-linear layer)
5. Combine (using layers.Concatenate) the outputs of 1 and 2 into a token-character-hybrid embedding and pass it series of output to Figure 1 and section 4.2 of [Neural Networks for Joint Sentence Classification in Medical Paper Abstracts](https://arxiv.org/pdf/1612.05251.pdf)
6. Combine (using `layers.Concatenate`) the outputs of 3, 4 and 5 into a token-character-positional tribrid embedding
7. Create an output layer to accept the tribrid embedding and output predicted label probabilities
8. Combine the inputs of 1, 2, 3, 4 and outputs of 7 into a `tf.keras.Model`


## Acknowledgements
* [TFHub Universal Sentence Encoder](https://tfhub.dev/google/universal-sentence-encoder/4)
* [PubMed 200k RCT: a Dataset for Sequential Sentence Classification in Medical Abstracts](https://arxiv.org/abs/1710.06071)
* [Neural Networks for Joint Sentence Classification in Medical Paper Abstracts](https://arxiv.org/pdf/1612.05251.pdf)
* [Daniel Bourke's version](https://github.com/mrdbourke/tensorflow-deep-learning/blob/main/09_SkimLit_nlp_milestone_project_2.ipynb)
