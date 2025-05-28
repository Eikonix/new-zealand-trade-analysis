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
