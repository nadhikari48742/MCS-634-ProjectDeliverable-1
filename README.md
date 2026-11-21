# MSCS 634 – Project Deliverable 1
## Data Collection, Cleaning, and Exploration

### Dataset
This project uses the **Online Retail** dataset from the UCI Machine Learning Repository. The dataset contains 541,909 transaction-line records and 8 attributes covering invoices, products, quantities, invoice dates, unit prices, customer identifiers, and countries. The records span 1 December 2010 to 9 December 2011.

- Official dataset page: https://archive.ics.uci.edu/dataset/352/online+retail
- DOI: https://doi.org/10.24432/C5BW33
- Local data file: `Online Retail.xlsx`

The dataset meets the assignment's minimum of 500 records and 8 attributes. **Note:** It has exactly 8 attributes; confirm with the instructor if “8–10 attributes” is intended to require more than 8.

### Why this dataset was selected
The data represents real retail transactions and includes numerical, categorical, product, customer, and date fields. It supports exploratory sales analysis and can be extended in later deliverables to regression, classification, customer clustering, and association-rule mining.

### Files
- `Online_Retail_Analysis.ipynb` – commented Python notebook containing data loading, inspection, cleaning, feature creation, EDA, visualizations, and interpretation prompts.
- `Online Retail.xlsx` – original dataset supplied for this project.

### Major cleaning and preparation steps
1. Preserved the original imported dataframe as `raw_df`.
2. Standardized text fields by trimming surrounding whitespace.
3. converted date and numeric columns to appropriate data types.
4. Removed exact duplicate rows from the analysis copy.
5. Removed rows missing essential transaction fields.
6. Created an `IsCancellation` flag based on invoice numbers beginning with `C`.
7. Created a line-item `Revenue` variable as `Quantity * UnitPrice`.
8. Kept an all-transactions dataset to preserve returns/cancellations.
9. Created a positive-sales dataset excluding cancellation invoices, non-positive quantities, and non-positive unit prices.
10. Created a customer-level subset containing known CustomerID values.

Missing CustomerID values were not imputed because invented identifiers would create false customer relationships. Extreme values were flagged and visualized rather than automatically deleted, since large orders may be genuine.

### Initial data-quality findings
The supplied workbook was inspected and showed:
- 541,909 rows and 8 columns.
- 135,080 missing CustomerID values.
- 1,454 missing Description values.
- 5,268 exact duplicate rows.
- 10,624 negative Quantity values.
- 2,515 zero UnitPrice values and 2 negative UnitPrice values.
- 9,288 invoice numbers beginning with `C`.
- 38 distinct countries and 4,372 distinct non-missing customer identifiers.

These are raw-data inspection counts. The notebook reports the resulting row counts after each cleaning step when executed.

### Exploratory analysis
The notebook includes:
- Histograms of quantity, unit price, and line-item revenue.
- Boxplots and IQR-based outlier flags.
- Monthly positive-sales revenue trend.
- Top 10 countries by positive-sales revenue.
- Top products by positive-sales revenue.
- Correlation heatmap for quantity, unit price, and revenue.

Run the notebook to generate the charts and data tables, then add a short interpretation of the actual outputs in the findings section.

### Challenges and how they were addressed
- **Missing customer identifiers:** retained for general transaction analysis but excluded from customer-level analysis.
- **Returns and cancellations:** preserved in the all-transactions dataset and separated from positive-sales analysis.
- **Duplicate records:** exact duplicates removed from the working copy.
- **Extreme quantities/prices:** flagged and inspected; not automatically deleted.
- **Country imbalance:** the United Kingdom dominates the dataset, so country comparisons need careful interpretation.

### How to run
1. Download or clone this repository.
2. Ensure `Online Retail.xlsx` is in the same folder as the notebook.
3. Install the required packages if necessary:

   ```bash
   pip install pandas numpy matplotlib seaborn openpyxl jupyter
   ```

4. Open and run `Online_Retail_Analysis.ipynb` from top to bottom.

### Reference
Chen, D. (2015). *Online retail* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5BW33

UCI Machine Learning Repository. (n.d.). *Online Retail*. https://archive.ics.uci.edu/dataset/352/online+retail
