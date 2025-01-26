# Personal Fitness Tracker

## Overview

The Personal Fitness Tracker is a Python-based application designed to help users track their physical activities and monitor their fitness goals. The application allows users to log activities, analyze their weekly progress, and check if they are meeting their fitness objectives.

## Features

1. **Activity Tracking**: Users can add custom physical activities, including the date, activity name, duration (in minutes), and calories burned.

2. **Weekly Summary**: Generates a summary of activities on a weekly basis to help users visualize their fitness achievements.

3. **Progress Monitoring**: Users can set weekly goals for minutes spent exercising and calories burned, and the application will compare actual data against these goals.

4. **Goal Setting**: Provides feedback on whether users have met their weekly and daily fitness goals based on their activity data.

## Requirements

- Python 3.x
- Pandas library for data manipulation
- Numpy library
- Google Colab for environment setup (optional, but currently used)

## Installation

1. Make sure you have Python installed on your system along with Pandas and Numpy. If you need to install Pandas and Numpy, you can do so via pip:

   ```bash
   pip install pandas numpy
   ```

2. If using Google Colab, simply open a new notebook.

## Usage

### Step 1: Import Libraries

Start by importing the required libraries and mounting Google Drive:

```python
import numpy as np
import pandas as pd
from google.colab import drive
drive.mount('/content/drive')
```

### Step 2: Load Data

Load the existing activity data from a CSV file:

```python
path = '/content/drive/MyDrive/pds-12/task1/2_Personal_Fitness_Tracker.csv'
data = pd.read_csv(path)
df = pd.DataFrame(data)
```

### Step 3: Add New Activity

You can add a new activity using the `addColumn` function:

```python
def addColumn(date, activity, duration, calories):
    """
    parameters:
    date: Date of the activity
    activity: Name of the activity
    duration: Duration in minutes
    calories: Calories burned
    """
    new_data = {"Date": date, "Activity Name": activity, "Duration (minutes)": duration, "Calories Burned": calories}
    data.append(new_data, ignore_index=True)
    df.to_csv('data.csv', index=False)
```

### Step 4: Weekly Summary

Get a summary of activities on a weekly basis:

```python
def weekly_summary(df):
    df["Date"] = pd.to_datetime(df["Date"])
    df["Week"] = df["Date"].dt.to_period("W")
    weekly_totals = df.groupby("Week")[["Duration (minutes)", "Calories Burned"]].sum().reset_index()
    return weekly_totals
```

### Step 5: Compare Goals

Define your weekly goals and check against actual activity levels:

```python
goal_minutes = int(input("Enter your weekly goal for minutes: "))
goal_calories = int(input("Enter your weekly goal for calories: "))
comparison = compare_goals(df, goal_minutes, goal_calories)
print(comparison)
```

### Step 6: Check Goals

Set daily and weekly goals and verify if they have been achieved:

```python
weekly_goal = int(input("Enter your weekly goal for minutes: "))
daily_goal = int(input("Enter your daily goal for calories: "))
check_goals(df, weekly_goal, daily_goal)
```

