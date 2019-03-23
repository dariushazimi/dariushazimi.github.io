---
layout: post
title: Data cleansing steps
# subtitle: How to get the elements from a list using Map
tags: [isnull, dropna, fillna,pandas]
---

# Data cleansing steps

## Remove unnecessary columns
Pandas offers two functions for handeling missing data:
` isnull()` and `notnull`.
These return a Boolean value to show if the passed value is missing data.

You can either replace them or drop them. 

In pandas missing values show up as `nan` values. (not a number).

`dropna()` drops all nan values from a dataframe
instead of drop all those values you can call `fillna()` to change the nan values with values you specifiy.
## Identify and remove duplicates
`duplicated()` functions finds duplicate values in a series.
`drop_duplicates()` removes the duplicates.
## Fix missing data 

If you need to alter the column used in an index, you can use `set_index()`.

`set_index()` allows you to change the column or columns you want to be the index column.




