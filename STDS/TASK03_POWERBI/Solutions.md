📞 Call Center Analytics — Power BI Solution
1️⃣ Data Exploration & Preparation
    -The first step was to understand the Call Center dataset and its structure. Key fields examined included:
Call timestamp
    -Call reason
    -Communication channel
    -Customer sentiment
  -Call duration
  -Data Cleaning Tasks Performed:
     *Verified and corrected data types
     *Ensured date and numeric columns were properly formatted
     *checked for missing values and inconsistencies

2️⃣ Date Table Creation

   -o support accurate time-based analysis, a separate Date Table was created using DAX:

     Date table:
 CENDAR(
    MIN('Call Center_Call Center'[Call Timestamp]),
    MAX('Call Center_Call Center'[Call Timestamp])
)


Additional Columns for Enhanced Analysis:

Day Name: For weekly trend analysis

Day Number: Ensures correct chronological order of weekdays

Month & Year: For long-term trend tracking

🔗 Data Modeling

A One-to-Many (1:N) relationship was established:

Date Table [Date] → Call Center Data [Call Timestamp]

The Date Table acts as the primary filter for all time-based visuals across the dashboard.

3️⃣ Key Metrics Using DAX

Advanced DAX measures were created to calculate KPIs for operational insights:

-- Total Calls
Total Calls = COUNTROWS('Call Center_Call Center')

-- Total Call Duration (min)
Total Call Duration (min) = SUM('Call Center_Call Center'[Total Call Duration (min)])

-- Average Call Duration
Avg Call Duration (min) = DIVIDE([Total Call Duration (min)], [Total Calls], 0)

-- SLA Compliance %
Response time % = 
DIVIDE(
    CALCULATE(
        [Total Calls],
        'Call Center_Call Center'[Response Time] = "Within SLA" 
        || 'Call Center_Call Center'[Response Time] = "Above SLA"
    ),
    [Total Calls], 0
)

4️⃣ Dashboard Design & Visualization

The dashboard was designed for clarity and interactivity, enabling quick insights into Call Center performance.

Design Components:

🎯 KPI Cards: Summary of total calls, average duration, SLA compliance, etc.

📊 Call Distribution Charts: Interactive bar charts showing call volumes by:

Day of the week

Call reason

Channel (e.g., Chatbot, Call Center)

Location

😀 Sentiment Analysis: Visual representation of customer satisfaction

📋 Operational Grid: Detailed table with individual call records

🔍 Interactive Slicers: Filters by Date, City, and Channel for deeper exploration

5️⃣ Key Insights & Observations

💡 Most Common Reason: Billing inquiries are the top reason for calls

💡 Channel Usage: Chatbot and Call Center channels handle the majority of calls

💡 SLA Performance: About 75% of calls meet SLA targets

💡 Volume Trends: Call volume varies significantly by day of the week

6️⃣ Project Deliverables

All related files are included for review:

File Type	Description	Link
Power BI Report	Full interactive .pbix dashboard	Download

Dataset	Raw call center records (.csv)	View Data

Home Dashboard	High-level KPIs & overview	View Image

Grid Dashboard	Detailed operational table view	View Image