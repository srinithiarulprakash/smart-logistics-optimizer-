Smart Logistics & Weather-Impact E-Commerce Optimizer

An end-to-end data engineering and business intelligence project demonstrating how to programmatically extract external weather data via a REST API, engineer supply chain risk features, and build an executive Power BI dashboard to evaluate retail revenue vulnerability and operational bottlenecks.

Project Overview

1. Situation
E-commerce and retail supply chains often operate under the blind assumption that weather has a negligible impact on delivery fulfillment. In reality, severe environmental conditions—such as heavy precipitation and storms—directly bottleneck logistics operations, leading to delivery delays, increased costs, and compromised customer satisfaction. However, internal transactional records rarely contain environmental context.

2. Task
The objective was to architect a production-grade data analytics pipeline that bridges this gap. This required programmatically connecting to a live meteorological web service, enriching historical retail transactions with exact weather metrics, engineering operational risk flags, and deploying an executive Power BI solution to visualize financial exposure and answer critical logistics questions.

3. Action
A rigorous, multi-stage engineering and analytical workflow was executed:
  * Automated Python ETL & REST API Integration:
  * Ingested raw transactional data (`online_retail.csv`) using `Pandas`.
  * Programmatically integrated the **Open-Meteo Historical Weather API** using Python's `Requests` library. Mapped transaction dates and geographic coordinates to dynamically query and fetch historical daily precipitation and weather metrics.
  * Advanced Data Cleaning & Feature Engineering:
  * Handled missing values, standardized data types, and merged the transactional dataset with the fetched API weather data.
  * Created a binary `Bad_Weather_Flag` derived from quantitative precipitation thresholds to distinguish normal operating days from high-risk weather conditions.
  * Dynamically generated a `Fulfillment_Status` logistics tier (On-Time, Minor Delay, Delayed) to isolate supply chain bottlenecks.
  * Exported the final processed asset as `enriched_retail_weather_data.csv`.
  * Data Modeling & Custom DAX Implementation:
  * Built a relational data model in Power BI, ensuring clean formatting and optimal data types.
  * Wrote custom DAX measures (`SUM`, `DIVIDE`, `CALCULATE`) to calculate core metrics:
    ```dax
    Total Revenue = SUM('enriched_retail_weather_data'[TotalSales])
    
    High Risk Order % = 
    DIVIDE(
        CALCULATE(COUNT('enriched_retail_weather_data'[InvoiceNo]), 'enriched_retail_weather_data'[Bad_Weather_Flag] = "High Risk"),
        COUNT('enriched_retail_weather_data'[InvoiceNo]),
        0
    )
    
    Average Order Value = AVERAGE('enriched_retail_weather_data'[TotalSales])
    ```
  * Executive Dashboard Architecture:** Designed a 3-tier visual hierarchy:
  * Top Row: Executive KPI cards showcasing Total Revenue, Average Order Value (AOV), and High-Risk Weather Exposure %.
  * Middle Row: Daily Revenue Trend line chart mapping sales fluctuations against weather anomalies over time.
  * Bottom Row: Split-column operational layout featuring a clustered column chart tracking revenue loss across fulfillment delay tiers, paired with a geographic breakdown and weather risk distribution donut chart.

4. Result & Strategic Business Insights
This project transformed raw, multi-source records into an operational intelligence tool that answers critical supply chain questions:

* What did we find out?
  * Quantified Weather Vulnerability: Pinpointed the exact percentage of total orders processed under "High Risk" weather conditions and calculated the exact revenue tied up in delayed fulfillment tiers.
  * Bottleneck Identification: Correlated specific precipitation spikes with delivery slowdowns, revealing which orders face minor vs. severe delays based on environmental conditions.
  * Geographic & Temporal Trends: Unearthed which regions and time periods suffer the steepest revenue dips during adverse weather events.
* What decisions can be made using these findings?
  * Proactive Inventory & Logistics Routing: Operations teams can use weather forecasts to reroute shipments or adjust carrier capacity before severe storms hit high-risk zones.
  * Dynamic Customer Communication: E-commerce platforms can automatically update estimated delivery dates (EDDs) for customers when a "High Risk" weather flag is triggered, reducing customer support tickets and churn.
  * Risk-Mitigated Resource Allocation: Management can optimize fulfillment center staffing and inventory buffers based on historical weather correlation data rather than reacting after delays occur.

---

Tech Stack & Skills Demonstrated
* Languages & Data Processing: Python, Pandas, Google Colab
* APIs & Data Engineering: RESTful APIs, Open-Meteo Historical Weather API, Automated ETL, Data Merging & Transformation
* Business Intelligence & Modeling: Power BI, Power Query, Relational Data Modeling
* Data Analysis & DAX: Custom measures (`CALCULATE`, `DIVIDE`, `SUM`), Time-Series Analysis, Operational KPI Tracking

---

Dashboard Architecture
* KPI Summary Layer: `Total Revenue`, `Average Order Value`, `High-Risk Weather Exposure %`
* Time-Series Analysis: Daily revenue fluctuations mapped against weather shifts.
* Operational Bottlenecks: Revenue loss per fulfillment tier (*On-Time* vs. *Delayed*), country-level performance, and risk distribution.


