# Autoencoders

### What is an autoencoder?

An autoencoder is a type of neural network that attempts to learn an approximation of the input function in a lower-dimensional space -- usually called the **latent space**. 

![](../.gitbook/assets/image%20%2812%29.png)

Once the model is trained, it can be split up into the `encoder` and the `decoder` sections, which allow us to compress an input into a lower-dimensional latent space. 

They're extremely useful in being able to compress high-dimensional data into lower \(more fundamental\) dimensions, which is a notion that lends itself very nicely to image segmentation and data compression.

Intuitively, an autoencoder can act like an unsupervised version of [PCA \(principal component analysis\)](../engineering/principal-component-analysis.md).

### Denoising Autoencoder Example

Here is an example of the results from a denoising autoencoder, implemented [here](https://github.com/adham-elarabawy/playground/blob/master/machine-learning/autoencoder/autoencoder.py). 

![](../.gitbook/assets/image%20%283%29.png)





