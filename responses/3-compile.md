Once we have decided on the specifics of our model, we need to do two processes: Compile the model and fit the data to the model. 

We can compile the model like so:

`model.compile(optimizer='sgd', loss='sparse_categorical_crossentropy', metrics=['accuracy'])`
    
Here we're just feeding three parameters to `model.compile`. We pick an optimizer, which determines how the model is updated as it gains information, a loss function, which measures how accurate the model is as it trains, and metrics, which specifies which information it provides  so we can analyze the model.

The optimizer we're using is the Stochastic Gradient Descent (SGD) optimization algorithm, but there are others available. For our loss we're using sparse_categorical_crossentropy. If our values were one-hot encoded, we would want to use "categorial_crossentropy" instead.
              
Then we have the model fit our training data:

`model.fit(train_data, train_labels, epochs=400)`

The three parameters `model.fit` needs are our training data, our training labels, and the number of epochs. One epoch is when the model has iterated over every sample once. Essentially the number of epochs is equal to the number of times we want to cycle through the data. We'll start with just 1 epoch, and then show that increasing the epoch improves the results.

**True or False**: We fit our model using *test_data* and *test_labels*.