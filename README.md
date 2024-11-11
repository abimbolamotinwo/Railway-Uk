# Railway-Uk
A Python-based analysis of railway transaction data, focusing on popular travel routes, peak travel times, revenue breakdown by ticket types and classes, and on-time performance with delay factors. This repository provides insights into passenger behavior, revenue patterns, and operational efficiency.

## TABLE OF CONTENTS
-	[Project Overview](https://github.com/abimbolamotinwo/Railway-Uk?tab=readme-ov-file#project-overview)
- [Project Scope](https://github.com/abimbolamotinwo/Railway-Uk?tab=readme-ov-file#project-scope)
- [Project Objectives](https://github.com/abimbolamotinwo/Railway-Uk?tab=readme-ov-file#project-objectives)
- [Expected Outcome](https://github.com/abimbolamotinwo/Railway-Uk?tab=readme-ov-file#expected-outcome)
- [Document Purpose](https://github.com/abimbolamotinwo/Railway-Uk?tab=readme-ov-file#document-purpose)
- [Use Case](https://github.com/abimbolamotinwo/Railway-Uk/blob/main/README.md#use-case)
- [Data Source](https://github.com/abimbolamotinwo/Railway-Uk/blob/main/README.md#data-source)
- [Data Cleaning and Processing](https://github.com/abimbolamotinwo/Railway-Uk/blob/main/README.md#data-cleaning-and-processing)
- [Data Analysis](https://github.com/abimbolamotinwo/Railway-Uk/blob/main/README.md#data-analysis)
- [Recommendation]()
- [Conclusion]()
  
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

- ### Use Case
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

3. #### How does the revenue vary by ticket types and classes?
Analyzing revenue distribution across ticket types and classes enables a deeper understanding of the revenue model. By identifying which ticket types or classes bring in the most revenue, the company can focus marketing efforts on profitable segments, adjust pricing strategies, and explore options to increase sales in underperforming segments.
Columns Required: Price, Ticket Type, Class columns
Approach:
Firstly, aggregate ticket prices by ticket type and class to get total revenue per category using groupby function. The result was stored under the variable name ‘revenue_by_ticket’. Here’s the Python code:

```Python
revenue_by_ticket = railway.groupby(['Ticket Class', 'Ticket Type']).agg( Total_Revenue=('Price', 'sum'), Average_Price=('Price', 'mean') ).reset_index()
```

 Afterwards, visualize revenue distribution across ticket types and classes using line and clustered bar chart.
Steps:
**Clustered Bar Chart:** Plot the total revenue as clustered bars, where each Ticket Class has bars for each Ticket Type.
**Line Chart:** Overlay a line chart on top of the clustered bars for average price, using a secondary y-axis to accommodate the different scale.
Here’s the Python code:

```Python
fig, ax1 = plt.subplots(figsize=(12, 8))

# Plot the stacked bar chart for Total Revenue
revenue_by_ticket.set_index(['Ticket Class', 'Ticket Type']).unstack()['Total_Revenue'].plot(kind='bar', ax=ax1, width=0.5, alpha=0.7)

# Set the labels and title for the stacked bar chart
ax1.set_xlabel("Ticket Class and Type")
ax1.set_ylabel("Total Revenue")
ax1.set_title("Total Revenue and Average Price by Ticket Class and Type")

# Create a second y-axis for average price
ax2 = ax1.twinx()
ax2.plot(revenue_by_ticket['Ticket Type'], revenue_by_ticket['Average_Price'], color='blue', label="Average Price")
ax2.set_ylabel("Average Price", color='blue')
ax2.tick_params(axis='y', labelcolor='blue')

plt.show()
```

![](https://github.com/abimbolamotinwo/Railway-Uk/blob/main/Total%20Revenue%20and%20Average%20Price%20by%20Ticket%20Class%20and%20Type.png)

This analysis examines revenue generated by different combinations of ticket class and ticket type, summarizing both total and average prices for each category. Here’s a breakdown of the findings:
**First Class Tickets:**
- Advance tickets generated a total revenue of £66,886 with an average price of £37.92. Advance tickets are likely popular for passengers seeking lower prices while planning ahead.
- Anytime tickets contributed £37,841 in revenue, with a higher average price of £77.23, reflecting the premium pricing for flexibility in travel timing.
- Off-Peak tickets had a total revenue of £44,672 and an average price of £55.56, appealing to passengers traveling outside peak hours while still enjoying First Class amenities.
**Standard Class Tickets:**
- Advance tickets in Standard Class are the top revenue generator at £242,388, with a lower average price of £15.34, making them highly attractive to price-sensitive travelers.
- Anytime tickets brought in £171,468 with an average price of £35.35, providing flexibility in travel timing at a moderate price.
- Off-Peak tickets earned £178,666 in revenue, with an average price of £22.48, catering to travelers who prefer to avoid peak times while saving on fares.
- 
The revenue distribution suggests that Standard Class Advance tickets are the most popular choice, likely due to their affordability, while Anytime tickets across both classes command higher average prices due to their flexibility. 

4. #### What is the on-time performance? What are the main contributing factors?
Assessing on-time performance is crucial for improving customer satisfaction, as punctuality is a key quality metric in public transportation. Analyzing factors that contribute to delays can lead to operational improvements. For example, if certain routes consistently experience delays, adjustments in scheduling, better resource allocation, or even route changes could enhance performance reliability.
Columns Required: Journey Status, Reason for Delay.
Approach:
First, calculate on-time performance rate, this is calculated using value_counts(normalize=true), The result was stored under the variable name ‘ontime_performance’. Here’s the Python code:

```Python
ontime_performance=round(railway['Journey Status'].value_counts(normalize=True)*100, 2)
print('Ontime_performance in % is', ontime_performance[0])
```
This shows an output- **Ontime_performance in % is 86.82**

Afterwards, filter delayed journeys and analyze the main reasons for delay. The filtered delayed journeys will be stored under the variable name ‘delay’. Here’s the Python code for filtering delayed journeys:

```Python
delay=railway[railway['Journey Status']=='Delayed']
```
Analyse the main contributing factors to delay. The result was stored under the variable name ‘delayed_reasons’. This will be visualized using bar chart, here the Python code:

```Python
delayed_reasons=delay['Reason for Delay'].value_counts()

#visualize using bar chart

plt.figure(figsize=(10, 6))
delayed_reasons.plot(kind='bar', color='green')
plt.title('Frequency of Reasons for Delay')
plt.xlabel('Reason for Delay')
plt.ylabel('Counts')
plt.xticks(rotation=30)
plt.show()
```

![](https://github.com/abimbolamotinwo/Railway-Uk/blob/main/Frequency%20of%20Reasons%20for%20delay.png)

Lastly, identify patterns by analyzing delay reasons by Route and Hour. To analyze delay reason by route, group the data by “Route” and “Reason for Delay”, then count occurrences-Frequency. The result was stored under the variable name ‘route_delay_reasons’ and visualized with a HeatMap. Here’s the Python Code:

```Python
#create a column called ‘Route’ concatenating Departure Station and Arrival Destination
delay[‘Route]= delay['Departure Station'] + " - " + delay['Arrival Destination']

# Group by Route and Reason for Delay, and count occurrences
route_delay_reasons= delay.groupby([‘Route’, 'Reason for Delay']).size().reset_index(name='Frequency')

# Sort by Route and Frequency, descending to get the most frequent reasons on top for each route
route_delay_reasons= route_delay_reasons.sort_values(by=['Route', ‘Frequency’], ascending=[True, False])

# Optionally, get top 3 reasons per route
 top_delay_reasons_by_route = route_delay_reasons.groupby('Route').head(3).reset_index(drop=True)

# Pivot the data for visualization
pivot_data = route_delay_reasons.pivot(index='route', columns='Reason for Delay', values='Frequency').fillna(0)

# Plot heatmap
plt.figure(figsize=(12, 8))
sns.heatmap(pivot_data, cmap='viridis', annot=True, fmt=".0f", cbar_kws={'label': 'Frequency'})
plt.xlabel('Reason for Delay')
plt.ylabel('Route')
plt.title('Heatmap of Delay Reasons by Route')
plt.show()
```

![](https://github.com/abimbolamotinwo/Railway-Uk/blob/main/Delay%20reasons%20by%20Route.png)

To analyze delay reason by Hour, group the data by “Hour” and “Reason for Delay”, then count occurrences-Frequency and visualize using a stacked bar chart. Here’s the Python Code:

```Python
# Group by Hour and Reason for Delay and count occurrences
 hour_delay_reasons = df.groupby(['Hour', 'Reason for Delay']).size().reset_index(name='Count')

# Pivot data for stacked bar chart
 pivot_data = hour_delay_reasons.pivot(index='Hour', columns='Reason for Delay', values='Count').fillna(0) 

# Plot stacked bar chart pivot_data.plot(kind='bar', stacked=True, figsize=(12, 8), colormap='viridis') plt.xlabel('Hour of Day') plt.ylabel('Count of Delay Reasons') plt.title('Delay Reasons by Hour of Day') plt.legend(title='Reason for Delay', bbox_to_anchor=(1.05, 1), loc='upper left') plt.show()
```

![](https://github.com/abimbolamotinwo/Railway-Uk/blob/main/Delay%20reasons%20by%20Hours.png)

This analysis measures the punctuality of train arrivals, identifying patterns or factors that influence delays.  Here’s a breakdown of the findings:

**On-Time Performance:**
The on-time performance of the railway system is 86.82%, meaning that around 87% of the trains arrived at their scheduled time. This reflects a generally good performance but indicates room for improvement to reduce delays.

**Main Contributing Factors to Delays:**
The analysis of delay reasons reveals several key contributors:
1. Weather (758 delays):
- Weather conditions are the most frequent cause of delays. This includes factors like rain, snow, and extreme temperatures, which can impact infrastructure and train schedules.
2.	Technical Issues (472 delays):
- Problems with train mechanics or operational systems contribute significantly to delays. These might include engine failures, electrical issues, or faults in signaling systems.
3.	Signal Failure (451 delays):
- Failures in signaling systems, essential for controlling train movements, are a common source of delays. This issue can halt train movements, leading to significant delays, especially during peak hours.
4.	Staff Shortages (183 delays):
- Lack of adequate staffing, particularly in key operational roles, leads to delays. This could be due to absenteeism or insufficient workforce during critical periods.
5.	Staffing Issues (172 delays):
- Broader staffing-related challenges, such as scheduling problems or lack of available personnel, contribute to delays, particularly at busy times.
6.	Weather Conditions (169 delays):
- This is a specific category under weather-related issues, such as fog, high winds, or extreme heat, which can disrupt train schedules.
7.	Traffic (87 delays):
- Congestion and traffic on the tracks or at stations can contribute to delays, particularly at busy junctions or during peak travel times.
- 
**Main Routes with Delays:**
The routes experiencing the most delays are:
-	Liverpool Lime Street - London Euston (780 delays): A major route affected by weather-related disruptions and technical issues.
-	Manchester Piccadilly - Liverpool Lime Street (354 delays): Also affected by weather and technical problems.
-	London Euston - Birmingham New Street (242 delays): Signal failures and weather contribute to delays on this route.
-	
**Delay Reasons by Time of Day:**
- Morning hours (8 AM - 9 AM) experience the highest frequency of weather-related delays, particularly at 8 AM with 597 delays, suggesting that early commuters are most affected by weather conditions.
- Signal Failures are most frequent around 9 AM and 5 PM, aligning with peak travel hours when the system is under the most stress.
- Staffing-related delays appear to be concentrated in the late morning and early afternoon, especially around 11 AM and 3 PM.
- 
**Conclusions:**
- Weather-related issues are the primary cause of delays, especially during peak travel hours.
- Technical and signal failures are other significant contributors, highlighting the need for equipment upgrades and better maintenance.
- Staff shortages and staffing issues also impact on-time performance, particularly during key periods.

