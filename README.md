# Case-Studies
Supermarket Sales - Data Cleaning Project

This repository contains a data-cleaning workflow performed on the file supermarket_sales_new.csv using Python and pandas.
The goal of this project is to ensure the dataset is accurate, consistent, and ready for further exploratory analysis or modeling.

1. Project Overview

The dataset includes transactional records from a supermarket: gender, branch, customer type, unit price, quantity, tax, and more.

This project focuses on:

Inspecting data quality
Detecting structural issues
Correcting inaccurate fields
Reconstructing the Total column
Exporting a fully cleaned dataset


2. Cleaning Steps Performed
   
2.1 Load the dataset

The file was imported using:

df = pd.read_csv("supermarket_sales_new.csv")

2.2 Inspect the structure

Checked:

Data types

Null values

Duplicate rows


Using:

df.head()
df.info()
df.isna().sum()
df.duplicated().sum()

Findings:

No missing values

No duplicate rows

Data types correct (object, int, float)

2.3 Recalculate Sales Tax

The dataset contains a field Tax 5%, but an additional check was performed to validate tax consistency.

df["expected_tax"] = df["Unit price"] * df["Quantity"] * 0.05
df[["Tax 5%", "expected_tax"]].head()

This comparison ensures the tax values follow the correct formula.
The temporary expected_tax column was dropped afterward:

df = df.drop(columns=["expected_tax"])

2.4 Recalculate Total

The Total value was rebuilt from scratch to guarantee numeric accuracy:

df["Total"] = df["Unit price"] * df["Quantity"] + df["Tax 5%"]


2.5 Export the Cleaned Dataset

The final cleaned file was saved as:

df.to_csv("supermarket_sales_cleaned.csv", index=False)


3. Files in This Repository

supermarket_sales_new.csv         # Original dataset
supermarket_sales_cleaned.csv     # Cleaned and corrected dataset
supermarket_sales_cleaning.ipynb  # Google Colab notebook containing all code
README.md                         # Project documentation


4. Tools Used

Python 3.10+

pandas for data manipulation

Google Colab for notebook execution



5. Purpose of This Project

This project demonstrates fundamental data-cleaning skills expected from a junior data analyst:

Validating raw data

Repairing inaccurate fields

Ensuring consistent calculations

Producing clean, ready-to-use datasets

Documenting the process clearly
