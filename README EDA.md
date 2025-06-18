# World Layoffs Exploratory Data Analysis

A comprehensive SQL-based exploratory data analysis (EDA) of global layoffs data, examining patterns, trends, and insights from corporate workforce reductions.

## 📊 Dataset Overview

The analysis uses the `world_layoffs.layoffs_staging2` table containing cleaned layoff data with the following key fields:
- `company` - Company name
- `location` - Geographic location
- `country` - Country
- `industry` - Industry sector
- `total_laid_off` - Number of employees laid off
- `percentage_laid_off` - Percentage of workforce affected
- `date` - Date of layoff announcement
- `stage` - Company funding stage
- `funds_raised_millions` - Total funding raised (in millions)

## 🎯 Analysis Objectives

This analysis aims to uncover:
- Scale and impact of layoffs across companies and industries
- Geographic and temporal patterns in workforce reductions
- The relationship between company funding and layoff decisions
- Identification of companies and sectors most affected
- Trends and patterns over time

## 📈 Key Findings

### Major Discoveries
- **Startup Vulnerability**: Companies with 100% layoffs were predominantly startups, including well-funded companies like Quibi ($2B+ raised)
- **Geographic Concentration**: Layoffs clustered in major tech hubs
- **Industry Impact**: Technology sector disproportionately affected
- **Temporal Patterns**: Clear acceleration periods are visible in rolling totals

### Notable Cases
- **BritishVolt**: EV company with complete workforce reduction
- **Quibi**: Streaming startup that raised ~$2 billion before shutting down
- **Tech Giants**: Major companies with significant single-day layoff events

## 🔍 Analysis Structure

### 1. Basic Exploratory Analysis
- Maximum and minimum layoff statistics
- Companies with 100% workforce reductions
- Funding analysis of failed companies

### 2. Aggregated Insights
- Top companies by total layoffs
- Geographic distribution analysis
- Industry and funding stage breakdowns
- Year-over-year trends

### 3. Advanced Analytics
- **Company Rankings by Year**: Using window functions to rank companies annually
- **Rolling Totals**: Monthly cumulative layoff tracking
- **Temporal Analysis**: Identifying peak periods and patterns

## 🛠️ Technical Implementation

### SQL Techniques Used
- **Window Functions**: `DENSE_RANK()`, `SUM() OVER()`
- **Common Table Expressions (CTEs)**: For complex multi-step queries
- **Date Functions**: `YEAR()`, `SUBSTRING()` for temporal analysis
- **Aggregation**: `GROUP BY`, `SUM()`, `AVG()`, `COUNT()`
- **String Functions**: Date formatting and manipulation

### Key Queries
1. **Basic Statistics**: Min/max values and distribution analysis
2. **Company Analysis**: Single vs. cumulative layoff comparisons
3. **Geographic Trends**: Location and country-based aggregations
4. **Temporal Patterns**: Year-over-year and rolling total calculations
5. **Advanced Rankings**: Top companies by year with window functions

## 📋 Query Categories

### Beginner Level
- Simple SELECT statements with basic filtering
- MIN/MAX calculations
- Basic sorting and limiting

### Intermediate Level
- GROUP BY aggregations
- Multiple column sorting
- Subqueries for filtering

### Advanced Level
- Complex CTEs with multiple levels
- Window functions for rankings
- Rolling calculations
- Time-series analysis

## 🚀 Getting Started

### Prerequisites
- MySQL database access
- `world_layoffs.layoffs_staging2` table with cleaned data

### Running the Analysis
1. Execute basic EDA queries to understand data structure
2. Run aggregated analysis for high-level insights
3. Use advanced queries for detailed trend analysis
4. Consider the enhanced analysis suggestions for deeper insights

## 📊 Potential Extensions

### Additional Analysis Ideas
- **Seasonal Patterns**: Monthly layoff distributions
- **Repeat Events**: Companies with multiple layoff rounds
- **Funding Correlation**: Relationship between funding and layoff scale
- **Industry Evolution**: Sector-specific temporal trends
- **Geographic Clustering**: Regional impact analysis
- **Survival Analysis**: Companies avoiding layoffs during peak periods

### Data Enhancement Opportunities
- **Economic Indicators**: Correlation with market conditions
- **Company Metrics**: Revenue, employee count, stock performance
- **Industry Context**: Sector-specific challenges and opportunities
- **Geographic Data**: Cost of living, business environment factors

## 📝 Code Quality Features

- **Consistent Formatting**: Clear indentation and structure
- **Descriptive Comments**: Explaining complex logic and business context
- **Modular Approach**: Separate queries for different analysis aspects
- **Performance Considerations**: Efficient use of indexes and filters

## 🔧 Best Practices Demonstrated

- **Data Validation**: NULL checking and data quality considerations
- **Incremental Complexity**: Building from simple to advanced queries
- **Business Context**: Connecting technical analysis to real-world insights
- **Documentation**: Clear commenting and result interpretation

## 📈 Business Value

This analysis provides:
- **Strategic Insights**: Understanding market trends and competitive landscape
- **Risk Assessment**: Identifying vulnerable company types and sectors
- **Investment Intelligence**: Funding vs. survival correlation analysis
- **Economic Indicators**: Workforce reduction patterns as economic signals

## 🤝 Contributing

To extend this analysis:
1. Add data validation queries for quality assurance
2. Implement additional statistical measures
3. Create visualization-ready output formats
4. Develop predictive models based on historical patterns
