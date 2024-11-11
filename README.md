# Railway-Uk
A Python-based analysis of railway transaction data, focusing on popular travel routes, peak travel times, revenue breakdown by ticket types and classes, and on-time performance with delay factors. This repository provides insights into passenger behavior, revenue patterns, and operational efficiency.

## TABLE OF CONTENTS
-	Project Overview
- Project Scope
- Project Objectives
- Expected Outcome
- Document Purpose
- Use Case
- Data Source
- Data Cleaning and Processing
- Data Analysis
- Recommendation
- Conclusion
  
## Project Overview
This project leverages Python to analyze UK National Rail ticket data from January to April 2024, focusing on key aspects such as travel routes, times, ticket types, and journey punctuality. The analysis aims to uncover actionable insights into passenger behavior, peak travel patterns, revenue distribution, and performance reliability. These insights are intended to enhance service efficiency and improve customer satisfaction.

## Project Scope
This analysis focuses on a selected dataset, covering ticket purchases and journeys taken between January and April 2024. The data includes ticket types, classes, journey times, departure and arrival stations, and pricing details. Key performance indicators such as popular routes, peak travel times, revenue variation, and on-time performance will be examined. Assumptions and limitations, such as seasonal data coverage or incomplete delay reasons, will also be clarified.

## Project Objectives
The primary objectives are to:
- Identify the most popular routes and busiest stations.
- Determine peak travel times to understand demand patterns.
- Analyze revenue distribution across different ticket types and classes.
- Assess on-time performance and identify common causes of delays.
- 
## Expected Outcome
Expected outcomes include clear insights into the most frequented routes, peak demand times, and the revenue breakdown by ticket type and class. Additionally, the on-time performance analysis aims to pinpoint the main causes of delays, ultimately supporting recommendations for operational improvements in route scheduling, ticket offerings, and customer satisfaction.

## Document Purpose
This document serves as a structured report summarizing the analysis process, methodologies, and key findings from the data. It is designed to communicate insights and support data-driven decision-making for enhancing service efficiency and revenue management within National Rail.
Use Case
The insights from this analysis offer valuable applications across various functional areas within National Rail:
- Operations Management: By identifying peak travel routes and times, operations teams can adjust schedules, optimize train frequency, and allocate resources effectively. This can help reduce overcrowding, enhance service reliability, and improve customer experience during high-demand periods.
- Revenue Management and Pricing Strategy: Insights into ticket type and class preferences enable revenue management to design targeted pricing models and promotional offers. These strategies can enhance revenue generation by aligning ticket offerings with customer demand patterns and seasonal travel behaviors.
- Customer Experience and Marketing: Customer service and marketing teams can leverage findings on popular routes and travel preferences to enhance communication, tailor promotions, and improve service delivery. By addressing identified delay causes, these teams can work to minimize disruptions and promote consistent on-time performance, reinforcing brand trust.
- Strategic Planning and Policy Development: For strategic planners and policy makers, the analysis provides data-backed insights into long-term travel trends and infrastructure needs. This aids in setting priorities for capacity expansion, station upgrades, and other service enhancements aligned with growing demand.
- Regulatory and Compliance Teams: Insights into on-time performance and delay factors support compliance with regulatory standards for service punctuality, helping ensure that National Rail meets or exceeds performance expectations and maintains a high level of service accountability.
Through this use case, stakeholders from various departments can align their strategies to improve National Rail's operational efficiency, customer satisfaction, and overall market competitiveness.

