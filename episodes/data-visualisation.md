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

For this module, we will use a different version of our circulation data that is in a tidy data format, where each variable forms a column, each observation forms a row, and each type of observation unit forms a row. If your workshop included the Tidy Data episode, you should be set and have an object called `df_long` in your Jupyter environment. If not, we’ll read that dataset in now, as it was provided for this lesson.


``` python
#import if it is already not
import pandas as pd
```

If `df_long` isn’t loaded already, we can read it in using `read_csv`. Note, if it isn’t present in your local `data/` folder.

``` python
df_long = pd.read_csv('data/circ_long.tsv', sep="\t")
```

We are using a couple of new parameters in our `read_csv` function above. Since the file we want to read in is a tab-separated values (TSV) file, we tell our `read_csv` function that using the `sep="\t"` parameter. `\t` is encoding for tab character in Python. Other separators or delimeters could include `|` or `;` depending on your data file.

Let’s look at the data:

``` python
df_long.head()
```

``` output
            branch                  address  ... circulation        date
0     Albany Park     5150 N. Kimball Ave.  ...        8427  2011-01-01
1         Altgeld    13281 S. Corliss Ave.  ...        1258  2011-01-01
2  Archer Heights      5055 S. Archer Ave.  ...        8104  2011-01-01
3          Austin        5615 W. Race Ave.  ...        1755  2011-01-01
4   Austin-Irving  6100 W. Irving Park Rd.  ...       12593  2011-01-01
```

## Convert a column to datetime

In order to plot this data over time we need to do two things to prepare it first. First, we need to tell Python that the data column is a [datetime object](https://docs.python.org/3/library/datetime.html) using the Pandas `to_dateime` function. Second, we assign the date column as our index for the data. These two steps will set up our data for plotting.

``` python
df_long['date']= pd.to_datetime(df_long['date'])
```

The above converts our date column to a datetime object. Let’s confirm it worked.

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
 5   year         11556 non-null  int64         
 6   month        11556 non-null  object        
 7   circulation  11556 non-null  int64         
 8   date         11556 non-null  datetime64[ns]
dtypes: datetime64[ns](1), float64(1), int64(3), object(4)
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

``` output
                     branch                  address  ...    month  circulation
 date                                                 ...                      
 2011-01-01     Albany Park     5150 N. Kimball Ave.  ...  january         8427
 2011-01-01         Altgeld    13281 S. Corliss Ave.  ...  january         1258
 2011-01-01  Archer Heights      5055 S. Archer Ave.  ...  january         8104
 2011-01-01          Austin        5615 W. Race Ave.  ...  january         1755
 2011-01-01   Austin-Irving  6100 W. Irving Park Rd.  ...  january        12593

```

## Plotting with Pandas 

Ok! We are now ready to plot our data. Since this data is monthly data, we can plot the circulation data over time.

At first, let’s focus on a specific branch. We can select the rows for the Albany Park branch:

``` python
albany = df_long[df_long['branch'] == 'Albany Park']
```

``` python
albany.head()
```

``` output
                   branch               address  ...    month  circulation
  date                                           ...                      
  2011-01-01  Albany Park  5150 N. Kimball Ave.  ...  january         8427
  2016-01-01  Albany Park                   NaN  ...  january        10905
  2017-01-01  Albany Park                   NaN  ...  january        11031
  2022-01-01  Albany Park   3401 W. Foster Ave.  ...  january         5561
  2018-01-01  Albany Park                   NaN  ...  january         9381
```

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

- We can pass parameters to matplotlib's `.plot()` function to assign a plot title, to declare a figsize - which accepts a width and height in inches - and to change the color of the line.
- Next we'll add text labels for the x and y axis using `.xlabel()` and `.ylabel`.
- Finally, we need a separate function `.show()` to display the plot using matplotlib.


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


One advantage that Plotly provides over matplotlib is that it has some interactive features out of the box. Hover your cursor over the lines in the output to find out more granular data about specific branches over time.


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
