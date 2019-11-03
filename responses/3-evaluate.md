*That's right!* We need to train 🏋️ our data before we test 🧪 it.

Now that the model is trained to our training data, we can test it against our training data:

```
loss_value, accuracy_value = model.evaluate(test_data, test_labels)
print(f'Our test accuracy was {accuracy_value})'
>>> Our test accuracy was 0.980132
```

`model.evaluate` will evaluate how strong our model is with the test data, and report that in the form of loss value and accuracy value (since we specified `accuracy` in our `selected_metrics` variable when we compiled the model). We'll just focus on our accuracy for now. With an accuracy of ~98%, it's not perfect, but it's very accurate.
 
We can also use our model to predict specific Pokémon, or at least have it tell us which status the Pokémon is most likely to have, with `model.predict`. All it needs to predict a Pokémon is the data for that Pokémon itself. We're providing that by selecting a certain `index` of `test_data`:

```
def predictor(test_data, test_labels, index):
    prediction = model.predict(test_data)
    if np.argmax(prediction[index]) == test_labels[index]:
        print(f'This was correctly predicted to be a \"{test_labels[index]}\"!')
    else:
        print(f'This was incorrectly predicted to be a \"{np.argmax(prediction[index])}\". It was actually a \"{test_labels[index]}\".')
        return(prediction)
```

Let's look at one of the more well-known legendary Pokémon: Mewtwo. He's number 150 in the list of Pokémon, so we'll look at index 149:

```
predictor(test_data, test_labels, 149)
>>> This was correctly predicted to be a "1"!
```

Nice! It accurately predicted Mewtwo was a legendary Pokémon.

*Close this issue when you have a predict function that is working* 