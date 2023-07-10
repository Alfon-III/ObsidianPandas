To access the ``csv``, you have to create a new google Colab notebook and navigate the left navigation bar to open the ```drive```  folder in order to access the ``.csv ``. 

To get the path, click the three dots and ``copy path`` 

```py
import pandas as pd

from google.colab import drive
path = '/content/drive/MyDrive/DataSets/netflix_titles.csv'
df = pd.read_csv(path)
df.head(5)
```



