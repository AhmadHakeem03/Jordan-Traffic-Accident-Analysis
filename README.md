# Jordan Traffic Accident Data Analysis

## Project Overview

This project analyzes traffic accident data in Jordan to uncover trends, patterns, and key insights related to accident severity, contributing factors, temporal patterns, and geographic distribution. The analysis utilizes SQL queries to explore a comprehensive dataset of traffic accidents and their associated conditions.

---

## Data Structure

```
Jordan Traffic Accident/
├── Code/
│   └── SQL Analysis.ipynb          # Main analysis notebook
├── Data/
│   ├── Raw/
│   │   └── JO_traffic_accidents_raw_data_En.csv
│   └── Cleaned/
│       └── JO_traffic_accidents_raw_data_En.csv
└── README.md
```

---

## Data Quality & Cleaning Process

### Raw vs. Cleaned Data

The **Raw** folder contains the original, unprocessed dataset, while the **Cleaned** folder contains data that has undergone quality measurement and validation checks to ensure reliability of analysis results.

### Data Quality Measurements Applied

The following data cleaning steps were implemented to improve data quality and consistency:

1. **Suspicious Row Removal**
   - Removed records with inconsistent Light column values (time of day)
   - Filtered out entries where:
     - Time is between 0:00 AM - 7:00 AM but Light column = "Day"
     - Time is between 8:00 AM - 6:00 PM but Light column = "Night"
   - These anomalies likely represent data entry errors or sensor malfunctions

2. **Driver Age Normalization**
   - Identified and standardized invalid driver ages:
     - Ages recorded as 0 or 1 → marked as "Unknown Age"
     - Ages above 100 years (outliers) → marked as "Unknown Age"
   - This prevents age-related outliers from skewing statistical analysis

3. **Duplicate Row Removal**
   - Identified and removed duplicate records
   - Ensures each accident event is counted only once in the analysis
   - Improves accuracy of aggregate statistics and trend analysis

---

## Key Outcomes of SQL Analysis

### 1. Geographic Severity Patterns
- **Highest-Risk Cities**: Maan (7.46%) and Mafraq (6.71%) have the highest rates of severe injuries and fatalities
- **Anomaly**: Amman, despite having the most accidents (21,360), has the lowest severity rate (0.37%), suggesting urban accidents are typically less severe
- **Insight**: Rural areas experience more severe outcomes per accident

### 2. High-Risk Driver Behaviors
- **Most Dangerous Mistake**: Operating without a license (50% severe/fatal outcome rate)
- **Second Most Dangerous**: Speeding 30–50 km/h above limit (11.11% rate)
- **Third Most Dangerous**: Improper overtaking (8.70% rate)
- **Common vs. Severe**: Violation of traffic rules is the most common cause (26,495 accidents) but has lower severity impact than license violations

### 3. Vehicle Involvement & Speed Correlation
- Average vehicles per accident: 2.1 vehicles
- Two-vehicle crashes are most common (25,259 accidents)
- **Speed Trend**: Clear upward correlation between number of vehicles and average speed
  - Single-vehicle accidents: ~50.6 km/h average
  - Five-to-seven vehicle accidents: 58–62 km/h average
- **Insight**: Higher speeds increase likelihood of multi-vehicle severe accidents

### 4. Temporal Patterns
**By Month:**
- Highest severity: November (1.47%), March (1.34%), December (1.30%)
- Highest volume: September (6,886), June (6,904), January (6,631)

**By Day of Week:**
- Highest severity: Friday (1.33%), Saturday (1.27%) — weekend peak
- Highest volume: Thursday (5,054), Sunday (4,593)

**By Season:**
- Highest severity: Winter (1.06%), Spring (1.05%), Fall (1.01%)
- Lowest severity: Summer (0.86%)
- Highest volume: Fall (8,955 accidents)

---

## Analysis Methodology

- **Data Preprocessing**: Excel for initial data cleaning and quality checks
  - Removal of suspicious rows with time/light inconsistencies
  - Driver age validation and normalization
  - Duplicate row identification and removal
- **Database**: SQLite for structured querying
- **Visualization**: Matplotlib and Seaborn for charts and statistical graphics
- **Deduplication**: Grouped by City/Date or Driver Mistake/Date to ensure that accidents involving multiple vehicles (2+ cars) are calculated only once per incident, preventing double-counting and ensuring accurate daily-level accuracy

---

## Key Files

- **SQL Analysis.ipynb**: Complete analysis with SQL queries, visualizations, and detailed interpretations
- **Cleaned Data**: Used for all analysis to ensure data integrity

---

## Recommendations

1. **Focus Prevention Efforts on High-Risk Areas**: Implement targeted traffic safety programs in Maan and Mafraq
2. **License Enforcement**: Strengthen enforcement of driver licensing requirements
3. **Speed Management**: Implement speed control measures, especially on routes prone to multi-vehicle accidents
4. **Seasonal Safety Campaigns**: Enhance safety awareness during November, March, and winter months
5. **Weekend Vigilance**: Increase traffic monitoring and enforcement on Fridays and Saturdays

---

**Last Updated**: June 2026
