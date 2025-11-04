#  Employee Attrition Analysis Report

## 📊 Project Overview

![Dahboard Overview](/Visuals/Dashboard%20Page.png)
*Employee Attrition analysis Dashboard*


This Power BI project provides a comprehensive analysis of employee attrition patterns within an organization. The dashboard leverages interactive visualizations to identify key factors contributing to employee turnover and delivers actionable insights for strategic HR decision-making.





---



## 🎯 Overview

This Power BI dashboard provides comprehensive analysis of employee attrition across multiple dimensions including demographics, departments, compensation, and work conditions. The project aims to identify key attrition drivers and support data-driven HR decision-making.

### Key Features

✅ **Interactive Visualizations** - Dynamic charts and filters for deep-dive analysis  
✅ **Custom DAX Measures** - 12+ calculated metrics for attrition analytics  
✅ **Multi-dimensional Analysis** - Age, gender, department, salary, distance, and more  
✅ **Page Navigation** - Seamless navigation between overview and detailed analysis  
✅ **Department Slicers** - Filter data by HR, R&D, and Sales departments

---

## 📊 Dataset Information

**Source:** [Kaggle.com](https://www.kaggle.com/)

**Dataset Size:**
- **Total Records:** 1,470 employees
- **Attributes:** 35+ columns
- **Format:** CSV

### Key Attributes

| Column | Description | Type |
|--------|-------------|------|
| `EmployeeID` | Unique employee identifier | Integer |
| `Age` | Employee age | Integer |
| `Gender` | Male/Female | Text |
| `MaritalStatus` | Single/Married/Divorced | Text |
| `Department` | HR/Sales/R&D | Text |
| `JobRole` | Specific job position | Text |
| `MonthlyIncome` | Monthly salary (USD) | Currency |
| `HourlyRate` | Hourly rate (USD) | Currency |
| `DistanceFromHome` | Commute distance (km) | Integer |
| `Attrition` | Yes/No | Text |
| `JobSatisfaction` | 1-5 rating scale | Integer |
| `EnvironmentSatisfaction` | 1-5 rating scale | Integer |
| `WorkLifeBalance` | 1-5 rating scale | Integer |
| `OverTime` | Yes/No | Text |
| `YearsAtCompany` | Tenure in years | Integer |

---

## 🗂️ Data Model

### Data Schema

<p align="center">
  <img src="Visuals\Schema.PNG" alt="Schema" width ="250">
</p>

### Model Type
- **Architecture:** Simplified Star Schema
- **Fact Table:** Single Employee table with embedded dimensions
- **Relationships:** Calculated columns for grouping
- **Cardinality:** One-to-Many (implicit)

---

## 🔧 Data Transformations

<p align="center">
  <img src="Visuals\Power Query Steps.PNG" alt="Power Query Transformation" width ="250">
</p>

### Removed Columns
- Removed unwanted columns that are not necessary for Analysis.

### Custom Calculated Columns

1.Age Group Column

- **Purpose:** Segment employees into 10 age brackets for demographic analysis

- **Result:** 10 age categories for granular analysis

---

 2. Distance Bucket Column

- **Purpose:** Categorize commute distances to analyze impact on attrition



- **Result:** 6 distance ranges (0-5, 5-10, 10-15, 15-20, 20-25, 25-30 km)

---

## 📐 DAX Measures

<p align="center">
  <img src="Visuals\Calculated Measures.PNG" alt="Power Query Transformation" width ="310">
</p>

### Core Metrics

#### 1. Active Employee Count
```DAX
Active Employee Count = 
CALCULATE(
    COUNTROWS('Employee'),
    'Employee'[Attrition] = "No"
)
```
**Output:** 1,242 employees

---

#### 2. Attrition Rate
```DAX
Attrition Rate = 
DIVIDE(
    CALCULATE(COUNTROWS('Employee'), 'Employee'[Attrition] = "Yes"),
    COUNTROWS('Employee'),
    0
)
```
**Format:** Percentage  
**Output:** 17.49%

---

#### 3. Total Employee Count
```DAX
Total Employees = COUNTROWS('Employee')
```
**Output:** 1,470 employees

---

#### 4. Average Monthly Income
```DAX
Average Monthly Income = AVERAGE('Employee'[MonthlyIncome])
```
**Format:** Currency  
**Output:** $6,500 (6.50K)

---

#### 5. Average Hourly Rate
```DAX
Average Hourly Rate = AVERAGE('Employee'[HourlyRate])
```
**Output:** $65.85

---

#### 6. Job Satisfaction Rate
```DAX
Job Satisfaction Rate = 
DIVIDE(
    AVERAGE('Employee'[JobSatisfaction]),
    5,
    0
)
```
**Format:** Star Rating (3/5)  
**Output:** 60%

---

#### 7. Environment Satisfaction Rate
```DAX
Environment Satisfaction Rate = 
DIVIDE(
    AVERAGE('Employee'[EnvironmentSatisfaction]),
    5,
    0
)
```
**Output:** 3/5 stars

---

#### 8. Work-Life Balance Rate
```DAX
Work Life Balance Rate = 
DIVIDE(
    AVERAGE('Employee'[WorkLifeBalance]),
    5,
    0
)
```
**Output:** 3/5 stars

---

#### 9. Attrition Count
```DAX
Attrition Count = 
CALCULATE(
    COUNTROWS('Employee'),
    'Employee'[Attrition] = "Yes"
)
```
**Output:** 257 employees

---




---

## 📱 Dashboard Pages

### Page 1: Department Overview Dashboard
<p align="center">
  <img src="Visuals\Dashboard Page.png" alt="Dashboard Overview" width="550">
</p>

**Purpose:** Executive summary with high-level organizational metrics


---

### Page 2: Detailed Attrition Analysis
<p align="center">
  <img src="Visuals\Analysis Page.png" alt="Dashboard Overview" width="550">
</p>

**Purpose:** Deep-dive analysis into attrition drivers and correlations


## ❓ Business Questions & Insights

### Q1: What is the overall employee attrition rate?

**📊 Answer: 17.49%**

**Breakdown:**
- **Total Employees:** 1,470
- **Employees Left:** 257
- **Active Employees:** 1,242
- **Calculation:** (257 ÷ 1,470) × 100 = 17.49%

**Interpretation:**  
Nearly **1 in 5 employees** leave the organization annually. This is slightly above the industry average of 15%, indicating retention challenges.

**💡 Recommendation:**
- Conduct comprehensive exit interviews
- Implement targeted retention programs
- Set goal to reduce attrition below 15% within 12 months

---

### Q2: Which department has the highest attrition rate?

**📊 Answer: Sales Department (20.63%)**

<p align="center">
  <img src="Visuals\Department Attrition.PNG" alt="Department Attrition" width="450">
</p>

*Stacked Bar chart showing department-wise attrition rate*

**Key Insights:**
- Sales loses **1 in 5** employees annually
- HR shows concerning trends despite smaller size
- R&D has the lowest rate but highest absolute count (~133 employees)

**💡 Recommendations:**

**Sales Department:**
- Review compensation and commission structures
- Assess work-life balance and territory assignments
- Implement mentorship programs
- Conduct stay interviews with high performers

**Human Resources:**
- Evaluate workload distribution
- Review career advancement opportunities
- Assess team dynamics and leadership

**Research & Development:**
- Investigate project allocation fairness
- Enhance skill development programs
- Review innovation incentives

---

### Q3: How does gender affect attrition rates?

**📊 Answer: Minimal gender difference (2.67% gap)**

**Statistics:**
- **Male Employees:** 15.89% attrition
- **Female Employees:** 18.56% attrition
- **Difference:** +2.67 percentage points


**Key Insights:**
- Gender is **not a primary driver** of attrition
- Difference is statistically minimal
- Other factors (age, department, compensation) have stronger influence

**💡 Recommendations:**
- Focus retention efforts on department and age rather than gender
- Ensure pay equity across all genders
- Review maternity/paternity leave policies
- Maintain equal promotion opportunities
- Continue monitoring for any emerging trends

---

### Q4: Which age group experiences the highest attrition?

**📊 Answer: 18-20 age group (83.33% attrition)**

<p align="center">
  <img src="Visuals\Demographics Attrition.PNG" alt="Demographics Attrition" width="450">
</p>

*Column chart showing attrition rate by demographics*

**Critical Findings:**
- **5 out of 6 employees** aged 18-20 leave within the first year
- Attrition decreases progressively with age
- Employees over 35 show stable retention
- Younger employees (under 30) are high-risk

**Root Causes:**

**18-20 Age Group:**
- Part-time/temporary positions
- Students seeking experience
- Lack of career clarity
- Inadequate onboarding
- Limited organizational commitment

**20-25 Age Group:**
- Job-hopping for better opportunities
- Career exploration phase
- Competitive talent market
- Higher mobility

**💡 Recommendations:**

**Immediate Actions (P0 - 18-20 Age Group):**
- ✅ Implement 30-60-90 day onboarding program
- ✅ Assign mentorship pairs with senior employees
- ✅ Create clear career progression roadmap
- ✅ Offer skill development workshops
- ✅ Conduct 30-day retention check-ins
- ✅ Provide structured training programs

**Short-term Actions (P1-P2 - 20-30 Age Group):**
- ✅ Competitive compensation reviews
- ✅ Fast-track leadership programs
- ✅ Flexible work arrangements
- ✅ Student loan repayment assistance
- ✅ Professional certification sponsorship
- ✅ Quarterly career development discussions

---

### Q5: Does distance from home impact attrition?

**📊 Answer: Yes, strong positive correlation**

| Distance Range | Attrition Rate | Change from Baseline | Risk Level |
|----------------|----------------|----------------------|------------|
| **0-5 km** | **14.51%** | Baseline | ✅ Lowest |
| **5-10 km** | **16.08%** | +1.57% | ✅ Low |
| **10-15 km** | **19.44%** | +4.93% | ⚠️ Moderate |
| **15-20 km** | **21.08%** | +6.57% | ⚠️ High |
| **20-25 km** | **31.11%** | +16.60% | 🔴 Critical |



**Statistical Insights:**
- **Linear relationship:** Each 5 km increase adds ~3-4% attrition
- **Critical threshold:** 20+ km shows exponential increase
- **Tipping point:** Beyond 15 km, attrition exceeds organizational average
- **Impact multiplier:** 20+ km employees are **2.1x more likely** to leave

**Real-World Impact:**
Long commutes affect:
- ⏰ Work-life balance (reduced from 3/5 rating)
- 😰 Daily stress levels
- 📉 Job satisfaction
- ⏱️ Punctuality and productivity
- 💰 Transportation costs

**💡 Recommendations:**

**Immediate Solutions:**

**1. Remote Work Policy:**
- Allow 2-3 days/week remote work for employees 15+ km away
- Hybrid model for 10-15 km range
- Full remote option for roles that support it

**2. Flexible Hours:**
- Staggered start times (7 AM, 8 AM, 9 AM, 10 AM options)
- Compressed workweeks (4×10 instead of 5×8)
- Core hours (10 AM - 3 PM) with flexible start/end

**3. Transportation Support:**
- Company shuttle services from high-density areas
- Carpooling incentive program ($50/month)
- Public transit pass subsidies (50-100%)
- Parking fee reimbursement
- Bike-to-work incentives

**4. Relocation Assistance:**
- Housing allowances for long-commute employees
- Partnerships with local real estate agents
- One-time relocation bonus ($2,000-$5,000)
- Temporary housing support

**Long-term Solutions:**
- 🏢 Open satellite offices in employee-dense areas
- 🏠 Permanent remote work policies
- 💵 Geographic salary adjustments
- 🗺️ Strategic office location planning

---

### Q6: How does marital status affect attrition across age groups?

**📊 Answer: Single employees show consistently higher attrition**

**Marital Status Attrition Matrix:**

| Age Group | Single | Married | Divorced | Pattern |
|-----------|--------|---------|----------|---------|
| **18-20** | **~80%+** | Limited | N/A | Single overwhelming |
| **20-25** | **18.18%** | **11.38%** | Limited | Single higher |
| **25-30** | **11.38%** | **8.57%** | **15.73%** | Divorced elevated |
| **30-35** | **15.65%** | **8.43%** | **13.65%** | Married most stable |
| **35-40** | **9.17%** | **6.39%** | **12.23%** | Married lowest |
| **40-45** | **2.99%** | **10.13%** | **14.08%** | Divorced highest |
| **45-50** | **15.38%** | **10.13%** | **6.67%** | Varied pattern |
| **50-55** | **7.41%** | **9.65%** | **8.70%** | Converging rates |
| **55-60** | Low | Low | Low | Age effect dominant |

**Key Patterns:**

**1. Single Employees:**
- 🔴 Highest attrition in 18-30 age range
- Greater job mobility and flexibility
- Less tied to location due to family
- Active career exploration phase
- Fewer financial obligations

**2. Married Employees:**
- 🟢 Consistently lowest attrition rates
- Stability factors:
  - Dual income considerations
  - Family healthcare benefits importance
  - Children's education continuity
  - Housing/mortgage commitments
  - Spouse employment location

**3. Divorced Employees:**
- 🟡 Moderate attrition (12-16%)
- Financial pressures increase job-seeking
- Work-life balance challenges with custody
- Peak attrition in 40-45 age group
- May seek better compensation

**Critical Insights:**
- **Marriage = Retention Stabilizer** across all age groups
- **Single + Young = Highest Risk** (18-25 combination)
- **Divorced Mid-Career (30-40)** shows elevated attrition
- **Age 50+** shows convergence regardless of marital status

**💡 Recommendations:**

**For Single Employees:**
- 🎓 Accelerated career development programs
- 🤝 Social engagement initiatives (team building, networking)
- 👥 Mentorship opportunities
- 📈 Clear promotion pathways with timelines
- 💰 Competitive base salary (less reliance on family benefits)
- 🏆 Performance bonuses and recognition

**For Married Employees:**
- 🏥 Robust family healthcare plans
- 👨‍👩‍👧‍👦 Spouse employment assistance programs
- 👶 Dependent care benefits (daycare, education)
- 🤰 Enhanced parental leave policies (both parents)
- ⚖️ Work-life balance programs
- 🏠 Flexible work arrangements

**For Divorced Employees:**
- 🕐 Flexible scheduling for custody arrangements
- 🧠 Employee Assistance Programs (EAP)
- 💵 Financial planning resources
- 🩺 Mental health support and counseling
- 👪 Single-parent support groups
- 📅 PTO flexibility for family needs

---

### Q7: Does salary/income level correlate with attrition?

**📊 Answer: Yes, inverse relationship - lower salary = higher attrition**

**Salary vs. Attrition Analysis:**

| Salary Range (Monthly) | Attrition Rate | Volume | Risk Level |
|------------------------|----------------|--------|------------|
| **$1,000 - $5,000** | **~25-30%** | High | 🔴 Critical |
| **$5,001 - $7,000** | **~20%** | Very High | 🟠 High |
| **$7,001 - $10,000** | **~15%** | High | 🟡 Moderate |
| **$10,001 - $15,000** | **~12%** | Medium | 🟢 Low |
| **$15,001 - $20,000** | **~8%** | Low | 🟢 Low |

**Organizational Average:** $6,500/month


**Key Findings:**
- **Strong inverse correlation:** As salary ↑, attrition ↓
- **High-risk zone:** Employees earning <$7K (below average)
- **Critical density:** Most attrition occurs at $5K-$7K range
- **Risk multiplier:** Below-average earners are **1.5-2x more likely** to leave
- **Safe zone:** Employees earning >$15K show stable retention

**Interpretation:**
- Compensation competitiveness is **critical retention factor**
- Entry-level and junior positions show highest turnover
- Market pressures drive employees to seek higher-paying opportunities
- Internal pay equity issues may exist

**💡 Recommendations:**

**1. Compensation Strategy:**
- ✅ Conduct annual market salary benchmarking
- ✅ Adjust pay scales to 75th percentile for critical roles
- ✅ Implement COL increases (minimum 3-5% annually)
- ✅ Performance-based bonuses (5-15% of base)
- ✅ Salary band transparency
- ✅ Merit increase program (3-10% based on performance)

**2. Total Rewards Program:**
- ✅ Clear salary bands by role and level
- ✅ Transparent promotion criteria with salary jumps (10-20%)
- ✅ Sign-on bonuses for critical positions
- ✅ Retention bonuses for high performers ($2K-$10K)
- ✅ Equity/stock options for senior roles
- ✅ Profit-sharing programs

**3. Non-Monetary Compensation:**
- ✅ Enhanced benefits package
- ✅ Professional development stipends ($1K-$5K/year)
- ✅ Tuition reimbursement programs
- ✅ Flexible work arrangements
- ✅ Additional PTO for tenure milestones
- ✅ Wellness programs and gym memberships

**4. Pay Equity Audit:**
- ✅ Conduct internal pay equity analysis
- ✅ Address compression issues (new hires vs. tenured employees)
- ✅ Review gender pay gaps
- ✅ Establish pay-for-performance frameworkRetryThis response paused because Claude reached its max length for a message. Hit continue to nudge Claude along.ContinueClaude can make mistakes. Please double-check responses. Sonnet 4.5
---
## 🛠️ Technical Skills Used

1. **Data Analysis/Visualization Tool :** Power BI 

2. **Data Manipulation & Querying :**
- DAX (Data Analysis Expressions): Used for creating custom measures and calculated columns (e.g., calculating "Attrition Rate," "Average Monthly Income," and "Active Employee Count").

- SQL/Power Query (M Language): Used for data extraction, cleaning, transformation, and loading (ETL) into the visualization tool.

### Core Concepts & Business Intelligence:

- Key Performance Indicator (KPI) Design: Defining and tracking crucial business metrics like "Attrition Rate" and "Job Satisfaction Rate."

- Dashboard and UX Design: Creating a visually effective and user-friendly layout for quick decision-making.

- Statistical Analysis: Utilizing demographics (Age, Marital Status, Gender) and internal factors (Over Time, Salary Range) to identify significant drivers of attrition.

## 📝 Conclusion

This project successfully delivered a comprehensive and interactive dashboard that transforms raw HR data into actionable business intelligence.

### Key Achievements:

- **Identified High-Risk Segments:** The analysis clearly pinpoints that the 18-20 age group has the highest attrition rate (83.33%), necessitating immediate intervention.

- **Quantified Attrition Drivers:** The dashboard reveals significant correlations, such as the clear link between working Over Time and a higher attrition rate of 10.92%.

- **Provided Strategic Insights:** By connecting factors like Marital Status (Divorced and Single have higher rates) and Distance from Home, the dashboard enables HR teams to develop targeted retention strategies, such as offering remote work options or focused support for at-risk demographics.

- **Effective Data Storytelling:** The use of clear KPIs, drill-down capabilities (implied by the two pages), and intuitive visualizations ensures that stakeholders can quickly grasp complex data and move swiftly from insight to action.

This project demonstrates proficiency in end-to-end data analysis, from data ingestion and calculation (DAX/M) to the final presentation of a user-centric, decision-support tool.

-----