Wow, "{{ pokemon }}" is also my favorite!

The dataset we'll be using is the compilation of stats and traits for the Pokémon video games. Pokémon is a popular game for generations of Nintendo handheld video game consoles where players collect and train animal-like creatures called Pokémon. We'll be creating a model to try to predict whether a Pokémon is a legendary Pokémon, a rare type of Pokémon who's the only one of its species.

There are a lot of existing compilations of Pokémon stats, but we'll be using a .CSV version [found on Kaggle](https://www.kaggle.com/alopez247/pokemon). There's a download button on the website, so save the file to your computer and we can begin.

First, we need to read in the CSV file. We'll be doing so using Pandas:

`df = pd.read_csv('/path/to/file/pokemon.csv')`

First, let's see what the categories of data are. This was also available on the Kaggle page, but that won't be the case for most real-world data:

```
df.columns
>>> Index(['Number', 'Name', 'Type_1', 'Type_2', 'Total', 'HP', 'Attack',
       'Defense', 'Sp_Atk', 'Sp_Def', 'Speed', 'Generation', 'isLegendary',
       'Color', 'hasGender', 'Pr_Male', 'Egg_Group_1', 'Egg_Group_2',
       'hasMegaEvolution', 'Height_m', 'Weight_kg', 'Catch_Rate',
       'Body_Style'],
      dtype='object')
```

Okay so we have a lot of types of data here! Some of these descriptions might be confusing to those who aren't very familiar with the games. That's okay, we'll narrow our focus a little and only select categories we think will be relevant. It's always nice to have more data to train the model with, but it also takes time to clean and prepare that data. We'll be keeping it simple here:

```
df = df[['isLegendary','Generation', 'Type_1', 'Type_2', 'HP', 'Attack', 'Defense', 'Sp_Atk', 'Sp_Def', 'Speed','Color','Egg_Group_1','Height_m','Weight_kg','Body_Style']]
```

*Which library did we use to read our CSV file?*

**Leave a comment with your answer to continue**