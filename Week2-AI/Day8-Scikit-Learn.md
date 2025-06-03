scikit-learn is an open source machine learning library for python

it features various classification, regression, clustering, dimentionality reduction, model selection, and preprocessing algorithms.

core concepts:
1. estimators - core objects in scikit-laern. any object that can learn from data is an estimation. it has a fit(x, y) method for training and often a predict(x) method for making predictions

2. features (x) - the input variables or attributes used for training and prediction. typically a 2D array-like structure where rows are samples and columns are features.

3. target (y) - the output variable you are trying to predict. typically a 1D array-like structure.

4. transformers - estimators that can transform input data. they have a fit(X, y) method to learn parameters and a transform(X) method to apply the transformation. 

common ML task - classification

classification - a supervised learning task where the goal is to predict a categorical class label.
- example:
    1. is this email spam or not spam? (binary classification)
    2. what is the species of this iris flower? (multi-class classification)

basic text feature extraction (CountVectorizer)
- machine learning models work with numbers, not raw text. we need to convert text data into a numerical format. this process is called feature extraction or vectorization.

- CountVectorizer:
    - a simple way to convert a collection of text documents to a matrix of token counts
    - it builds a vocabulary of all words seen in the training text and then counts how many times each word appears in each document
    - the result is often a sparse matrix (many zeros) because most documents only contain a small subset of overall vocabulary
    - example: 
        - document 1: "the cat sat"
        - document 2: "the dog sat"
        - vocabulary: {"the","cat","sat","dog"}
        - vector for doc 1: [1, 1, 1, 0] (1 "the", 1 "cat", 1 "sat", 0 "dog")
        - vector for doc 2: [1, 0, 1, 1] (1 "the", 0 "cat", 1 "sat", 1 "dog")

training a simple classifier
common and relatively simple classifier like:
1. LogisticRegression: despite it's name, it's a linear model for classification.
2. MultinomialNB (Naive Bayes): often works well for text classification tasks, especially with CountVectorizer. It's based on Bayes' theorem with a "naive" assumption of feature independence.

mini-project
1. setup your python environment for ML locally
2. open your terminal
3. create a dedicated directory for this ML script
4. create a python environment
5. install necessary libraries
6. create your data set (CSV file)
7. create your python training script
8. run the script 