Now that we can see all of our data, we'll need to format it to be read by the model. First, we need to make sure all the data is numerical. A lot of our data already is, such as stats like 'HP' and 'Attack'. Great!

A few of the categories aren't numerical however. One example is the category that we'll be training our model to detect: the "isLegendary" column of data. These are the labels that we will eventually separate from the rest of the data and use as an answer key for the model's training. We'll convert this column from boolean "False" and "True" statements to the equivalent "0" and "1" integers:

df['isLegendary'] = df['isLegendary'].astype(int)

There are a few other categories that we'll need to convert as well. Let's look at "Type_1" as an example. Pokémon have associated elements, such as water and fire. Our first intuition at converting these to numbers could be to just assign a number to each category, such as: Water = 1, Fire = 2, Grass = 3 and so on. This isn't a good idea because these numerical assignments aren't ordinal; they don't lie on a scale. By doing this, we would be implying that Water is closer to Fire than it is Grass, which doesn't really make sense. 

The solution to this is to create dummy variables. By doing this we'll be creating a new column for each possible variable. There will be a column called "Water" that would be a 1 if it was a water Pokémon, and a 0 if it wasn't. Then there will be another column called "Fire" that would be a 1 if it was a fire Pokémon, and so forth for the rest of the types. This prevents us from implying any pattern or direction among the types. Let's do that:

`def dummy_creation(df, dummy_categories):
    for i in dummy_categories:
        df_dummy = pd.get_dummies(df[i])
        df = pd.concat([df,df_dummy],axis=1)
        df = df.drop(i, axis=1)
    return(df)`

This function first uses `pd.get_dummies` to create a dummy DataFrame of that category. As it's a seperate DataFrame, we'll need to `concat`enate it to our original DataFrame. And since we now have the variables represented properly as separate columns, we `drop` the original column. Having this in a function is nice because we can quickly do this for many categories:

df = dummy_creation(df, ['Egg_Group_1', 'Body_Style', 'Color','Type_1', 'Type_2'])

*Why do we need to create dummy variables?*

A. Some categories are not numerical.
B. Converting multiple categories into numbers implies that they are on a scale.
C. The categories for "Type_1" should all be boolean (0 or 1).
D. All of the above are true.

**Leave a comment with your answer to continue**