# **ECE-2112-PA-3**
**Dean Matthew M. Calibut | 2ECE-D**

This repository details the implementation of Experiment 3 (PA3), focusing on data manipulation, positional and label-based slicing, and dynamic Boolean indexing using the Pandas library. The code fulfills the intended learning outcomes of loading tabular CSV datasets and extracting specific DataFrame subsets without modifying original source values.

# **Initial Setup & Library Imports**
Before tackling the specific problems, the necessary Python libraries must be imported to establish the working environment.

## **The Following Modules were imported:**

```python
import pandas as pd
```
* `import pandas as pd`: This is the foundational library required for data manipulation and tabular data analysis in this experiment. Importing it under the standard alias pd allows for concise calls to read CSV files and utilize structure-handling tools like DataFrame, .iloc, and .loc.

```python
new_cars = pd.read_csv('cars.csv')
```
* `pd.read_csv('cars.csv')`: Loads the automotive specification CSV file into a 2D tabular Pandas DataFrame named new_cars.

# **1. Positional and Label-Based Slicing**
#### **Objective:** This problem requires displaying the shape and complete list of column names of the cars DataFrame, using positional indexing (iloc) to extract rows 6 through 10 into cars_6_to_10 where the first data row is treated as row 1, and then using column labels to display only the Model, mpg, cyl, hp, and gear columns from cars_6_to_10 in that exact order.

The Following Methods/Functions were used:

```python
# Part A: Display dataset dimensions and column headers
print("Shape of cars DataFrame:", cars.shape)
print("Column Names:", cars.columns.tolist())
```
The .shape attribute displays the overall dimensions (32 rows by 12 columns), and .columns.tolist() returns a complete list of all column attribute names present in the dataset.

```python
# Part B: Positional slicing using .iloc
cars_6_to_10 = cars.iloc[5:10]
```
The .iloc[5:10] positional indexer applies zero-based slicing ([start:stop]). Treating row 1 as index position 0, rows 6 through 10 correspond to zero-based index positions 5, 6, 7, 8, and 9.

```python
# Part C: Label-based column selection
cars_6_to_10_selected = cars_6_to_10.loc[:, ['Model', 'mpg', 'cyl', 'hp', 'gear']]
display(cars_6_to_10_selected)
```
The .loc[:, ['Model', 'mpg', 'cyl', 'hp', 'gear']] selector isolates the exact required columns by label in the specified order without relying on numerical column indices.

# **2. Model Lookup**
#### **Objective:** This problem requires using Boolean indexing on the Model column to dynamically locate and store the complete row record for "Toyota Corolla" into toyota, while extracting only the Model, mpg, hp, and wt columns for "Pontiac Firebird" into pontiac without relying on any hardcoded row numbers.

The Following Methods/Functions were used:

```python
# Part A: Complete record query for Toyota Corolla
toyota = cars.loc[cars['Model'] == 'Toyota Corolla']
display(toyota)
```
The evaluation cars['Model'] == 'Toyota Corolla' generates a dynamic Boolean mask array. Passing this mask to .loc[] isolates the matching vehicle record across all dataset columns.

```python
# Part B: Selective attribute query for Pontiac Firebird
pontiac = cars.loc[cars['Model'] == 'Pontiac Firebird', ['Model', 'mpg', 'hp', 'wt']]
display(pontiac)
```
For the Pontiac Firebird query, .loc[mask, column_list] combines dynamic Boolean row matching with precise column label selection in a single operation.

# **3. Multi-Model Subsetting**
#### **Objective:** Create a 6x6 array containing the squares of the first 36 positive integers and isolate elements strictly greater than the array's overall mean.

The Following Methods/Functions were used:

```python
target_models = ['Datsun 710', 'Lotus Europa', 'Ferrari Dino']
target_cols = ['Model', 'mpg', 'cyl', 'hp', 'gear']

# Filter by model values and retain target columns
selected_cars = cars.loc[cars['Model'].isin(target_models), target_cols]

display(selected_cars)
print("Shape of selected_cars:", selected_cars.shape)
```
To extract these specific records without hardcoding row indices or writing out long, repetitive OR conditions (such as (cars['Model'] == 'Datsun 710') | (cars['Model'] == 'Lotus Europa')), the .isin() method is utilized. This function vectorizes the conditional check, generating a single Boolean mask array that flags True for any row where the Model matches a value inside the target_models list.

By passing both this Boolean mask and the target_cols list directly into the .loc[row_indexer, column_indexer] accessor, Pandas executes a highly efficient two-dimensional slice. It dynamically filters the rows based on the True condition matches and simultaneously subsets the dataset down to the five requested column labels. This approach ensures the original index ordering is preserved while discarding unwanted data.

Finally, evaluating the .shape attribute acts as a structural validation check, confirming that the resulting matrix has successfully been filtered down to exactly 3 rows and 5 columns (3, 5) as mandated by the problem requirements.

To see the main Python program for Experiment 3, click this link https://github.com/Matt-Mallari/ECE-2112-PA-2/blob/main/ECE2112_PA2.ipynb, download the .ipynb file, open it in Jupyter Notebook, and run all cells.

Moreover, the `.npy` file for each respective array can be viewed here https://github.com/Matt-Mallari/ECE-2112-PA-2/tree/main/NumPy%20Files.
Furthermore, 

### **README File Version History**
* 2026, September 10: Repository Created
