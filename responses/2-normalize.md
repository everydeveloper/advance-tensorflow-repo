Now that we have our labels extracted from the data, let's normalize the data so everything is on the same scale:

```
def data_normalizer(train_data, test_data):
    train_data = preprocessing.MinMaxScaler().fit_transform(train_data)
    test_data = preprocessing.MinMaxScaler().fit_transform(test_data)
    return(train_data, test_data)

train_data, test_data = data_normalizer(train_data, test_data)
```
Now we can get to the machine learning! Let's create the model using Keras. Keras is an API for Tensorflow. We have a few options for doing this, but we'll keep it simple for now. A model is built upon layers. We'll add two fully connected neural layers.

The number associated with the layer is the number of neurons in it. The first layer we'll use is a 'ReLU' (Rectified Linear Unit)' activation function. Since this is also the first layer, we need to specify `input_size`, which is the shape of an entry in our dataset.

After that, we'll finish with a softmax layer. Softmax is a type of logistic regression done for situations with multiple cases, like our 2 possible groups: 'Legendary' and 'Not Legendary'. With this we delineate the possible identities of the Pokémon into 2 probability groups corresponding to the possible labels:

```
length = train_data.shape[1]

model = keras.Sequential()
model.add(keras.layers.Dense(500, activation='relu', input_shape=[length,]))
model.add(keras.layers.Dense(2, activation='softmax'))
```

**True or False**: *We normalize data so that everything is on the same scale.*