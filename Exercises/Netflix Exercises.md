$ByChatGPT$

Sources: 

[Amazon Prime Dataset]([https://www.kaggle.com/datasets/shivamb/amazon-prime-movies-and-tv-shows]()
[Netflix Dataset](https://www.kaggle.com/datasets/shivamb/netflix-shows?resource=download)
[Disney Dataset](https://www.kaggle.com/datasets/shivamb/disney-movies-and-tv-shows)


> [!todo]
> - [x]  **Task 1**: Display the first 5 rows of the DataFrame.
> - [x]  **Task 2**: Check the data types of each column in the DataFrame.
> - [x]  **Task 3**: How many rows and columns are there in the DataFrame?
> - [x]  **Task 4**: Remove the columns 'director', 'cast', and 'description' from the DataFrame.
> - [x]  **Task 5**: Replace any missing values in the 'date_added' column with the current date (today's date).
> - [x]  **Task 6**: Sort the DataFrame in ascending order based on the 'release_year' column.
> - [x]  **Task 7**: How many movies and series are included in the DataFrame? Count the occurrences of each type.
> - [x]  **Task 8**: Create a new column 'age' that contains the age of each movie/series since its release year.
> - [x]  **Task 9**: Extract the top 3 most common countries from the 'country' column.
> - [x]  **Task 10**: Filter the DataFrame to only show movies with a rating higher than 8.0.
> - [ ]  **Task 11**: Calculate the average duration of movies and series separately.
> - [ ]  **Task 12**: Group the data by 'rating' and 'type' and calculate the maximum 'duration' in each group.
> - [ ]  **Task 13**: Create a new DataFrame that contains only movies released in the last 5 years.
> - [ ]  **Task 14**: Find the movie/series with the longest duration.
> - [ ]  **Task 15**: Plot a bar chart showing the number of movies/series released each year.

##### Task 1: Display the first 5 rows of the DataFrame.
``` py
df.head(5)
```

##### **Task 2**: Check the data types of each column in the DataFrame.

df.dtypes

If a type is `object` you can use some built-in functions to transform from  a string to datetime. 

> [!info] 
> In case of error, add these labels: 
> If `coerce`, then invalid parsing will be set as NaN.
> If `ignore`, then invalid parsing will return the input.
>`errors='coerce'`
> `errors='ignore'`
> [Source](https://pandas.pydata.org/docs/reference/api/pandas.to_numeric.html)


``` py
df['date_added'] = pd.to_datetime(df['date_added'], format='%B %d, %Y', errors='coerce')
```

#####  **Task 3**: How many rows and columns are there in the DataFrame?

We have various options

| **Function**  |                      **Explanation**                      |
| --------- |:-----------------------------------------------------:|
| df.info() |           General info: Size and dataTypes            |
| df.shape  |                  $$(rows, columns)$$                  |
| df.size   |            $$ size = rows\times columns$$             |
| df.ndim   |                 Number of dimensions                  |
| df.axes   | Return a list representing the axes of the DataFrame. |
| df.index  |       The index (row labels) of the DataFrame.        |

##### **Task 4**: Remove the columns 'director', 'cast', and 'description' from the DataFrame.

[Drop Info](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop.html#)

``` py
df.drop(columns=['column_1', 'column_2, 'column_3'])
df.drop(['B', 'C'], axis=1)
```


``` py
df_aux = df.copy()
print(df_aux.shape)
df_aux = df_aux.drop(columns=['director', 'cast', 'description'])
print(df_aux.shape)

```

> [!tip] 
> *You can use inplace to avoid reasigning the value*
> ``` py
df_aux.drop(columns=['director', 'cast', 'description'], inplace=True)

##### **Task 5**: Replace any missing values in the 'date_added' column with the current date (today's date).

``` py
today_date = datetime.today().date()
df['date_added'] = pd.to_datetime(df['date_added'], format='%B %d, %Y', errors='coerce')
df.loc[df['date_added'].isna(), 'date_added'] = today_date
```

Extra: order by date_added 

``` py
df['date_added'] = pd.to_datetime(df['date_added'], format='%B %d, %Y', errors='coerce')
today_date = datetime.today().date()
df.loc[df['date_added'].isna(), 'date_added'] = today_date


df.date_added = pd.to_datetime(df.date_added)
df.loc[df['date_added'] < datetime(2022, 1, 1)].sort_values(by='date_added', ascending=False)
```


##### **Task 6**: Sort the DataFrame in ascending order based on the 'release_year' column.
``` py
df.sort_values(by='release_year', ascending=False)
```

##### Task 7: How many movies and series are included in the DataFrame? Count the occurrences of each type.

``` py
df.value_counts(['type'])
```

##### **Task 8**: Create a new column 'age' that contains the age of each movie/series since its release year.

``` py
df['age'] = df.date_added.dt.year - df.release_year
df['age']

df.loc[df['date_added'].dt.year != '2023']
```

##### **Task 9**: Extract the top 3 most common countries from the 'country' column.

``` py
df.value_counts(['country']).nlargest(3)
```

##### **Task 10**: Filter the DataFrame to only show movies with a rating higher than '8'.

##### Task Extra: Get the duration in minutes of the TV Shows and make a Graph

``` py
df['duration'] = df.loc[df['type'] == 'Movie', 'duration'].apply(lambda x: int(x.split()[0]) if isinstance(x, str) else x)

df.loc[df['type'] == 'Movie'].sort_values(by='duration', ascending=False)[['title', 'duration']]
```

Make a Graph

[[Pyplot]]