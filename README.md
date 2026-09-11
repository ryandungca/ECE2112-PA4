# ECE2112: Programming Assignment 4
**Ryan Joseph C. Dungca, 2ECE-D**

This repository contains code for Programming Assignment 4 of the course ECE2112, covering three problems related to _Module 4: Data Wrangling and Visualization_. The creation of this code demonstrates the ability to:
- filter tabular data using several categorical and numerical conditions;
- construct focused DataFrames by selecting relevant features;
- summarize the relationship between categorical features and a numerical variable; and
- communicate a data comparison using clear and correctly labeled plots.

To view the code itself, access the [related Python notebook file](ECE2112-PA4.ipynb). The requisite `board2.xlsx` file to be used alongside the code is not included.

# A. Visayas Communication Dataframe
>_Objective_: Create a DataFrame named `VisComm` containing students whose `Hometown` is `Visayas` and whose `Track` is `Communication`. Retain only these columns, in the stated order: `Name, Gender, Math, Electronics, Average`. Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to the source dataset before the columns are selected.

The constructed solution is:
```py
VisComm = board.loc[(board['Hometown']=='Visayas')&(board['Track']=='Communication'), ['Name', 'Gender', 'Math', 'Electronics','Average']]

display(VisComm)
print(len(VisComm))
```

# B. Visayas Female Dataframe
>_Objective_: Create a second DataFrame named `VisFemale` containing students whose `Hometown` is `Visayas` and whose `Gender` is `Female`. Retain only: `Name, Track, GEAS, Electronics, Average`. Display `VisFemale`. Then display only the rows of `VisFemale` whose `Average` is at least 60. Do not overwrite `VisFemale` when performing this second filter.

The constructed solution is:
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

The constructed solution is:
```py
mtrack = board.pivot_table(index='Track', values='Average').reset_index()
mgender = board.pivot_table(index='Gender', values='Average').reset_index()
mregion = board.pivot_table(index='Hometown', values='Average').reset_index()

display(mtrack)
display(mgender)
display(mregion)

graph, axes = plt.subplots(nrows=1, ncols=3, figsize=(16,4)) # works like a numpy matrix, for graphs

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
