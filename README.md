# ECE2112: Programming Assignment 4
**Ryan Joseph C. Dungca, 2ECE-D**

This repository contains code for Programming Assignment 4 of the course ECE2112, covering three problems related to _Module 4: Data Wrangling and Visualization_. The creation of this code demonstrates the ability to:
- filter tabular data using several categorical and numerical conditions;
- construct focused DataFrames by selecting relevant features;
- summarize the relationship between categorical features and a numerical variable; and
- communicate a data comparison using clear and correctly labeled plots.

To view the code itself, access the [related Python notebook file](ECE2112-PA4.ipynb). The requisite `board2.xlsx` file to be used alongside the code is not included.

To perform all the required tasks, the file `board2.xlsx` is imported as a DataFrame by the line `board = pd.read_excel('board2.xlsx')`; notably, as it is an `.xlsx` file, it uses a different function. Additionally, as the column `Average`, which is required for all three tasks, is missing, it is inserted with the line `board['Average']=(board['Math'] + board['Electronics'] + board['GEAS'] + board['Communication'])/4`, generating the column `Average` based on the values of the `Math`, `Electronics`, `GEAS`, and `Communication` columns. This new column is then attached to the rightmost end of the DataFrame.

Similarly to Programming Assignment 3, the `display()` function is preferred for displaying DataFrames over `print()` for the richer formatting.

# A. Visayas Communication Dataframe
>_Objective_: Create a DataFrame named `VisComm` containing students whose `Hometown` is `Visayas` and whose `Track` is `Communication`. Retain only these columns, in the stated order: `Name, Gender, Math, Electronics, Average`. Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to the source dataset before the columns are selected.

To generate the requested DataFrame, the `.loc` method is used, where the rows are identified by the Boolean condition `&` where both the row's `Hometown` and `Track` must be Visayas and Communication, respectively. The range of columns included are those required by the instructions, namely `Name`, `Gender`, `Math`, `Electronics`, and `Average`.

The DataFrame is then displayed by `display(VisComm)`, and line `print(len(VisComm))` prints the amount of rows of the new DataFrame `VisComm`. Here, the function `len()` returns the amount of items in an object; for a DataFrame, this is the amount of rows or entries present.

The constructed solution, omitting importing additional libraries and the `board2.xlsx` file, is:
```py
VisComm = board.loc[(board['Hometown']=='Visayas')&(board['Track']=='Communication'), ['Name', 'Gender', 'Math', 'Electronics','Average']]

display(VisComm)
print(len(VisComm))
```

# B. Visayas Female Dataframe
>_Objective_: Create a second DataFrame named `VisFemale` containing students whose `Hometown` is `Visayas` and whose `Gender` is `Female`. Retain only: `Name, Track, GEAS, Electronics, Average`. Display `VisFemale`. Then display only the rows of `VisFemale` whose `Average` is at least 60. Do not overwrite `VisFemale` when performing this second filter.

To construct the requested DataFrame, similar to problem A, the `.loc` method is used, instead requiring that the row's `Hometown` and `Gender` are Visayas and Female, respectively. The columns requested to be retained are also identified in the second argument, these being `Name`, `Track`, `GEAS`, `Electronics`, and `Average`.

The DataFrame is then displayed by `display(VisFemale)`. The line `display(VisFemale.loc[VisFemale['Average']>=60]` then fulfills the second display request of the problem, where the `.loc` method uses the Boolean operator `>=` to identify all rows of `VisFemale` where the recorded `Average` is greater than or equal to 60, without constructing additional DataFrames or altering the source. 

The constructed solution, omitting importing additional libraries and the `board2.xlsx` file, is:
```py
VisFemale = board.loc[(board['Hometown']=='Visayas')&(board['Gender']=='Female'), ['Name', 'Track', 'GEAS', 'Electronics', 'Average']]

display(VisFemale)
display(VisFemale.loc[VisFemale['Average']>=60])
```

# C. Category-Average Visualization
>_Objective_: Examine how the recorded `Average` differs across the three categorical features `Track`, `Gender`, and `Hometown`.
> - For each feature, compute the mean of `Average` for every category using Pandas.
> - Display the three summary tables.
> - Create one figure containing three bar charts: mean `Average` by `Track`, by `Gender`, and by `Hometown`.
> - Below the figure, write three concise statements identifying the category with the highest sample mean for each feature.

For each requested category, the mean average of the features is computed by using the `.pivot_table()` method, which groups data according to a certain `index`, and processes some related data `values` using a certain function `aggfunc`: if `aggfunc` is not specified, it defaults to taking the mean of all values. Also, multiple values can be given for `index`, in which case the pivot table will use all possible combinations of `index` values to summarize data. To ease the processing of the pivot tables, the method `.reset.index()` is stacked, which properly assigns each group of data its own index, allowing the data to more easily be called later on.

