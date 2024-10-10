# Merging Extra Practice

For these questions, you'll be using data from the Austin Animal Center, containing information on animal intakes and animal outcomes. The original sources of this data are [here](https://data.austintexas.gov/Health-and-Community-Services/Austin-Animal-Center-Intakes/wter-evkm) and [here](https://data.austintexas.gov/Health-and-Community-Services/Austin-Animal-Center-Outcomes/9t4d-g238/about_data).

Read the provided csv files into DataFrames named "intakes" and "outcomes".

0. Is the relationship between the intakes and outcomes tables one-to-one, many-to-one, one-to-many, or many-to-many?
1. The key identifier variable for this data is the Animal ID. Perform a merge to determine if there are any animal ids from the intakes data that do not appear in the outcomes data and vice versa. Think carefully about which column or columns you'd like to merge on.
2. Sometimes, the column you want to merge on is the index of the DataFrame. For this problem, let's try merging on the index. Set the index of the intakes and outcomes dataframes to "Animal ID" (using the [set_index method](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.set_index.html) and then merge the two. Afterwards, you may want to set the index back to how it originally was (using the [reset_index method](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.reset_index.html)).
3. Merge the intakes and outcomes dataframe on just the Animal ID column. Notice that any other columns that are in common get a _x and _y suffix. Use the suffixes parameter to change this to _intake and _outcome. Are there are animal ids which have different Name values in the intake and outcomes DataFrames?
4. Merging just on Animal ID doesn't necessarily match a given intake to its corresponding outcome. However, we can change the way that we merge to try to match these up correctly.
    a. We'll need to make use of the DateTime columns in order to make this merge work. Convert these columns to the datetime type.
    b. Now, use the [merge_asof function](https://pandas.pydata.org/docs/reference/api/pandas.merge_asof.html) in order to match intake rows to their corresponding outcome rows. That is, each intake row should be matched with the outcome that is nearest to it in the future (still matched by Animal ID).
    c. Are there any instance of an intake that doesn't have an outcome before the next intake? Keep only the last intake row for those cases.
    d. Create a new column showing the time between intake and outcome. What does the distribution of these values look like? Does it vary by animal type?
    e. Find all rows where the animal is intact at intake and spayed or neutered at outcome. What percentage of intact intakes result in a spay or neuter?