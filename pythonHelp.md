

# PYTHON
## Dataframes

#### read file, flexible delimiter
`df = pd.read_csv("whitespace.csv", header=None, delim_whitespace=True)`

#### create empty dataframe
`dfObj  =  pd.DataFrame(columns=['User_ID',  'UserName',  'Action'])`
#### append rows to dataframe
`dfObj  =  dfObj.append({'User_ID':  25,  'UserName':  'Jack',  'Action':  'Login'},  ignore_index=True)`

#### append columns to dataframe
```
dfObj['UserName'] = ['Riti', 'Aadi', 'Jack']
dfObj['Name'] = ['Riti', 'Aadi', 'Jack']
```
#### Add rows to an empty dataframe at existing index
```
dfObj.loc['a'] = [23, 'Riti', 'Login']
dfObj.loc['b'] = [24, 'Aadi', 'Logout']
dfObj.loc['c'] = [25, 'Jack', 'Login']
```


#### getting the dimensions
```
In  [5]: df.shape
Out[5]:  (4,  3)
```
#### selecting with row numbers
'If you have a dataframe like':
```
df = pd.DataFrame(data={
'X': [1.5, 6.777, 2.444, pd.np.NaN],
 'Y': [1.111, pd.np.NaN, 8.77, pd.np.NaN], 
 'Z': [5.0, 2.333, 10, 6.6666]})
```
'Instead of iloc,you can use .loc with row index and column name like':
```
df.loc[row_indexer,column_indexer]=value
df.loc[[0,3],'Z'] = 3
```
Output:
```
     X       Y        Z
0    1.500   1.111    3.000
1    6.777   NaN      2.333
2    2.444   8.770    10.000
3    NaN     NaN      3.000
```
#### iterate over rows 
```
for row in df.iterrows():
   print row['c1'], row['c2']
```

#### get column as series
`s = pd.Series(df['c1'])`
#### get absolute value of series
`s.abs()`

#### exclude indices from series
`s = s[~s.index.isin([0, 3, 4])]`

#### List unique values in the df['name'] column
`df.name.unique()`
#### get number of unique values in the df['name'] column
`len(df['name].unique()) `
#### get value counts
`s.value_counts(dropna=False)`
`s.value_counts()`
#### normalized value counts:
With normalize set to True, returns the relative frequency by dividing all values by the sum of values.
`s.value_counts(normalize=True)`
#### column to list
`s = pd.Series(df['name']).tolist()`

#### Column Slicing
To select rows whose column value equals a scalar,  `some_value`, use  `==`:
```
df.loc[df['column_name'] == some_value]
```
To select rows whose column value is in an iterable,  `some_values`, use  `isin`:
```
df.loc[df['column_name'].isin(some_values)]
```
Combine multiple conditions with  `&`:
```
df.loc[(df['column_name'] >= A) & (df['column_name'] <= B)]
```
Note the parentheses. Due to Python's  [operator precedence rules](https://docs.python.org/3/reference/expressions.html#operator-precedence),  `&`  binds more tightly than  `<=`  and  `>=`. Thus, the parentheses in the last example are necessary. Without the parentheses
```
df['column_name'] >= A & df['column_name'] <= B
```
is parsed as
```
df['column_name'] >= (A & df['column_name']) <= B
```
which results in a  [Truth value of a Series is ambiguous error](https://stackoverflow.com/questions/36921951/truth-value-of-a-series-is-ambiguous-use-a-empty-a-bool-a-item-a-any-o).

----------

To select rows whose column value  _does not equal_  `some_value`, use  `!=`:

```
df.loc[df['column_name'] != some_value]
```

`isin`  returns a boolean Series, so to select rows whose value is  _not_  in  `some_values`, negate the boolean Series using  `~`:

```
df.loc[~df['column_name'].isin(some_values)]
```

#### coerce column to numeric
`df["a"] = pd.to_numeric(df["a"], errors='coerce')`
(sets problems to NaN)
`df["a"] = pd.to_numeric(df["a"], errors='ignore')` 
(returns orig series untouched




## Matplotlib
#### Add subplots to figure
in the parens: 1st digit = number of rows , 2nd digit = number of columns, 3rd digit = index of the subplot
```
fig = plt.figure(figsize=(20,15))
a1 = fig.add_subplot(431)
a2 = fig.add_subplot(432)
a3 = fig.add_subplot(433)
a4 = fig.add_subplot(434)
a5 = fig.add_subplot(435)
a6 = fig.add_subplot(436)
a7 = fig.add_subplot(437)
a8 = fig.add_subplot(438)
a9 = fig.add_subplot(439)
a10 = fig.add_subplot(4,3,10) 
```







## Seaborn
#### violin plot
```
ax = sns.violinplot(x="day", y="total_bill", hue="sex",
                     data=tips, palette="Set2", split=True,
                     scale="count", 
                     inner="quartile").set_title('title')
```



> Written with [StackEdit](https://stackedit.io/).
