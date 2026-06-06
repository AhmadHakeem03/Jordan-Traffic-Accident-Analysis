# Jordan Traffic Accident Data Analysis

## Project Overview

This project analyzes traffic accident data in Jordan to uncover trends, patterns, and key insights related to accident severity, contributing factors, temporal patterns, and geographic distribution. The analysis utilizes SQL queries to explore a comprehensive dataset of traffic accidents and their associated conditions.

---

## Data Structure

```
Jordan Traffic Accident/
├── Code/
│   └── SQL Analysis.ipynb                    # Main analysis notebook
├── Data/
│   ├── Raw/
│   │   └── JO_traffic_accidents_raw_data_En.csv
│   └── Cleaned/
│       ├── JO_traffic_accidents_raw_data_En.csv
│       └── JO_traffic_accidents_cleaned_data_En_V2.csv    # Enhanced dataset with Power BI columns
├── PowerBI/
│   └── JO_Traffic_Accident_Dashboard                      # Interactive dashboard
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

## Data Enhancement for Power BI Performance

### Version 2: Enhanced Dataset (V2)

To optimize Power BI dashboard performance and eliminate the need for recalculated columns during report refresh, the cleaned dataset was enhanced with **helper columns** pre-calculated in Excel. The **JO_traffic_accidents_cleaned_data_En_V2.csv** includes the following helper fields:

#### Helper Columns Created

**1. Age Group** - Groups driver ages into 7 demographic segments (Under 18, 18-25, 26-35, 36-45, 46-55, 56-65, 65+) for easier demographic analysis and dashboard filtering

**2. Age Group Order** - Provides numeric sorting order for age group visualizations to ensure correct sequence in Power BI (assigns 0 for Unknown Age, then 1-7 for each age bracket)

**3. Expected Vehicle** - Maps vehicle license classes to standardized vehicle type categories (e.g., Class 1 → Motorcycle, Class 3 → Passenger Vehicle, Class 6a/6b/6ab → Heavy Vehicle/Bus/Trailer) for clearer categorization

**4. License Status** - Flags potential mismatches between driver license class and actual vehicle type to identify data quality issues (e.g., when license class doesn't align with vehicle classification)

**5. Violation Flag** - Binary indicator (1 or 0) marking records with license-vehicle mismatches for quick filtering and data quality monitoring in Power BI

---

## Power BI Dashboard Insights

### Page 1: Driver & Vehicle Risk Analysis

**Key Findings:**

1. **Age Group Risk Distribution**
   - **Highest Risk Segment**: 26-35 age group accounts for 20,300 accidents
   - **Second Highest**: 36-45 age group with 14,000 accidents
   - **Business Implication**: Young-to-middle-aged drivers (26-45) represent the largest accident demographic, suggesting need for targeted safety campaigns and intervention programs in this age bracket

2. **Vehicle Type Accident Frequency**
   - **Most Accidents**: Passenger vehicles (up to 9 seats) lead with 54,000 incidents
   - **Second Most**: Trucks with 7,000 accidents
   - **Insight**: Private passenger vehicles dominate the accident distribution, reflecting high circulation volume on roads

3. **Most Critical Driver Error**
   - **Improper Lane Changes**: Identified as the most dangerous mistake category
   - **Fatal Incidents**: 58 deaths attributed to improper lane changes (2018 data)
   - **Business Action**: Implement lane discipline awareness campaigns and consider road markings enhancement in high-risk corridors

### Page 2: Geographic & Environmental Risk Patterns

**Key Findings:**

1. **Weather Conditions Impact**
   - **Dominant Condition**: Clear weather accounts for the majority of recorded accidents across cities
   - **Notable Exception - Amman**: Slight but measurable percentage of rain-related accidents
   - **Insight**: Weather does not appear to be a primary accident driver; road infrastructure and driver behavior are likely more significant factors

2. **Fatality Distribution by Driver License Class**
   - **Highest Deaths**: Class 3 (Passenger Vehicle) with 123 deaths
   - **Secondary Risk**: Class 6ab (Heavy Vehicle/Bus/Trailer) with 18 deaths
   - **Pattern**: Passenger vehicle accidents account for the majority of fatalities, correlating with their higher accident frequency

3. **Road Surface Conditions**
   - **Predominant State**: Dry surfaces across all cities
   - **Secondary Condition**: Wet surfaces present in minority of cases
   - **Infrastructure Recommendation**: Enhanced drainage systems (تصريف المياه) infrastructure improvements needed to prevent wet surface accidents during rainy seasons

4. **Road Properties Distribution**
   - **Standard Pattern**: Flat, straight roads dominate across all governorates
   - **Amman Exception**: Very low percentage of upright straight roads, reflecting urban environment complexity
   - **Interpretation**: Road design is relatively consistent; accident variations driven more by traffic volume and driver behavior than road geometry

---

## Analysis Methodology

- **Data Preprocessing**: Excel for initial data cleaning and quality checks
  - Removal of suspicious rows with time/light inconsistencies
  - Driver age validation and normalization
  - Duplicate row identification and removal
  - Pre-calculated field engineering for Power BI optimization
- **Database**: SQLite for structured querying
- **Visualization**: 
  - Matplotlib and Seaborn for statistical charts
  - Power BI for interactive dashboard and drill-down analysis
- **Deduplication**: Grouped by City/Date or Driver Mistake/Date to ensure that accidents involving multiple vehicles (2+ cars) are calculated only once per incident, preventing double-counting and ensuring accurate daily-level accuracy

---

## Business Recommendations

Based on the comprehensive analysis of traffic accident data in Jordan:

1. **Driver Safety Interventions**: Target 26-45 age demographic with specialized training programs focusing on lane discipline and speed awareness
2. **Infrastructure Improvement**: Prioritize drainage system enhancements (تصريف المياه) in urban areas to reduce wet surface accidents
3. **License Class Enforcement**: Strengthen validation mechanisms for Class 3 (Passenger Vehicle) license holders given their high fatality rate
4. **Temporal Campaigns**: Intensify road safety campaigns during high-risk periods (November, March, December, and weekends)
5. **Geographic Focus**: Implement severity-reduction programs in rural governorates (Maan, Mafraq, Tafila) with proven intervention strategies

---

## Key Files

- **SQL Analysis.ipynb**: Complete SQL analysis with queries, visualizations, and detailed interpretations
- **JO_Traffic_Accident_Dashboard**: Interactive Power BI dashboard with geographic, temporal, and demographic drill-down capabilities
- **Cleaned Data (V2)**: Enhanced dataset with pre-calculated columns optimized for Power BI reporting

---

**Last Updated**: June 2026
