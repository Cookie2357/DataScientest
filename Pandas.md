
# Pandas

`Import pandas as pd`

`pd.DataFrame(data, index : list, columns : list)`

Create a DataFrame from data. 
That is indexed by _index_ and the columns are named after _columns._
_Data_ can be a NPA, a dictionary or another DataFrame

`pd.read_csv(filepath_or_buffer, sep , header , index_col )`

Create a DataFrame from a CSV file.
The relative path is passed as a string to _filepath_or_buffer._
The separator is given by _sep_ usually ‘,’ or ‘;’.
The parameter _header_ is passed the index of the row that contains the column names. 0 for first None if not included.
The parameter _index_col_ is passed the name or index of the column that contains the database indices. Possible values: 0, ‘ID’, None

  
Display specific column(s) with
`df[list of column names]`

## Methods and Attributes of DataFrames

`df.head(n)`
Get the first n entries of df

`df.tail(n)`
Get the last n entries of df.

`df.loc[j]`
Method to access lines with label 'j', lists or slices.
**Note:** loc works with [ ].
**Note:** To access slices indeces must be unique.

  
`df.iloc[]`
Method to access lines and slices with numeric values (similar to NPAs)
Example: df.iloc[0:3, 5:10]
**Note**: iloc can be used in the presence of duplicates.

DFs can be indexed conditionally much like NPAs.
*Example*: `df.loc[df[‘col_3’] == 3] # returns those rows where the value in col_3 = 3`

`df.describe()`
Return a summary of descriptive statistics for numerical features
Note: All features are treated as numerical by describe
  
`df.columns`
Get a list of column names

`df.shape`
Get the dimension of df

## Data Cleaning:

`df.duplicated()`
Returns a pandas Series Object (?) that tells for each row if it is a duplicate or not. The first appearance of each row is not treaded as a duplicate.

`df.drop_duplicates(subset, keep, inplace)`
*subset*: list of column(s) that should be considered. Default: None (all columns are considered)
*keep*: possible values: ‘first’ (default value, keep first occurrence), ‘last’ (keep last occurrence), False (remove both)
*inplace*: True: overwrite current object, False (default): return a modified copy of the object.


`df.replace(to_replace, value)`
*to_replace*: tuple of values to be replaced
*value*: tuple of values to replace the old ones

  
`df.rename(dic, axis)`
Rename columns of a DataFrame
*dic*: a dictionary that has old name - new name pairs
*axis*: set to 1 you rename columns

  
`df.astype()`
Modify the type of a column. Expects a dictionary or a single column. 
*Example single column*: `df[‘col_1’] = df[‘col_1’].astype(‘int’)`

  

`df.apply(func, axis)`
*axis*: 0 apply to rows, 1 apply to columns
Typically func is an anonymous lambda function.
Example: `df.apply(lambda x: np.sin(x + 2), axis = 0)`

  

## Missing Values:

`df.isna()` or  `df.isnull()` they are semantically equivalent
Returns a DataFrame of same dimensions with entries True if NaN False else

`df.any(axis)`
Determine which columns (axis = 0) or rows (axis = 1) have NaN values.

`df.fillna()`
Replace missing values with specified value
*Example* : `df.fillna(-1)`

  
`df.dropna(axis, how, subset)`
Delete missing values
*subset*: list of column(s)/row(s) that should be considered. Default: None (all columns/rows are considered)
*axis*: 0 for rows, 1 for colums
*how*: ‘any’ delete if any value NaN, ‘all’ delete if all values NaN

## Data Processing:

### Filtering
For filtering we use & instead of and, | instead of or and  -  instead of not
Example: `df[(df['year'] == 1979) & (df['surface']> 60)] `

### Ordering:

`df.sort_values(by = ['col_i', 'col_j'], ascending)`
*by*: expects a list of column names. First the rows of the DF will be sorted according to `col_i`. If two rows have the same value in `col_i` they will be sorted by `col_j`. 
*ascending*: Boolean 

### Merging:

Two DFs can be merged if they have a common column.
`df.merge(right, on, how)`
*right*: DF that is to be merged with the called upon DF.
*on*: Column name that should be merged on
*how*: allows to choose type of join. Possible values:

 - `inner`: not recommended. Returns DF for all this rows where espective value is found in both DFs.
 - `outer`: Can generate a lot of NaNs. Match those that occur in both and fill others with NaN. (No row deleted)
 - `left`: returns all the rows of left DF
 - `right`: returns all the rows of the right DF

**Note**: Merge makes index numerical. We can `set_index()` with name of col or with NPA. Use`reset_index` to go back to numerical.

`df.index`
returns the index of df

`concat(objects, axis)`
pd.concat works just as for NPAs. Here non matching dimensions are filled with NaN

### Grouping

`df.groupby(col_name)`
Returns a DataFrameGroupBy Object. It splits so that the rows that have the same value in `col_name` are grouped. 

We can apply standard statistical procedures to a DataFrameGroupBy Object
*Example*: `df.groupby(col_name).mean()`
As methods of DataFrameGroupBy Object they return a df by combining the groups. 

`dfg.agg(dictionary)`
allows us to apply different functions to different columns. 
*Example*: `df.groupby(col_name).agg({col_j : 'mean', col_k : some_function})`


`pd.crosstab(col_1, col_2, normalize)`
returns a DF with `col_1 ` row indices and `col_2` as column indices. `pd.crosstab(col_1, col_2, normalize)[0,0]` gives the number of occurences of feature 0 from `col_1` such that also feature 0 from `col_2` is also present. 
 *Normalize* is optional. If 0 we normalise over rows. If 1 we normalise over columns. 
