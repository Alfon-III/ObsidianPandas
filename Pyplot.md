

``` py
plt.hist(df.loc[df['type'] == 'Movie', 'duration'], bins=20, edgecolor='black')

plt.xlabel('Duration (minutes)')
plt.ylabel('Number of Movies')
plt.title('Distribution of Movie Durations')

plt.show()
```

