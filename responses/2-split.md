Now that we have our data in a useable form, we need to split it. We want to have a set of data that we'll use to train our model, and we'll use another set of data to test our model after we've trained it. In general, the data is randomly split with about 70% being used for training and 30% used for testing. For easier visualization, we'll be splitting the data by Pokémon generation. The first generation of Pokémon (from Pokémon Red, Blue, and Yellow) will be our testing data while the rest will be our training data:

```
def train_test_splitter(DataFrame, column):
    df_train = DataFrame.loc[df[column] != 1]
    df_test = DataFrame.loc[df[column] == 1]

    df_train = df_train.drop(column, axis=1)
    df_test = df_test.drop(column, axis=1)

    return(df_train, df_test)

df_train, df_test = train_test_splitter(df, 'Generation')
```

This function takes any Pokémon whose "Generation" label is equal to 1 and putting it into the test dataset, and putting everyone else in the training dataset. It then `drop`s the `Generation` category from the dataset. 

Now that we have our two sets of data, we'll need to separate the labels (the 'islegendary' category) from the rest of the data. Remember, this is the answer key to the test the algorithms are trying to solve, and it does no good to have them learn with the answer-key in (metaphorical) hand:

```
def label_delineator(df_train, df_test, label):
    
    train_data = df_train.drop(label, axis=1).values
    train_labels = df_train[label].values
    test_data = df_test.drop(label,axis=1).values
    test_labels = df_test[label].values
    return(train_data, train_labels, test_data, test_labels)
```

This function extracts the data from the DataFrame and puts it into arrays that TensorFlow can understand with`.values`. We then have the four groups of data:

```
train_data, train_labels, test_data, test_labels = label_delineator(df_train, df_test, 'isLegendary')
```

*Comment with the generation number we used in the test dataset.*