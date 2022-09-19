### Merging Dataframes Vertically (Appending Data from one table to another)

#### Basic concatenation
- ```pd.concat(df_1,df_2,df_3) ``` results in a new dataframe which contains data from dataframes df_1, df_2, df_3 stacked vertically in that order
- all the dataframes used in the concat function above are assumed to have same column names and same number of columns
- To the ```pd.concat()``` function call, we can pass the value of 0 to the axis parameter but the default value of axis is 0 so its optional if we want vertical concatenation of dataframes
- For example - ```pd.concat(df_1,df_2,df_3, axis=0)``` is same as ```pd.concat(df_1,df_2,df_3) ```
 
 #### Ignoring indices of dataframes while merging
 - By default the merged data will preserve their indices (the index in the original dataframes)
 - If the indices for dataframes being merged do not carry any special meanings, they can be ignored by setting ```ignore_index = false``` like this ```pd.concat(df_1,df_2, ignore_index=True)```

 #### Setting keys to rows from different dataframes in the merged dataframe
 - passing a list of string to the ```concat()``` method assigns keys to set of rows belonging to specific tables
 - Example - ```pd.concat(df_1,df_2,df_3, ignore_index=False, keys=["df1","df2","df3"])```
 - Doing this results in a multi-index table with the labels as the first level index
 - **NOTE:** The ```ignore_index``` argument has to be ```False``` when you want to assign key labels to the rows of data from different tables. You **CANNOT** set ```ignore_index``` to ```True``` and assign keys to the data rows at the same time.

#### Merging tables with different number of columns
- The merged dataframe will contain all the columns from all the individual tables merged
- For a tables missing a certain column, the values will appear as NaN for missing columns
- If we only want the matching columns in the resulting dataframe, set the join argument to ```inner``` and only the columns common in all the dataframes will appear in the merged data
***Example -*** ```pd.concat(df_1,df_2,df_3, ignore_index=True, join=inner)```

#### Using ```.append()``` method
- Its a simplified version of concat method
- Supports ```ignore_index``` and ```sort``` arguments
- Does not support ```keys``` and ```join``` arguments

#### Validating merge using ```validate``` argument and ```verify_integrity``` arguments
- ```.merge()``` - uses ```validate``` argument
- ```.concat()``` - uses ```verify_integrity```
- The validate argument can have one of the following values:
    -```one_to_one```
    -```one_to_many```
    -```many_to_one```
    -```many_to_many```
- If the expected validation criteria is not met, pandas will throw error. We should fix that error before proceeding with the merge
- Example - ```df1.merge(df2,on="joining_col_name", validate="one_to_one")```

