#  Batch Normalization – Practice

Batch normalization is most useful when building deep neural networks. To demonstrate this, we'll create a convolutional neural network with 20 convolutional layers, followed by a fully connected layer. We'll use it to classify handwritten digits in the MNIST dataset, which should be familiar to you by now.

This is **not** a good network for classfying MNIST digits. You could create a _much_ simpler network and get _better_ results. However, to give you hands-on experience with batch normalization, we had to make an example that was:
1. Complicated enough that training would benefit from batch normalization.
2. Simple enough that it would train quickly, since this is meant to be a short exercise just to give you some practice adding batch normalization.
3. Simple enough that the architecture would be easy to understand without additional resources.

## How to install

`git clone https://github.com/chjoo7/batch-norm.git`

This notebook includes two versions of the network that you can edit. The first uses higher level functions from the `tf.layers` package. The second is the same network, but uses only lower level functions in the `tf.nn` package.

1. [Batch Normalization with `tf.layers.batch_normalization`](#example_1)
2. [Batch Normalization with `tf.nn.batch_normalization`](#example_2)

# Batch Normalization using `tf.layers.batch_normalization`<a id="example_1"></a>

This version of the network uses `tf.layers` for almost everything, and expects you to implement batch normalization using [`tf.layers.batch_normalization`](https://www.tensorflow.org/api_docs/python/tf/layers/batch_normalization) 

With this many layers, it's going to take a lot of iterations for this network to learn. By the time you're done training these 800 batches, your final test and validation accuracies probably won't be much better than 10%. (It will be different each time, but will most likely be less than 15%.)

Using batch normalization, you'll be able to train this same network to over 90% in that same number of batches.


# Add batch normalization

We've copied the previous three cells to get you started. **Edit these cells** to add batch normalization to the network. For this exercise, you should use [`tf.layers.batch_normalization`](https://www.tensorflow.org/api_docs/python/tf/layers/batch_normalization) to handle most of the math, but you'll need to make a few other changes to your network to integrate batch normalization. You may want to refer back to the lesson notebook to remind yourself of important things, like how your graph operations need to know whether or not you are performing training or inference. 

If you get stuck, you can check out the `Batch_Normalization_Solutions` notebook to see how we did things.

With batch normalization, you should now get an accuracy over 90%. Notice also the last line of the output: `Accuracy on 100 samples`. If this value is low while everything else looks good, that means you did not implement batch normalization correctly. Specifically, it means you either did not calculate the population mean and variance while training, or you are not using those values during inference.

# Batch Normalization using `tf.nn.batch_normalization`<a id="example_2"></a>

Most of the time you will be able to use higher level functions exclusively, but sometimes you may want to work at a lower level. For example, if you ever want to implement a new feature – something new enough that TensorFlow does not already include a high-level implementation of it, like batch normalization in an LSTM – then you may need to know these sorts of things.

This version of the network uses `tf.nn` for almost everything, and expects you to implement batch normalization using [`tf.nn.batch_normalization`](https://www.tensorflow.org/api_docs/python/tf/nn/batch_normalization).

**Optional TODO:** You can run the next three cells before you edit them just to see how the network performs without batch normalization. However, the results should be pretty much the same as you saw with the previous example before you added batch normalization. 

**TODO:** Modify `fully_connected` to add batch normalization to the fully connected layers it creates. Feel free to change the function's parameters if it helps.

**Note:** For convenience, we continue to use `tf.layers.dense` for the `fully_connected` layer. By this point in the class, you should have no problem replacing that with matrix operations between the `prev_layer` and explicit weights and biases variables.

Once again, the model with batch normalization should reach an accuracy over 90%. There are plenty of details that can go wrong when implementing at this low level, so if you got it working - great job! If not, do not worry, just look at the Batch_Normalization_Solutions notebook to see what went wrong.

