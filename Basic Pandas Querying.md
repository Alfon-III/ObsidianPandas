
### New Column

```py
db['new_column'] = df['a'] + df['b']
```

### Selecting & Indexing


Get rows that fulfills condition
```py
sales.loc[sales['Satate'] == 'Kentucky']
```

Get the average of a ```column``` 
```py
sales.loc[sales['Age_group'] == 'Youth (<25)', 'revenue'].mean()
```

Add more constraints
```py
sales.loc[(sales['Age_group'] == 'Youth (<25)') & (sales['Satate'] == 'Kentucky'), 'revenue'].mean()
```

Modify filetred DF

```py
sales.loc[sales['Age_group'] == 'Youth (<25)', 'revenue'] *= 1.03
```

