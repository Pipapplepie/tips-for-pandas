# tips-for-pandas
some tips to data analysis in python (mainly pandas dataframes, matplotlib, etc.)

Start with the classic data-analysis dundle of 3;

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt    # I like seaborn, as well

# import dataset
df = pd.read_csv('file.csv')
```

## for loop in a list

```python
x = list(df['time'].unique())

# in case your dataframe is not ordered with time
x = sorted(x) 
```

Basically, for loop in list can shorten your code greatly.

```python
# my time column is of string type: e.g., 2001-01-01
# using this format as plot label will seem clustered, so I shorten it below
x_simplified = [time[-2:] for time in x]
```

## Lambda function in count vs. time statistics

Now, I want to count rows w.r.t. dates.

If you know SQL, you can use aggregate function to do this in one line.

```sql
SELECT count(*)
FROM dataset
GROUP BY date
```

Below is the one-line python code, operating like the aggregate function in SQL.

```python
y = list(map(lambda x: df['time'].loc[df['time']==x].count(), x))
```

```python
plt.plot(x_simplified, y)

# add captions and labels
plt.title('cases count per day')
plt.xlabel('time')
plt.ylabel('cases count')

# show the plot
plt.show()
print(f'the case minimum: {min(y)} per day.')
print(f'the case maximum: {max(y)} per day.')
```

