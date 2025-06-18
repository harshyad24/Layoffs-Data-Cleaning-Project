# Layoffs Data Cleaning Project

A comprehensive SQL data cleaning project analyzing global layoffs data from 2022, focusing on data standardization, duplicate removal, and preparing the dataset for exploratory data analysis.

## 📊 Project Overview

This project demonstrates end-to-end data cleaning techniques using MySQL to process layoffs data from various companies worldwide. The dataset contains information about layoffs including company details, locations, industries, layoff numbers, and funding information.

## 🎯 Objectives

- Clean and standardize messy real-world data
- Remove duplicate entries while preserving data integrity
- Handle missing values appropriately
- Prepare data for meaningful analysis
- Demonstrate best practices in SQL data cleaning

## 📁 Dataset

**Source**: [Kaggle - Layoffs 2022 Dataset](https://www.kaggle.com/datasets/swaptr/layoffs-2022)

**Original Columns**:
- `company` - Company name
- `location` - Company location
- `industry` - Industry sector
- `total_laid_off` - Number of employees laid off
- `percentage_laid_off` - Percentage of workforce laid off
- `date` - Date of layoffs
- `stage` - Company funding stage
- `country` - Country location
- `funds_raised_millions` - Funding raised in millions

## 🛠️ Technologies Used

- **Database**: MySQL
- **Tools**: MySQL Workbench
- **Techniques**: Window functions, CTEs, data standardization, duplicate detection

## 📋 Data Cleaning Process

### 1. Data Preparation
- Create staging table to preserve original data
- Set up safe working environment with backups

### 2. Duplicate Removal
- Identify duplicates using ROW_NUMBER() window function
- Create comprehensive partitioning strategy
- Remove duplicate entries while preserving unique records

### 3. Data Standardization
- **Industry**: Standardize variations (e.g., "Crypto Currency" → "Crypto")
- **Country**: Remove trailing periods and inconsistencies
- **Date**: Convert text dates to proper DATE format
- **Text Fields**: Trim whitespace and handle empty strings

### 4. Null Value Handling
- Convert empty strings to NULL values
- Populate missing industry data where possible using company matching
- Preserve meaningful NULL values for analysis

### 5. Data Validation
- Remove records with no useful layoff information
- Clean up temporary columns
- Validate final dataset integrity

## 🗂️ File Structure

```
layoffs-data-cleaning/
├── README.md
├── data/
│   └── raw_data.sql              # Original dataset
├── sql/
│   ├── 01_setup.sql              # Initial setup and staging
│   ├── 02_remove_duplicates.sql  # Duplicate identification and removal
│   ├── 03_standardize_data.sql   # Data standardization
│   ├── 04_handle_nulls.sql       # Null value processing
│   └── 05_final_cleanup.sql      # Final cleanup and validation
└── docs/
    └── data_dictionary.md        # Column definitions and notes
```

## 🚀 Getting Started

### Prerequisites
- MySQL Server 8.0+
- MySQL Workbench (recommended)
- Access to the layoffs dataset

### Setup Instructions

1. **Clone or download the project files**

2. **Create the database**:
   ```sql
   CREATE SCHEMA world_layoffs;
   ```

3. **Import the raw data**:
   ```sql
   -- Create the original table and import your CSV data
   CREATE TABLE world_layoffs.layoffs (
       company TEXT,
       location TEXT,
       industry TEXT,
       total_laid_off INT,
       percentage_laid_off TEXT,
       date TEXT,
       stage TEXT,
       country TEXT,
       funds_raised_millions INT
   );
   ```

4. **Run the cleaning scripts in order**:
   - Execute each SQL file in the `sql/` directory sequentially
   - Follow the numbered order (01, 02, 03, etc.)

## 🔍 Key SQL Techniques Demonstrated

### Window Functions
```sql
ROW_NUMBER() OVER (
    PARTITION BY company, location, industry, total_laid_off,
                percentage_laid_off, date, stage, country, funds_raised_millions
) AS row_num
```

### Data Standardization
```sql
-- Standardize industry names
UPDATE layoffs_staging2
SET industry = 'Crypto'
WHERE industry IN ('Crypto Currency', 'CryptoCurrency');

-- Clean country names
UPDATE layoffs_staging2
SET country = TRIM(TRAILING '.' FROM country);
```

### Safe Data Operations
```sql
-- Disable safe mode for bulk operations
SET SQL_SAFE_UPDATES = 0;
-- Perform operations
-- Re-enable safe mode
SET SQL_SAFE_UPDATES = 1;
```

## 📈 Results

### Before Cleaning
- Raw dataset with inconsistencies
- Duplicate entries
- Mixed data formats
- Empty and null values

### After Cleaning
- ✅ Standardized industry categories
- ✅ Consistent country names
- ✅ Proper date formatting
- ✅ Removed duplicates
- ✅ Clean null value handling
- ✅ Validated data integrity

## 🎓 Learning Outcomes

This project demonstrates:
- **Data Quality Assessment**: Identifying common data quality issues
- **SQL Best Practices**: Proper use of staging tables, window functions, and CTEs
- **Error Handling**: Managing MySQL safe mode and transaction boundaries
- **Data Validation**: Ensuring cleaning operations maintain data integrity
- **Documentation**: Comprehensive commenting and process documentation

## 🔧 Common Issues & Solutions

### Safe Update Mode Error
**Problem**: `Error Code: 1175. You are using safe update mode...`

**Solution**:
```sql
SET SQL_SAFE_UPDATES = 0;
-- Your UPDATE/DELETE operations
SET SQL_SAFE_UPDATES = 1;
```

### CTE Delete Issues
**Problem**: `The target table DELETE_CTE of the DELETE is not updatable`

**Solution**: Use staging table approach with ROW_NUMBER() column instead of direct CTE deletion.

## 📊 Sample Queries for Analysis

After cleaning, you can perform analysis like:

```sql
-- Top 10 companies by total layoffs
SELECT company, SUM(total_laid_off) as total_layoffs
FROM layoffs_staging2
WHERE total_laid_off IS NOT NULL
GROUP BY company
ORDER BY total_layoffs DESC
LIMIT 10;

-- Layoffs by industry
SELECT industry, COUNT(*) as layoff_events, SUM(total_laid_off) as total_affected
FROM layoffs_staging2
WHERE total_laid_off IS NOT NULL
GROUP BY industry
ORDER BY total_affected DESC;
```

## 🤝 Contributing

This is a learning project, but suggestions for improvements are welcome! Areas for enhancement:
- Additional data validation checks
- More sophisticated duplicate detection algorithms
- Performance optimization for larger datasets
- Additional standardization rules

## 📝 Notes

- Always work with staging tables when cleaning data
- Validate your results at each step
- Keep the original data unchanged
- Document your cleaning decisions
- Test queries on small samples first
