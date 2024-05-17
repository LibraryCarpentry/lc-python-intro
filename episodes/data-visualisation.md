---
title: 'Data Visualisation'
teaching: 20
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions 

- How can I use Python tools like Pandas and Plotly to visualize library circulation data?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Generate plots using Python to interpret and present data on library circulation.
- Apply data manipulation techniques with pandas to prepare and transform library circulation data into a suitable format for visualization.
- Analyze and interpret time-series data by identifying key trends and outliers in library circulation data.

::::::::::::::::::::::::::::::::::::::::::::::::

For this module, we will use the tidy (long) version of our circulation data, where each variable forms a column, each observation forms a row, and each type of observation unit forms a row. If your workshop included the Tidy Data episode, you should be set and have an object called `df_long` in your Jupyter environment. If not, we’ll read that dataset in now, as it was provided for this lesson.


``` python
#import if it is already not
import pandas as pd
df_long = pd.read_pickle('data/df_long.pkl')
```

Let’s look at the data:

``` python
df_long.head()
```

|     | branch         | address                 | city    | zip code | ytd    | year | month   | circulation |
|-----|----------------|-------------------------|---------|----------|--------|------|---------|-------------|
| 0   | Albany Park    | 5150 N. Kimball Ave.    | Chicago | 60625.0  | 120059 | 2011 | january | 8427        |
| 1   | Altgeld        | 13281 S. Corliss Ave.   | Chicago | 60827.0  | 9611   | 2011 | january | 1258        |
| 2   | Archer Heights | 5055 S. Archer Ave.     | Chicago | 60632.0  | 101951 | 2011 | january | 8104        |
| 3   | Austin         | 5615 W. Race Ave.       | Chicago | 60644.0  | 25527  | 2011 | january | 1755        |
| 4   | Austin-Irving  | 6100 W. Irving Park Rd. | Chicago | 60634.0  | 165634 | 2011 | january | 12593       |

## Convert year and month to datetime

