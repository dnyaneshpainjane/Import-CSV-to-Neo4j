## Import CSV to Neo4J and applying cypher Query to extract required data

#### About Dataset:
This dataset shows the Monthly Passenger Traffic Statistics by Airline at San Francisco International Airport. Because airport data is seasonal, any comparisons should be made on a period-over-period basis (i.e. January 2010 vs. January 2009), rather than period-to-period (i.e. January 2010 vs. February 2010). It's also worth noting that the correlations between fact and attribute fields aren't necessarily 1:1. For example, United Airlines Passenger Counts will appear in several attribute variables and are additive, giving the user the ability to generate categorized Passenger Counts as needed.

### Follwing is step-by-step guide 
1.how to load CSV data to Neo4j 

2.How to create node 

3.How to extract perticular filtered data from Neo4j

### Connect to Neo4j server: 
![image](https://user-images.githubusercontent.com/81969659/156782489-34af3354-6767-4947-a729-56fc86e29824.png)
### Create database with name “scit”:
 ![image](https://user-images.githubusercontent.com/81969659/156782554-d102244f-1ce1-42a5-b13b-9b9b95f231e2.png)
### Using scit database:
 ![image](https://user-images.githubusercontent.com/81969659/156782774-8851385b-ec43-4806-b969-311caba9b3a9.png)

### Importing data and saving in node:
WITH "https://bit.ly/3Iyl4b6"AS uri
LOAD CSV WITH HEADERS FROM uri AS line
CREATE (data1:Data1{airline_name:line.Operating_Airline,IATA_code:line.Operating_Airline_IATA_Code,
        geo_region:line.GEO_Region,geo_summary:line.GEO_Summary,
        month:line.Month,year:toInteger(line.Year),
        activity_type:line.Activity_Type,activity_period:line.Activity_Period,
        price_category:line.Price_Category,passenger_count:toInteger(line.Passenger_Count),
        boarding_area:line.Boarding_Area})
        
 ![image](https://user-images.githubusercontent.com/81969659/156782814-92874fd7-48fa-4980-a23d-e516def356eb.png)

### Descriptive Statistics:
MATCH (n) 
RETURN
DISTINCT labels(n),
count(*) AS SampleSize,
avg(size(keys(n))) as Avg_PropertyCount,
min(size(keys(n))) as Min_PropertyCount,
max(size(keys(n))) as Max_PropertyCount,


 ![image](https://user-images.githubusercontent.com/81969659/156782837-9dca58f5-7f45-40a9-8831-5a189e0a562f.png)

### Question:
#### show the GEO region of domestic flights having passanger count > 100000 in december month?
Ans:
MATCH (filter_data:Air_Traffic_Data)
WHERE filter_data.geo_summary="Domestic" AND filter_data.month="December" 
AND filter_data.passenger_count>=100000
RETURN filter_data

 ![image](https://user-images.githubusercontent.com/81969659/156782944-b426787c-f746-40a3-8e25-262b0fba36fc.png)

 


