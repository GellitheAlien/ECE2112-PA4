## ECE2112_PA4

Made by: Geri Allison Geneta | 2ECE-B

This repository contains our Programming Assignment 4 for ECE2112. This project covers three python problems referenced to Module 3 - Pandas and Module 4 - Data Wrangling and Visualization.

```python
import pandas as pd
```

The board2.csv file is read using pd.read_csv() and stored in the variable df. The DataFrame is then displayed so the complete student dataset can be viewed before performing the required operations.

```python
df = pd.read_csv('board2.csv')
df
```

## A. VISAYAS COMMUNICATION DATAFRAME

The following problem asks to filter the student data to find Communication students from Visayas, select the needed columns, calculate their average Math and Electronics scores, and count the number of students.

The following functions and methods were used in this problem:

* .loc[] - a Pandas indexing method used to filter rows and select specific columns from the DataFrame.

* & - a Boolean AND operator used to combine conditions. Both conditions must be true for a student to be included.

* .mean(axis = 1) - calculates the mean across the columns in each row.

* .shape[0] - gets the number of rows in the DataFrame, which represents the number of students.

These were combined to filter the Communication students from Visayas, select their Name, Gender, Math, and Electronics scores, and calculate their average:

```python
Adf = df.loc[(df['Track'] == 'Communication') & (df['Hometown'] == 'Visayas')]

```

```python
Viscomm = Adf.loc[:, ['Name', 'Gender', 'Math', 'Electronics']]

```

```python
Viscomm['Average'] = Viscomm[['Math', 'Electronics']].mean(axis = 1)
Viscomm

```

The number of students was then obtained using:

```python
Viscomm.shape[0]
```

## B. VISAYAS FEMALE DATAFRAME

The following problem asks to filter the student data to find female Communication students from Visayas, select the required columns, calculate their average GEAS and Electronics scores, and keep only students with an average of at least 60.

The following functions and methods were used in this problem:

* .loc[] - a Pandas indexing method used to filter rows and select specific columns.

* & - a Boolean AND operator used to combine the three conditions. All conditions must be true for a student to be included.

* .mean(axis = 1) - calculates the mean of the selected scores across each row.

* ">=" - a comparison operator used to check if the student's average is greater than or equal to 60.

These operations were applied to filter the female Communication students from Visayas and calculate their GEAS and Electronics average:

```python
Bdf = df.loc[(df['Track'] == 'Communication') & (df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')]
Bdf
```

```python
VisFemale = Bdf.loc[:, ['Name', 'Track', 'GEAS', 'Electronics']]
```

```python
VisFemale['Average'] = VisFemale[['GEAS', 'Electronics']].mean(axis = 1)
VisFemale
```

The students with an average of at least 60 were then filtered using:

```python
VisFemale.loc[(VisFemale['Average'] >= 60)]
```

## C. CATEGORY-AVERAGE VISUALIZATION

This problem asks to calculate the overall average of each student using their Math, Electronics, GEAS, and Communication scores, then group the results according to Track, Gender, and Hometown.

The following functions and methods were used in this problem:

* .mean(axis = 1) - calculates the average of the four subject scores for each student.

* .groupby() - groups the students according to a specific category such as Track, Gender, or Hometown.

* .mean() - calculates the mean overall average for each group.

* These were combined to calculate each student's overall average:

```python
df['Average'] = df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis = 1)

```

The average was then grouped by Track:

```python
trackdf = df.groupby('Track')['Average'].mean()
trackdf
```

The average was also grouped by Gender:

```python
genderdf = df.groupby('Gender')['Average'].mean()
genderdf
```

The average was then grouped by Hometown:

```python
hometowndf = df.groupby('Hometown')['Average'].mean()
hometowndf

```

* matplotlib.pyplot - a library used to create the bar graphs for the calculated sample means.

```python
import matplotlib.pyplot as plt
```

The three DataFrames were then plotted as bar graphs:

```python
fig, axes = plt.subplots(1, 3, figsize=(20, 5))

Trackdf.plot(kind='bar', ax=axes[0])
Genderdf.plot(kind='bar', ax=axes[1])
Hometowndf.plot(kind='bar', ax=axes[2])
```

The resulting figure contains three bar graphs showing the sample mean according to Track, Gender, and Hometown.

* The highest sample mean in the Track category is Communication
  
Based on the calculated sample means, the Communication track has a mean of 67.975, Instrumentation has 65.225, and Microelectronics has 67.500. The notebook therefore identifies Communication as having the highest sample mean in the Track category.

* The highest sample mean in the Gender category is Male

The calculated sample mean is 66.616667 for Female students and 67.183333 for Male students. The notebook therefore identifies Male as having the higher sample mean in the Gender category.

* The highest sample mean in the Hometown category is Luzon

The calculated sample mean is 68.083333 for Luzon, 66.678571 for Mindanao, and 65.750000 for Visayas. The notebook therefore identifies Luzon as having the highest sample mean in the Hometown category.

The dataset shows differences in average scores across Track, Gender, and Hometown groups. However, these differences describe only the observed data and do not establish that a student's Track, Gender, or Hometown causes a higher or lower board-exam score.

The End.

## Thank You for Reading!
