# McDonald's Nutritional Value Analysis

This project analyzes the nutritional data of McDonald's menu items to uncover interesting insights and answer specific questions about the caloric content and nutritional comparisons. The goal is to provide a data-driven understanding of McDonald's menu offerings.

**Dataset:** The analysis uses a dataset containing nutritional information for various McDonald's menu items, including categories like Breakfast, Beef & Pork, Chicken & Fish, Salads, Snacks & Sides, Drinks, and Coffee & Tea.

## Table of Contents

- [Project Goal & Questions](#project-goal--questions)
- [Methodology](#methodology)
- [Analysis & Findings](#analysis--findings)
    - [Question 1: Average Calories for a McDonald's Value Meal](#question-1-average-calories-for-a-mcdonalds-value-meal)
    - [Question 2: Beverage Contribution to Overall Caloric Intake](#question-2-beverage-contribution-to-overall-caloric-intake)
    - [Question 3: Grilled vs. Crispy Chicken Nutritional Comparison](#question-3-grilled-vs-crispy-chicken-nutritional-comparison)
    - [Question 4: Whole Egg vs. Egg White Nutritional Comparison](#question-4-whole-egg-vs-egg-white-nutritional-comparison)
    - [Question 5: Least Number of Items for Nutritional Requirements](#question-5-least-number-of-items-for-nutritional-requirements)
- [Technologies Used](#technologies-used)
- [How to Run the Analysis (Optional)](#how-to-run-the-analysis-optional)
- [Conclusion](#conclusion)
- [Author](#author)
- [License](#license)


## Project Goal & Questions

The primary goal of this analysis is to explore the nutritional data of McDonald's menu items to answer the following key questions:

1.  What is the approximate caloric content of a typical McDonald's "value meal"?
2.  How much do beverages (like soda or coffee) contribute to the overall caloric intake of a value meal?
3.  Does ordering grilled chicken instead of crispy chicken increase a menu item's nutritional value (e.g., lower calories, fat, sodium, higher protein)?
4.  What are the nutritional differences between menu items offering whole egg versus egg white options?
5.  What is the least number of items could you order from the menu to meet one day's nutritional requirements?


## Methodology

1.  **Data Loading & Inspection:** The `Mc_Donald_Nutritional_Value_Data.csv` dataset was loaded using pandas. Initial steps involved inspecting the data for structure, missing values, and data types.
2.  **Data Cleaning & Preparation:** No significant cleaning was required beyond ensuring consistent string handling for item names.
3.  **Feature Engineering (Base Names):** Custom functions were created to extract 'base names' for menu items (e.g., 'Chicken Classic' from 'Premium Grilled Chicken Classic') to enable direct comparison between different versions of the same item.
4.  **Nutritional Analysis:** Python's pandas library was used to filter, group, and aggregate data to answer each specific question.
5.  **Insights Generation:** Key findings and observations were extracted from the statistical analysis.


### Question 1: Average Calories for a McDonald's Value Meal
Definition of a "Value Meal": For this analysis, a "value meal" is defined as a combination of:

- A main item (average of 'Beef & Pork' and 'Chicken & Fish' categories).
- A side (average calories of 'Fries').
- A drink (average of 'Drinks' and 'Coffee & Tea' categories).

### Findings:
A typical McDonald's value meal, as defined above, contains approximately **1113.30 calories.**

### Code Used:
```import pandas as pd

# Load the dataset
df = pd.read_csv('Mc_Donald_Nutritional_Value_Data.csv')

# Calculate average calories for main items (Beef & Pork, Chicken & Fish)
main_items_calories = df[df['Category'].isin(['Beef & Pork', 'Chicken & Fish'])]['Calories']
average_main_item_calories = main_items_calories.mean()

# Calculate average calories for fries (specific item within Snacks & Sides)
fries_items = df[df['Category'] == 'Snacks & Sides']['Item'].str.contains('Fries', case=False)
average_fries_calories = df[df['Category'] == 'Snacks & Sides'][fries_items]['Calories'].mean()

# Calculate average calories for beverages (Drinks, Coffee & Tea)
beverage_calories = df[df['Category'].isin(['Drinks', 'Coffee & Tea'])]['Calories']
average_beverage_calories = beverage_calories.mean()

# Calculate total average value meal calories
average_value_meal_calories = average_main_item_calories + average_fries_calories + average_beverage_calories

print(f"Average Calories for Main Item: {average_main_item_calories:.2f}")
print(f"Average Calories for Fries: {average_fries_calories:.2f}")
print(f"Average Calories for Drinks: {average_beverage_calories:.2f}")
print(f"The average McDonald's value meal contains approximately {average_value_meal_calories:.2f} calories.")```