- ## Data Source
The dataset for this analysis was sourced from [Maven Analytics](https://mavenanalytics.io/data-playground?page=2&pageSize=5) website, an educational platform offering curated datasets for data professionals. Specifically, this dataset simulates UK National Rail transactions from January to April 2024, including information on journey dates, ticket classes, ticket types, station locations, times, prices, and journey statuses. The data offers a comprehensive snapshot of travel patterns, ticket preferences, and operational performance for this period.

- ## Data Cleaning and Processing
The dataset was initially well-constructed, with thorough checks confirming the absence of null values and duplicates. However, several transformations were needed to prepare the data for analysis:
1.	Date and Time Columns: The date and time columns—"Date of Purchase”, “Time of Purchase”, “Date of Journey”, “Departure Time”, “Arrival Time”, and “Actual Arrival Time”—were initially stored as object data types. To enable accurate date and time calculations, these columns were converted to the datetime64 data type. 
 The columns were converted from object datatype to datetime64 with this Python code:

```Python
railway['Date of Purchase'] = pd.to_datetime(railway['Date of Purchase'])
railway['Date of Journey'] = pd.to_datetime(railway['Date of Journey'])
railway['Time of Purchase'] = pd.to_datetime(railway['Time of Purchase'], format='%H:%M:%S')
railway['Departure Time'] = pd.to_datetime(railway['Departure Time'], format='%H:%M:%S')
railway['Arrival Time'] = pd.to_datetime(railway['Arrival Time'], format='%H:%M:%S')
railway['Actual Arrival Time'] = pd.to_datetime(railway['Actual Arrival Time'], format='%H:%M:%S')
```

2. Text Standardization: The “Reason for Delay” column contained text in inconsistent cases (uppercase, lowercase, mixed). This was standardized to proper case (capitalizing the first letter of each word) using a proper case function, ensuring consistency in the data. Here’s the Python code:

```Python
railway['Reason for Delay']=railway['Reason for Delay'].str.title()
```

3.	New Columns: Two additional columns were created to support time-based analysis:
- Hour of Departure: Extracted the hour from the “Departure Time” column to identify peak travel hours.
- Day of the Week: Derived the day of the week from the “Date of Journey” column to analyze travel patterns by weekday.
Here’s the Python code from creating column “Hour” and “Weekdays”:

 ```Python
railway['Reason for Delay']=railway['Reason for Delay'].str.title()
```

These cleaning steps ensured that the data was properly formatted, enriched with new columns, and allows for more efficient handling of temporal data enabling more detailed and accurate analysis of travel patterns and delays.

- ## Data Analysis
The aim of this analysis is to comprehensively examine UK National Rail ticketing and journey data to uncover patterns, optimize operations, and improve overall service quality and profitability. By analyzing travel demand, revenue trends, and punctuality metrics, this study seeks to understand core travel behaviors, identify high-demand routes, and assess the effectiveness of various ticket types and classes.

A primary goal is to enhance the efficiency of National Rail services by identifying when and where peak demand occurs, allowing the organization to adjust service schedules and capacity. Furthermore, analyzing revenue across ticket types and classes offers insights into customer preferences and potential areas for pricing or marketing adjustments, helping maximize revenue while maintaining a competitive service offering.

On-time performance is another essential component, as it directly influences customer satisfaction and operational reputation. By examining punctuality and delay patterns, we can pinpoint recurring issues and contributing factors, enabling targeted improvements that ensure better service reliability.

This analysis ultimately provides National Rail with data-driven insights that can inform strategic planning, from operational adjustments to targeted marketing campaigns, ensuring a better experience for passengers and a more optimized revenue model for the organization. Through systematic exploration of travel trends, revenue generation, and service performance, this study aims to support National Rail in delivering a reliable, efficient, and financially sustainable rail service.
To provide insights into this analysis, the following questions will be addressed:

1. #### What are the most popular routes?
The purpose of this analysis is to understand the most frequently traveled routes as it helps in resource allocation, such as adjusting the frequency of trains or adding capacity on high-demand routes. It also allows identification of key travel corridors, which can inform strategic decisions around infrastructure investments or targeted marketing campaigns to increase ticket sales on less popular routes.
To achieve this, columns required is “Departure station”, “Arrival Destination”, and frequency count- this counts occurrence of each unique pair to determine the frequency of each route.
Firstly, start by grouping the data based on the “Departure Station” and “Arrival Destination” columns and count occurrences (Frequency), it was stored with a variable name ‘routecounts’. 
 Here’s the Python code:

```Python
routecounts=railway.groupby(['Departure Station', 'Arrival Destination']).size().reset_index(name=’Frequency’)
```
Afterwards, sort the routes by Frequency in descending order for easier analysis, then select top 10 by Frequency, it was stored with a variable name ‘top_routes’. The result was visualized using a bar chart, here’s the Python code:

```Python
top_routes=routecounts.sort_values(‘Frequency', ascending=False).head(10)

# Visualize with a bar chart
plt.figure(figsize=(10, 6))
sns.barplot(x='Frequency', y=top_routes['Departure Station'] + " - " + top_routes['Arrival Destination'], data=top_routes, palette="viridis")
plt.xlabel('Frequency')
plt.ylabel('Route (Departure - Arrival)')
plt.title('Top 10 Most Popular Routes')
plt.xticks(rotation=45)
plt.show()

```
![](https://github.com/abimbolamotinwo/Railway-Uk/blob/main/Top10%20popular%20route.png)

The above analysis shows that the top 10 popular routes are:
- Manchester Piccadilly to Liverpool Lime Street with frequency counts of 4628
- London Euston to Birmingham New Street with frequency counts of 4209
- London Kings Cross to York with frequency counts of 3922
- London Paddington to Reading with frequency counts of 3873
- London St Pancras to Birmingham New Street with frequency counts of 3471
- Liverpool Lime Street	 to Manchester Piccadilly with frequency counts of 3002
- Liverpool Lime Street to London Euston with frequency counts of 1097
- London Euston to Manchester Piccadilly with frequency counts of	712
- Birmingham New Street to London St Pancras with frequency counts of 702
- London Paddington to Oxford with frequency counts of 485

2. #### What are the Peak Travel Times?
The aim of this analysis is to identify peak travel times as it helps in planning and optimizing service schedules, which can enhance passenger experience by reducing overcrowding during high-demand hours. Insights into daily and weekly travel patterns also allow for better workforce management and help in aligning services with customer needs, potentially improving operational efficiency.
Columns Required: Departure Time and Date of Journey columns
Approach:
 Firstly, extract hour from “Departure Time” column, group by hour and count occurrences using value_counts(), then select top 5. The result was stored with a variable name ‘peak_travel_hours’ and visualized with a bar chart. Here’s the Python code:

 ```Python
peak_travel_hours=railway['Hours'].value_counts().head()

# Visualize using bar chart
plt.figure(figsize=(10, 6))
peak_travel_hours.plot(kind='bar', color='skyblue')
plt.title('Top 5 Peak Travel Hours')
plt.xlabel('Hour of Departure')
plt.ylabel('Number of Departures')
plt.show()
```
![](https://github.com/abimbolamotinwo/Railway-Uk/blob/main/Peak%20Travel%20hour.png)

Afterwards, extract weekdays from “Date of Journey” column, group by weekdays and count occurrences using value_counts(), then select top 5. The result was stored with a variable name ‘peak_travel_days’ and visualized with a bar chart. Here’s the Python code:

```Python
peak_travel_days=railway['Weekdays'].value_counts().head()

#Visualize using bar chart
plt.figure(figsize=(10, 6))
peak_travel_days.plot(kind='bar', color='salmon')
plt.title('Top 5 Peak Travel Days')
plt.xlabel('Day of the Week')
plt.ylabel('Number of Journeys')
plt.show()
```
![](https://github.com/abimbolamotinwo/Railway-Uk/blob/main/Peak%20Travel%20days.png)

The Peak travel hour analysis shows that:
-	18:00 (6 PM) has the highest number of departures, with 3,113 trips, suggesting this is a peak time for travel, likely due to workers leaving their jobs at the end of the typical workday.
-	06:00 (6 AM) follows closely with 3,112 trips, suggesting this time is popular among early commuters heading to work.
-	17:00 (5 PM) is another busy hour, with 2,888 departures, aligning with people finishing work or heading to evening activities.
-	07:00 (7 AM) sees 2,795 departures, supporting the start times for work and school, as commuters aim to arrive by 8 or 9 AM.
-	16:00 (4 PM) has 2,301 trips, which may reflect travel by students finishing school or individuals with earlier work schedules.

The Peak travel weekday analysis shows that:
- Wednesday (4,692 trips) has the highest number of journeys, possibly due to regular midweek commuting for work or business.
- Tuesday (4,607 trips) is also a popular travel day, likely driven by business travel schedules. Many professionals prefer traveling on Tuesday to avoid the busier start-of-week traffic on Monday.
- Thursday (4,580 trips) and Sunday (4,580 trips) show similar travel volumes. Thursday may be popular for people traveling to wrap up their business week, while Sunday likely sees an increase due to leisure travel and people returning from weekend activities.
- Monday (4,436 trips) has a slightly lower count, likely influenced by commuters heading to work and people traveling back from weekend trips.


