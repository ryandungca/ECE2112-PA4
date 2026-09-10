# ECE2112: Programming Assignment 4
**Ryan Joseph C. Dungca, 2ECE-D**

This repository contains code for Programming Assignment 4 of the course ECE2112, covering three problems related to _Module 4: Data Wrangling and Visualization_. The creation of this code demonstrates the ability to:
- filter tabular data using several categorical and numerical conditions;
- construct focused DataFrames by selecting relevant features;
- summarize the relationship between categorical features and a numerical variable; and
- communicate a data comparison using clear and correctly labeled plots.

To view the code itself, access the [related Python notebook file](), which is currently not available.

# A. Visayas Communication Dataframe
>_Objective_: Create a DataFrame named `VisComm` containing students whose `Hometown` is `Visayas` and whose `Track` is `Communication`. Retain only these columns, in the stated order: `Name, Gender, Math, Electronics, Average`. Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to the source dataset before the columns are selected.

The constructed solution is:
```
(PRB_SOL_1)
```

# B. Visayas Female Dataframe
>_Objective_: Create a second DataFrame named `VisFemale` containing students whose `Hometown` is `Visayas` and whose `Gender` is `Female`. Retain only: `Name, Track, GEAS, Electronics, Average`. Display `VisFemale`. Then display only the rows of `VisFemale` whose `Average` is at least 60. Do not overwrite `VisFemale` when performing this second filter.

The constructed solution is:
```
(PRB_SOL_2)
```

# C. Category-Average Visualization
>_Objective_: Examine how the recorded `Average` differs across the three categorical features `Track`, `Gender`, and `Hometown`.
> - For each feature, compute the mean of `Average` for every category using Pandas.
> - Display the three summary tables.
> - Create one figure containing three bar charts: mean `Average` by `Track`, by `Gender`, and by `Hometown`.
> - Below the figure, write three concise statements identifying the category with the highest sample mean for each feature.

The constructed solution is:
```
(PRB_SOL_3)
```

## History
- 2026, September 10: File created.
