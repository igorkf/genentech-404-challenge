## Genentech 404 Challenge (Kaggle) - 7th place entry

My solution is pretty simple:
1. put the data in the `data` folder
2. run `solution.ipynb`

The data for the competition can be found [here](https://www.kaggle.com/competitions/genentech-404-challenge/data).

### Method

This is a longitudinal data where each patient is observed for some (variable) time.

The idea is simple:
1. Sort the data for each patient in ascending mode (lowest months first)
2. For each variable impute data using (in this order):
   1. linear interpolation
   2. forward fill
   3. backward fill

3. For the remaining data* (where there are still NA), apply:
   1. Apply standardization 
   2.  [iterative imputation](https://scikit-learn.org/stable/modules/generated/sklearn.impute.IterativeImputer.html#sklearn.impute.IterativeImputer) with Huber regressor
   3. Inverse transform to get predictions ins original scale

4. Apply roundings and clipping

***

\* There will be still NA after imputation because some patient has either all NA in a specific variable or only one row.