For instance, the line `mtrack = board.pivot_table(index='Track', values='Average').reset_index()` provides the arguments `(index='Track', values='Average')`: this groups the data in the `Average` column by the respective `Track` it belongs to. However, since there is no `aggfunc` specified, the pivot table defaults to taking the mean of all `Average` values. `.reset_index()` is then stacked to assign an index of 0 to 2 to each row, corresponding to the three total listed `Track` values. This process is repeated to group data based on `Gender` and `Hometown`, with all three DataFrames being stored in `mtrack`, `mgender`, and `mregion`.

Matplotlib is then used to construct the requested graphs, by `graph, axes = plt.subplots(nrows=1, ncols=3, figsize=(16,4))`. The `.subplots()` function returns two elements: the figure, here the first variable `graph`, and the subplot, here the second variable `axes`; the figure serves as the overall container for the subplot, which works as an array of objects that each draw a graph in a dedicated area within the plot. The amount of subplots corresponds to the provided `nrows` and `ncols` arguments, which specify the number of rows and columns to divide the figure into. Additionally, a `figsize` argument can be passed to the figure to dictate the exact dimensions of the figure. These arguments can be omitted, and the method will simply default to generating one row and one column. Here, the arguments `nrows=1, ncols=3, figsize=(16,4)` is used, specifying that there should be three adjacent areas for subplots, using the `figsize` of 16 by 4.

The subplots can then be modified by invoking them by their index, similar to invoking data from a Numpy array or Pandas DataFrame. As the plot only has one row and three columns, each subplot will be invoked by their column index, starting from `0` to `2`. For each subplot, two lines of code are used. The first line, `axes[0].bar(mtrack['Track'], mtrack['Average'])`, uses the `.bar()` method to construct a bar graph within the first subplot, `axes[0]`. Two arguments must be supplied; the first, here `mtrack['Track']`, identifies the values for the x-axis of the bar graph, and the second, here `mtrack['Average']`, identifies the corresponding value for the y-axis. The second line of code, `axes[0].set(title='Mean Average by Track', xlabel='Track', ylabel='Mean Average')`, uses the `.set()` method to supply additional labels to the graph within the subplot. A title, x-axis label, and y-axis label, are all set by providing the arguments `title`, `xlabel`, and `ylabel`, respectively. 

Finally, text is inserted into the figure by using the `.text()` method on the figure `graph`. The first three necessary arguments specify the position of the text along the x- and y-axes of the figure, and then the text iself. Notably, if the provided position exceeds the size of the figure, the figure will be extended to contain it. Additional arguments may be supplied to specify the weight, style, or size of the text, through `weight`, `style`, and `size`, respectively. Two lines of text are introduced by the code: one at coordinates `0.125, -0.1`, serving as a larger, bold label for the interpretation of the graphs. The next line introduces the actual interpretations at coordinates `0.125, -0.25`, simply stating which category holds the highest mean average for each feature. Finally, the entire completed figure is displayed by using the `.show()` function.

The constructed solution is:
```py
mtrack = board.pivot_table(index='Track', values='Average').reset_index()
mgender = board.pivot_table(index='Gender', values='Average').reset_index()
mregion = board.pivot_table(index='Hometown', values='Average').reset_index()

display(mtrack)
display(mgender)
display(mregion)

graph, axes = plt.subplots(nrows=1, ncols=3, figsize=(16,4))

axes[0].bar(mtrack['Track'], mtrack['Average'])
axes[0].set(title='Mean Average by Track', xlabel='Track', ylabel='Mean Average')

axes[1].bar(mgender['Gender'], mgender['Average'])
axes[1].set(title='Mean Average by Gender', xlabel='Gender', ylabel='Mean Average')

axes[2].bar(mregion['Hometown'], mregion['Average'])
axes[2].set(title='Mean Average by Region', xlabel='Region', ylabel='Mean Average')

graph.text(0.125, -0.1, 'Interpretation:', weight='bold', size=14)
graph.text(0.125, -0.25, 'By track, Communication holds the highest mean average (67.975).\n'
           'By gender, Male holds the highest mean average (67.183).\n'
           'By home region, Luzon holds the highest mean average (68.083).')

plt.show()
```

## History
- 2026, September 10: File created.
- 2026, September 11: Uploaded Jupyter notebook; solutions introduced.
- 2026, September 12: Introduced explanations for solutions to problems A and B.
- 2026, September 13: Introduced explanation for solution to problem C.