In order to plot this data over time we need to do two things to prepare it first. First, we need to combine the year and month columns into a single [datetime](https://docs.python.org/3/library/datetime.html) column using the Pandas `to_datetime` function. Second, we assign the date column as our index for the data. These two steps will set up our data for plotting.

``` python
df_long['date'] = pd.to_datetime(df_long['year'].astype(str) + '-' + df_long['month'], format='%Y-%B')
```

Let's unpack that code:

- `df_long['date']` - First, we create a new `date` column. 
- `pd.to_datetime()` - Next we package everything into a datetime object.
- `df_long['year'].astype(str)` - We use the `.astype(str)` method to convert the year column to a string
- `+ '-' + df_long['month'],` - We concatenate a `-` to the string as a separator, followed by the month column.
- `format='%Y-%B'` - We pass the datetime parameter to tell Python to expect a 4 digit year (%Y), followed by a dash, followed by the month's full name (%B).

If we take a look at the date column, we'll see that datetime automatically adds a day (always `01`) in the absence of any specific day input.

```python
df_long['date']
```
```output
0       2011-01-01
1       2011-01-01
2       2011-01-01
3       2011-01-01
4       2011-01-01
           ...    
11551   2022-12-01
11552   2022-12-01
11553   2022-12-01
11554   2022-12-01
11555   2022-12-01
Name: date, Length: 11556, dtype: datetime64[ns]
```

``` python
df_long.info()
```

``` output
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 11556 entries, 0 to 11555
Data columns (total 9 columns):
 #   Column       Non-Null Count  Dtype         
---  ------       --------------  -----         
 0   branch       11556 non-null  object        
 1   address      7716 non-null   object        
 2   city         7716 non-null   object        
 3   zip code     7716 non-null   float64       
 4   ytd          11556 non-null  int64         
 5   year         11556 non-null  object        
 6   month        11556 non-null  object        
 7   circulation  11556 non-null  int64         
 8   date         11556 non-null  datetime64[ns]
dtypes: datetime64[ns](1), float64(1), int64(2), object(5)
memory usage: 812.7+ KB
```

That worked! Now, we can make the datetime column the index of our DataFrame. In the Pandas episode we looked at Pandas default numerical index, but we can also use `.set_index()` to declare a specific column as the index of our DataFrame. Using a datetime index will make it easier for us to plot the DataFrame over time. The first parameter of `.set_index()` is the column name and the `inplace=True` parameter allows us to modify the DataFrame without assigning it to a new variable.


``` python
df_long.set_index('date', inplace=True)
```

If we look at the data again, we will see our index will be set to date.

``` python
df_long.head()
```

|            | branch         | address                 | city    | zip code | ytd    | year | month   | circulation |
|------------|----------------|-------------------------|---------|----------|--------|------|---------|-------------|
| date       |                |                         |         |          |        |      |         |             |
| 2011-01-01 | Albany Park    | 5150 N. Kimball Ave.    | Chicago | 60625.0  | 120059 | 2011 | january | 8427        |
| 2011-01-01 | Altgeld        | 13281 S. Corliss Ave.   | Chicago | 60827.0  | 9611   | 2011 | january | 1258        |
| 2011-01-01 | Archer Heights | 5055 S. Archer Ave.     | Chicago | 60632.0  | 101951 | 2011 | january | 8104        |
| 2011-01-01 | Austin         | 5615 W. Race Ave.       | Chicago | 60644.0  | 25527  | 2011 | january | 1755        |
| 2011-01-01 | Austin-Irving  | 6100 W. Irving Park Rd. | Chicago | 60634.0  | 165634 | 2011 | january | 12593       |


## Plotting with Pandas 

Ok! We are now ready to plot our data. Since this data is monthly data, we can plot the circulation data over time.

At first, let’s focus on a specific branch. We can select the rows for the Albany Park branch:

``` python
albany = df_long[df_long['branch'] == 'Albany Park']
```

``` python
albany.head()
```

|            | branch      | address              | city    | zip code | ytd    | year | month   | circulation |
|------------|-------------|----------------------|---------|----------|--------|------|---------|-------------|
| date       |             |                      |         |          |        |      |         |             |
| 2011-01-01 | Albany Park | 5150 N. Kimball Ave. | Chicago | 60625.0  | 120059 | 2011 | january | 8427        |
| 2012-01-01 | Albany Park | 5150 N. Kimball Ave. | Chicago | 60625.0  | 83297  | 2012 | january | 10173       |
| 2013-01-01 | Albany Park | 5150 N. Kimball Ave. | Chicago | 60625.0  | 572    | 2013 | january | 0           |
| 2014-01-01 | Albany Park | 5150 N. Kimball Ave. | Chicago | 60625.0  | 50484  | 2014 | january | 35          |
| 2015-01-01 | Albany Park | NaN                  | NaN     | NaN      | 133366 | 2015 | january | 10889       |

Now we can use the `plot()` function that is built in to pandas. Let’s try it:

``` python
albany.plot()
```

![](fig/albany-plot-1.png){alt="Line plot of zip code, ytd, year, and circulation numbers over time from the albany DataFrame"}

That's interesting, but by default `.plot()` will use a line plot for all numeric variables of the DataFrame. This isn’t exactly what we want, so let’s tell `.plot()` what variable to use by selecting the `circulation` column.


``` python
albany['circulation'].plot()
```

![](fig/albany-circ-3.png){alt="Line plot of the Albany Park branch circulation showing a big drop from 2013 to 2014."}

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: challenge

## Analyze the Circulation Trends

Examine the line graph depicting library circulation data. You will notice two significant periods where the circulation drops to zero: first in March 2020 and then a two-year zero circulation period starting in 2012. Evaluate the graph and identify any trends, unusual patterns, or notable changes in the data.

::::::::::::::::::::::::::::::::::::::::::::::::::: solution

The significant drop in circulation in March 2020 is likely due to the COVID-19 pandemic, which caused widespread temporary closures of public spaces, including libraries. 

The drop from 2012 through part of 2014 corresponds to the reconstruction period of the Albany Park Branch. The original building at 5150 N. Kimball Avenue was demolished in 2012, and a new, modern building was constructed at the same site. The new Albany Park Branch opened on September 13, 2014, at 3104 W. Foster Avenue in the North Park neighborhood of Chicago. More details about this renovation can be found on the Chicago Public Library webpage: [Chicago Public Library - Albany Park](https://www.chipublib.org/news/stories-we-tell-albany-park-exhibit/).
::::::::::::::::::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Use Matplotlib for more detailed charts

What if we want to alter the axis labels and the title of the graph. In order to do that, we need to first import `matplotlib`, an extensive plotting package in Python that lets us alter all aspects of a graph.

- We can pass parameters to Matplotlib's `.plot()` function to assign a plot title, to declare a figsize - which accepts a width and height in inches - and to change the color of the line.
- Next we'll add text labels for the x and y axis using `.xlabel()` and `.ylabel`.
- Finally, we need a separate function `.show()` to display the plot using Matplotlib.


``` python
# the plotting package pandas is using under the hood to `plot()`  
import matplotlib.pyplot as plt

albany['circulation'].plot(title='Circulation Count Over Time', figsize=(10, 5), color='blue')
# Adding labels and showing the plot
plt.xlabel('Date')
plt.ylabel('Circulation Count')
plt.show()
```

![](fig/albany-circ-labeling-5.png){alt="Line plot of the Albany Park branch circulation with matplotlib styles applied."}

### Changing plot types with Matplotlib

What if we want to use a different plot type for this graphic? To do so, we can change the `kind` parameters in our `.plot()` function.

``` python
albany['circulation'].plot(kind='area', title='Circulation Count Area Plot at Albany Park', alpha=0.5)
plt.xlabel('Date')
plt.ylabel('Circulation Count')
plt.show()
```
![](fig/albany-circ-area-7.png){alt="Area plot of the Albany Park branch circulation."}

We can also look at our circulation data as a histogram.

``` python
albany['circulation'].plot(kind='hist', bins=20, title='Distribution of Circulation Counts at Albany Park')
plt.xlabel('Circulation Count')
plt.show()
```

![](fig/albany-circ-hist-9.png){alt="histogram of the Albany branch circulation."}

## Use Plotly for interactive plots 

Let’s switch back to the full DataFrame in `df_long` and use another
plotting package in Python called Plotly. First let’s install and then use the package.

```python
# uncomment below to install plotly if the import fails. 
# !pip install plotly
import plotly.express as px
```

Now we can visualize how circulation counts have changed over time for selected branches. This can be especially useful for identifying trends, seasonality, or data anomalies. We willfirst create a subset of our data to look at branches starting with the letter 'A'. Feel free to select different branches. After subsetting, we will sort our new DataFrame by date and then plot our data by date and circulation count.

``` python
# Creating a line plot for a few selected branches to avoid clutter
selected_branches = df_long[df_long['branch'].isin(['Altgeld',
 'Archer Heights',
 'Austin',
 'Austin-Irving',
 'Avalon'])]
selected_branches = selected_branches.sort_values(by='date')
```

``` python
fig = px.line(selected_branches, x=selected_branches.index, y='circulation', color='branch', title='Circulation Over Time for Selected Branches')
fig.show()
```

Here is a view of the [interactive output of the Plotly line chart](learners/line_plot_int.html).  


One advantage that Plotly provides over Matplotlib is that it has some interactive features out of the box. Hover your cursor over the lines in the output to find out more granular data about specific branches over time.


### Bar plots with Plotly

Let’s use a barplot to compare the distribution of circulation counts
among branches. We first need to group our data by branch and sum up the circulation counts. Then we can use the bar plot to show the
distribution of total circulation over branches.

``` python
# Aggregate circulation by branch
total_circulation_by_branch = df_long.groupby('branch')['circulation'].sum().reset_index()

# Create a bar plot
fig = px.bar(total_circulation_by_branch, x='branch', y='circulation', title='Total Circulation by Branch')
fig.show()
```

Here is a view of the [interactive output of the Plotly bar chart](learners/bar_plot_int.html).  



::: keypoints
-   Explored the use of pandas for basic data manipulation, ensuring correct indexing with DatetimeIndex to enable time-series operations like resampling.
-   Used pandas’ built-in plot() for initial visualizations and faced issues with overplotting, leading to adjustments like data filtering and resampling to simplify plots.
-   Introduced Plotly for advanced interactive visualizations, enhancing user engagement through dynamic plots such as line graphs, area charts, and bar plots with capabilities like dropdown selections.
:::
