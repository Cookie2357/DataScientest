The Module is devided into three sections
1. Analysis of numerical (continuous) variables
2. Analysis of qualitative (discrete) and temporal variables
3. Statistical tests (Correlation and dependence of variables)

# 1. Analysis of numerical (continuous) variables

`so.unique()` to display the unique values of a variable. Where so is a Series Object
*Example:* `df['age'].unique()`

`df.info()` gives a short overview of the data. Including variables, their types and more. 

`df.dtypes()` gives a series object that has the types of the variables. We can apply series methods like value_counts() to get the number of variables with a given type.

**Definition**: *Inter Quantile Range*:  $IQR = Q_3 - Q_1$ 

**Definition**: *extreme value*:  $e$ is an extreme value if $e <  Q_1 - 1.5 * IQR$ or $e >  Q_3 + 1.5 * IQR$

**Definition**: *outlier*: Value that is not feasible. *Example*: -10 cm for a persons height
*Note* Outliers should always be removed. Extreme Values are generally kept. Depending on the use case. 

`so.quantile(q = list)` for a list with values in $[0, 1]$ it returns the respective quantiles.
*Note*: Not an Interval!

*Rule of Thumb*: Quantiles are better measures for data distribution. Hence use quantile(0.05) instead of min, quantile(0.95) instead of max and median() instead of mean(). They are more robust against extreme values. 

`np.random.normal(loc, scale, size)` samples size many datapoints from N(loc, scale). 

`np.random.seed()` takes an int to set a seed for the random number generator. 


# 2. Analysis of qualitative (discrete)

`df.select_dtypes(include = list)` allows us create a dataframe with only those types included in the list.
*Example*: `df.select_dtypes(include = 'object')`

`so.value_counts(normalize)` get modalities of values. 
*normalize* is an optional boolean parameter.

`pd.qcut(col, listOfLabels, q = number of cuts)` us it to make a continuous variable discrete. With q many values. 
*Example*: `pd.qcut(df['temperature'], labels = [0, 1, 2, 3], q = 4)`

Using groupby and agg explained in pandas.md we can make continous variables depend on discrete ones like so: `# TODO Set Link`
*Example*: `df.groupby(['vacances', 'temperature_labels']).agg({'nb_locations': 'sum'})``# get for each value of vacation and temperature, the total number of bookings for that specific case`

# 3. Temporal Variables

`pd.to_datetime(col)` convert col into datatime format

`pandas.Grouper()` creates a pandas.grouper object. We use it with *key* which is the columns name and *freq* which is either 'y', 'm' or 'd' and groups into years, months or days respectively. 

Use the Grouper object in the groupby method by simply including it in the list. 
*Example*: `df.groupby([grouper_mois, df["conditions_meteo"]]).agg({'nb_locations':'mean'}).unstack()`

`unstack()` -> Not explained. But it somehow moves the weather conditions in the columns. 
## Correlation:

### quantitative variables

Visually using a QQPlot to match distribution with normal distribution. (See Seaborn hopefully)

`np.corrcoef(X, Y)` to get the correlation matrix

(Spearmans) Correlation between X and Y is given by: 

$ r(X, Y) = \frac{cov(X, Y)}{\sigma_X \sigma_Y}$

where cov(X, Y) is the covariance between X and Y and \sigma_i is the standard deviation of i. 

$r(X, Y) \in [-1, 1]$. If $r(X, Y) \in [-0.5, 0.5]$. Generally the correlation is weak. And string otherwise. However, this also depends on the use case. 

`df.corr()` gives the correlation of all variables in df. 

### Carrying out a statistical test:

1. Formulate Hypothesis h0 m = m0 for some theoretical average m0; h1 m ~ m0 for $ ~ \in \{<, >, \neq, \}$
If the observed difference is significat we reject h0 and assert h1. *Note* If if the observed difference is not significant we can not reject h0 but we also do not assert h0. With statistical testing we never assert h0. 
2. Choose a test and a threshold. Depending on the nature of the variables and the expected corrolation there are different tests available. We learned: 
- ANOVA
- $\chi^2$
- t-test (student test)
