torch.nn module - building blocks for neural networks
- torch.nn: pytorch's module specifically designed for building neural networks. it provides:
    - layers: pre-defined building blocks like linear(fully connected) layers, convolutional layers, recurrent layers, etc.
    - activation functions: non-linear functions applied after layers to introduce compelxity and allow the network to learn non-linear patterns.
    - loss functions: measure how far the model's output is from the tru target.
    - containers: ways to group layers, like nn.Sequential.

defining a model as a class
- in pytorch, you typically define your neural network model as a python class that inherits from torch.nn.Module.

key methods to implement:
- __init__(self) constructor:
    - this is where you define and initialize all the layers your network will use.
    - you msut call super().__init__() as the first line.
    - layers are typically assigned as attributes of the class
- forward(self, x)
    - this method defines the forward pass of the network: how input data x flows through the layers you defined in __init__ to product an ouput.
    - you call the layers sequentially, often applying activation functions in between.

- nn.Linear Layer
    - a fully connected layer, also known as a dense layer.
    - it applies a linear transformation to the incoming data: y=xA^T+b, where x is the input, A is the weight matrix, and b is the bias vector.
    - parameters: 
        - in_features: the number of input features
        - out_features: the number of output features
        - pytorch automatically initializes the weights and biases for you

imagine a very simplified AI task for assessment:

Task: Predict if a student's short answer (represented by some numerical features, NOT raw text for this simple model) is "Correct" (1) or "Incorrect" (0).

Hypothetical Input Features: Imagine we've already processed the student's answer and a model answer into a fixed number of numerical features. For example:

Feature 1: Keyword match score (0.0 to 1.0)
Feature 2: Answer length (normalized)
Feature 3: Sentiment score of the answer
... and so on. Let's say we have 10 such features.


Output: A single value (logit) that can be passed through a sigmoid function to get a probability of being "Correct".

mini project
- continue using the same venv where you installed pytorch
- create a python script
- run the script
- observe the output