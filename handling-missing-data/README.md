<h1>
  <span class="headline">Cleaning and Combining Data With Pandas</span>
  <span class="subhead">Handling Missing Data</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to identify and handle missing data in a dataset using various strategies.

| Lesson                | Duration |
| --------------------- | -------- |
| Handling Missing Data | 30 min   |

## NULLs

A **NULL** value is _any missing value_ in your data. One common way of conceptualizing a NULL value is thinking of it as **"empty"** — not zero `0`, not the word `"NULL"`, but simply _empty_.

> 💡 A **NULL** value is a common data issue.

<img src="./assets/magnifying-glass.png" alt="Magnifying Glass Image" style="width: 300px; height: auto;">

## Identifying Missing Data

The first step when dealing with NULLs is to identify whether or not we’re missing data at all. We have a few ways to explore missing data, reminiscent of Boolean filters:

`isnull()` converts values into `True` if NULL, `False` otherwise

```python
data_frame.isnull()
```

We can then use `.sum()` to count up the number of NULL values

```python
data_frame.isnull().sum()
```

## Understanding Missing Data

Finding missing data is the easy part! Determining what to do next is more complicated.

Typically, we’re most interested in knowing **_why_** we are missing data. Once we know the **"type of missingness"** (i.e., the source or cause of missing data), we can proceed effectively. This is essential to deciding whether to delete incomplete values or fill them in and, if so, with what.

## Four Primary Strategies for Handling NULLs

| **Strategy**                           | **Description**                                                                    | **Notes**                                                                                                         |
| -------------------------------------- | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Using external references**          | Find the true value of the missing data and fill it in.                            |                                                                                                                   |
| **Make educated guesses**              | Impute (i.e., fill in) missing values with the mean, median, or some other number. | The most common solution when the missing data is minimal and the dataset is large                                |
| **Ignore them**                        | Choose to leave the NULL values as they are without making any changes.            | **Proceed with caution!** These strategies can rely on dangerous assumptions and are usually not good approaches. |
| **Delete rows containing NULL values** | Remove any rows from the dataset that contain NULL values.                         | **Proceed with caution!** These strategies can rely on dangerous assumptions and are usually not good approaches. |

## Options for Missing Values

| **Option**                        | **Rationale**                                                                                           | **Example**                                                                                               |
| --------------------------------- | ------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Remove them**                   | For some analyses, rows without a specific column are entirely useless.                                 | `df["column"].dropna(inplace=False)` <br> `df.dropna(subset=["column_a", "column_b"])`                    |
| **Fill with arbitrary value**     | Useful if you want to keep incomplete records but still mark them with a specific value.                | `df["column"].fillna("Unknown")` <br> `df.fillna({"column_a":0, "column_b":100}) `                        |
| **Fill with computed value**      | For some statistical analysis, it may make sense to fill in the mean or median of the complete records. | `df["column"].fillna(df["column"].mean())`                                                                |
| **Replace specific values**       | You can replace a value or regex pattern with something else, which can help standardize data sets      | `df.replace("Illinois", "IL")` <br> `# replaces all appearances of "Illinois" with the abbreviation "IL"` |
| **Fill with interpolated values** | Pandas will automatically calculate missing values based on linear calculations                         | `# given [0,1,NA,3] as a series...` <br> `df['sales_total'].interpolate()` <br> `# results in [0,1,2,3] ` |

> 💡 Note that the examples provide both Series and DataFrame usages of these methods.

<br>

<div class="activity guided-walkthrough">
  <h2 class="title">3.1 Identifying Missing Data</h2>
  <span class="minutes">20 min</span>
</div>

Let's use the "Orders" table from Superstore to work with missing data in **Section 3.1** of the workbook.

<img src="./assets/shopping-cart.png" alt="Shopping Cart Image" style="width: 300px; height: auto;">
