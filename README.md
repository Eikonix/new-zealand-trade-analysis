# new-zealand-trade-analysis
Analysis of New Zealand's export and import trade data from 2022-2024
# New Zealand Trade Data Analysis (2022-2024)

## Overview
This project analyzes New Zealand's export and import trade statistics from 2022 to 2024. The primary goal is to identify key trade trends, major trading partners, and significant commodities to gain insights into New Zealand's trade structure.

## Dataset Used
*   **Data Source:** Stats NZ「Overseas merchandise trade datasets」
*   **Period Covered:** January 2022 - December 2024
*   **Contents:** Monthly data aggregated by HS code, country, including export/import values, etc.

## Technologies & Libraries Used
*   Python
*   Pandas (Data manipulation and analysis)
*   Matplotlib (Data visualization)
*   Seaborn (Data visualization)
*   Plotly (Interactive data visualization)
*   Kaggle Notebooks (Analysis environment)

## Analysis Steps

### Step 1: Data Loading and Preprocessing

#### 1.1 Data Loading
Individual CSV files for export and import data for each year (2022, 2023, and 2024) were loaded into Pandas DataFrames.
A 'year' column was added to each DataFrame, and then all yearly data were concatenated into two main DataFrames: `df_exports_all` for exports and `df_imports_all` for imports.

```python
# Example: Key part of data loading and concatenation (illustrative)
import pandas as pd

# Loading yearly data (example for exports)
# df_export_2022 = pd.read_csv('path/to/your/export_2022.csv')
# df_export_2023 = pd.read_csv('path/to/your/export_2023.csv')
# df_export_2024 = pd.read_csv('path/to/your/export_2024.csv')
# (Similar for import data: df_import_2022, etc.)

# Adding year information and concatenating (example for exports)
# df_export_2022['year'] = 2022
# df_export_2023['year'] = 2023
# df_export_2024['year'] = 2024
# df_exports_all = pd.concat([df_export_2022, df_export_2023, df_export_2024], ignore_index=True)
# (Similarly for df_imports_all)

#### 1.2 Data Type Verification and Conversion
The `df.info()` method was utilized to inspect the data types and count of non-null values for each column in the concatenated DataFrames (`df_exports_all` and `df_imports_all`).

A key preprocessing step involved addressing columns representing monetary values (e.g., 'Total Exports ($NZD fob)', 'Imports ($NZD cif)'). These columns were initially loaded as `object` type (strings) due to the presence of characters like commas. The following actions were taken:
*   Non-numeric characters, primarily commas, were removed from these string values.
*   The cleaned string values were then converted to a numeric data type (specifically, integer type `int`) to enable numerical calculations and analysis.

Furthermore, for time-series analysis of monthly trends (covered in a later step), a 'Period' (or 'YearMonth') column was engineered. This involved combining the existing 'Month' and 'year' columns and converting them into a `datetime` object format. This ensures proper chronological sorting and facilitates monthly aggregations.

```python
# Example: Value conversion snippet (illustrative)
# value_columns = ['Total Exports ($NZD fob)', 'Imports ($NZD cif)']
# for df in [df_exports_all, df_imports_all]:
#     for col in value_columns:
#         if col in df.columns:
#             df[col] = df[col].astype(str).str.replace(',', '', regex=False)
#             df[col] = pd.to_numeric(df[col], errors='coerce').fillna(0).astype(int)

### 1.3 Dropping Unnecessary Columns
To streamline the datasets for analysis, columns deemed unnecessary were removed. This included:
Completely blank columns that were artifacts of the CSV import process (e.g., 'Unnamed: 12', 'Unnamed: 13', 'Unnamed: 14').
Quantity-related columns (e.g., 'Unit Qty', 'Exports Qty', 'Re-exports Qty', 'Total Exports Qty') that were not the focus of this particular value-based trade analysis.
The df.drop() method was used for this purpose, specifying the list of columns to be removed.

### 1.4 Adding HS2 Code Column and Descriptions
For aggregated commodity analysis, the Harmonized System (HS) codes needed to be processed.
HS2 Code Extraction: A custom Python function (get_hs2_code) was defined to extract the first two digits (Chapter level) from the detailed 'Harmonised System Code' column. This function was applied to create a new 'HS2_Code' column in both the export and import DataFrames.
HS2 Description Mapping: To make the HS2 codes more interpretable, mapping dictionaries (hs2_export_desc_map and hs2_import_desc_map) were created. These dictionaries link each unique HS2 code to its corresponding official chapter description (typically the first description encountered for that HS2 code in the dataset). This allows for clearer labeling and understanding in subsequent commodity-based visualizations and analyses.

---
### Step 2: Yearly Trade Analysis (2022-2024)

To understand the overall trade performance, the total export value, total import value, and trade balance (exports minus imports) were calculated for each year from 2022 to 2024.

#### 2.1 Data Aggregation
*   **Exports:** The total export value ('Total Exports ($NZD fob)') was summed for each year.
*   **Imports:** Similarly, the total import value ('Imports ($NZD cif)') was summed for each year.
*   **Trade Balance:** The trade balance was calculated as: `Total Export Value - Total Import Value` for each year. A positive value indicates a trade surplus, while a negative value indicates a trade deficit.

#### 2.2 Visualization and Insights
A grouped bar chart was created using Plotly to visualize these yearly figures, showing exports, imports, and the trade balance side-by-side for each year.

*(Here, you would ideally insert an image of your yearly trade summary bar chart. You can take a screenshot of the graph from your Kaggle notebook, save it as an image (e.g., `yearly_trade_summary.png`), upload it to your GitHub repository in the same directory as README.md or an `images` sub-directory, and then embed it in the README like this: `![Yearly Trade Summary](yearly_trade_summary.png)` or `![Yearly Trade Summary](./images/yearly_trade_summary.png)`)*

**Key Observations from the Yearly Trade Data:**
*   **Export Trend:** [Describe the trend you observed for exports. e.g., "Exports showed a consistent increase over the three-year period.", "Exports peaked in 2023 before slightly declining in 2024.", etc.]
*   **Import Trend:** [Describe the trend you observed for imports. e.g., "Imports remained relatively stable with minor fluctuations.", "There was a significant surge in imports in 2022.", etc.]
*   **Trade Balance:** [Describe the trade balance. e.g., "New Zealand experienced a trade deficit in all three years, with the deficit widening/narrowing in [year].", "A trade surplus was observed in [year], primarily due to strong export performance in [mention key sectors if known or inferable from later analysis].", etc.]
*   **(Optional) Specific Year Notes:** [If any year had a particularly noteworthy event or result, mention it. e.g., "The large deficit in 2022 could be attributed to increased import costs for X, Y, Z product categories post-pandemic." - *This is an example, be factual based on your data or general knowledge.*]

The detailed code for this aggregation and Plotly visualization can be found in the [Kaggle Notebook]({your_kaggle_notebook_link_here}). *(Replace {your_kaggle_notebook_link_here} with the actual link you obtained earlier)*.

---
