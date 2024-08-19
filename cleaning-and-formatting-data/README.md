<h1>
  <span class="headline">Cleaning and Combining Data With Pandas</span>
  <span class="subhead">Cleaning and Formatting Data</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to clean and format data using Pandas, including reformatting dates, extracting specific time properties, removing duplicates, applying custom functions, and handling timestamps effectively

| Lesson                       | Duration |
| ---------------------------- | -------- |
| Cleaning and Formatting Data | 25 min   |

## Data Cleaning

Data cleaning is the process of assembling data into a **usable format for analysis**.

Common data cleaning actions include:

- **Reformatting dates** so that Python recognizes them.

- **Extracting day/hour/month/year from a date** to aggregate by those categories.

- **Removing duplicate values** or rows.

- **Combining data sources** into one table.

- **Concatenating or separating** data.

![Image Placeholder](TKTK)

> 💡 The data sets that we receive as analysts are often very messy, but there’s no need to be fazed by them. While we can’t possibly cover every single cleaning function in this course, there are tons of resources out there about cleaning functions.

## Modifying Series Within DataFrames

Many of our cleaning operations involve applying an operation to a Series:

```python
data_frame['column_a'] = data_frame['column_a'].to_numeric()
```

This can also be used to create new columns based on existing data:

```python
data_frame['Fahrenheit'] = data_frame['Celsius'] * (9/5) + 32
```

## Handling Dates and Times

Some of the most challenging, frequently ill-formatted types of data are dates and times.

Fortunately, Pandas is on top of it with the `.to_datetime()` method:

```python
df['Column'].to_datetime(inplace=True)
```

Once a Series has been given a datetime data type, we can use access methods to extract specific time properties, like day or hour.

We can also use the Pandas `Timestamp()` method to convert data into timestamps:

```python
pd.Timestamp(date_string_or_number)
```

## Anatomy of a TimeStamp

A **TimeStamp** in Pandas is an object that represents a specific moment in time. It is very similar to Python's datetime objects but comes with additional capabilities tailored for data analysis.

```python
moment_in_time = pd.Timestamp("19890602T07:43:55")
```

In this example, `moment_in_time` is a Timestamp object representing **June 2, 1989, at 7:43:55 AM**.

Pandas makes it easy to extract specific parts of the timestamp:

```python
moment_in_time.year
# 1989
moment_in_time.month
# 6
moment_in_time.day
# 2
moment_in_time.hour
# 7
moment_in_time.minute
# 43
moment_in_time.second
# 55
```

> 💡 Pandas also offers a range of methods for converting and formatting timestamps, which can be especially useful when dealing with diverse datasets from different sources.

## apply()

There is also the `apply()` method, which allows us to use any function or method:

```python
def strip_dollar_sign(str):
    return str.replace("$", "")

df['column_a'] = df['column_a'].apply(strip_dollar_sign)
```

If you need to apply a function to each row by row, set `axis=1` as an argument.

> Note the row-by-row argument, as it will be relevant to solving an upcoming workbook challenge.

## Addressing Duplicates

Fortunately, the issue of duplicate data is a mere Pandas method away from being solved!

We can use the `.drop_duplicates()` method:

```python
df.drop_duplicates()
```

If we want to drop duplicates based on certain columns, we can do that, too:

```python
df.drop_duplicates(subset=['column_a', 'column_b'])
```

> Thinking about which combination of columns constitutes a removable duplicate is a problem worth addressing during exploratory data analysis.Some combination of columns will inevitably be duplicates, so determine which exact combinations should never be shared between different rows.

<br>

<div class="activity partner-exercise">
  <h2 class="title">3.2 Cleaning and Formatting Data</h2>
  <span class="minutes">15 min</span>
</div>

Let's use the Superstore data set for **Section 3.2** to practice applying cleaning functions.

![Image Placeholder](TKTK)
