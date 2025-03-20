SF Trees: Analyzing urban tree data for community improvement

- Overview

This project explores and analyzes San Francisco's urban tree data to identify trends, improve city planning, and support environmental efforts. By leveraging machine learning models and statistical techniques, we aim to understand tree planting trends, predict future growth, and analyze tree species distribution and care patterns.

- Dataset

Street tree: https://data.sfgov.org/City-Infrastructure/Street-Tree-List/tkzw-k3nq/about_data

Neighborhood: https://data.sfgov.org/Geographic-Locations-and-Boundaries/Analysis-Neighborhoods/j2bu-swwd/about_data

The primary dataset used in this analysis is SF_Street_Tree_List.csv, which contains information on urban trees in San Francisco. Key columns include:

	PlantDate: The date a tree was planted.
	DBH: Diameter at Breast Height (inches), indicating tree size.
	qSpecies: The species of the tree.
	qCaretaker: Entity responsible for tree maintenance.
	Latitude and Longitude: Geographic coordinates of trees.
	Neighborhoods (old): The neighborhood the tree is located in.

A secondary dataset, Neighborhood.csv, is used to map trees to their respective neighborhoods. This dataset contains:

	neighborho: The name of the neighborhood.
	Neighborhood_Code: A unique identifier assigned to each neighborhood.


- Data Cleaning and Preprocessing:

	Handling Missing Values: Missing numerical values (DBH, Latitude, Longitude) are filled using the median.


- Filtering Outliers:

	Removed trees with unrealistic DBH values (>100 inches or DBH = 9999).
	Applied an Interquartile Range (IQR) method with adjusted thresholds to filter extreme values.


- Feature Engineering:

	Extracted PlantYear from PlantDate.
	Calculated TreeAgeYears by computing the difference between PlantDate and the current date.


- Encoding Categorical Variables:

	One-hot encoding applied to qSpecies and qCaretaker.


- Scaling Numerical Features:

	Used StandardScaler to normalize DBH, TreeAgeYears, Latitude, and Longitude.


- Neighborhood Mapping:

	Used Neighborhood.csv to map trees to their corresponding neighborhoods using Neighborhood_Code.
	Ensured all neighborhoods were properly assigned and duplicates were removed.


- Exploratory Data Analysis:

	Tree Species Distribution: A bar plot visualizing the top 10 most common tree species in San Francisco.
	Tree Age vs. DBH Scatterplot: Examines tree growth trends over time.
	Tree Planting Trends: Analyzes tree planting trends over the years.
	Tree Caretaker Distribution: Shows the number of trees managed by different caretaker entities.
	Tree Density by Neighborhood: A bar chart depicting tree distribution across neighborhoods.

- Clustering Analysis

	Applied K-Means Clustering (k=5) on latitude and longitude to group trees by geographic regions.
	Visualized tree location clusters using a scatterplot.
	Cluster plot looks pretty accurate compared to the actual map.
	

- Predictive Modeling

To predict future tree planting rates, I implemented three models:

	Polynomial Regression
	Exponential Smoothing 
	LSTM Neural Network (Deep Learning) - had to choose 3 years instead of 10 because 
										  of overfitted data. 


- Training Process:

	Data was split into training (80%) and testing (20%) sets.
	The models were trained and tested using historical planting data.
	Forecasted planting rates for the next 10 years.


Results Visualization:

A line plot comparing historical planting trends with future predictions from all three models.
LSTM performed the best of all since it gave most relevant looking prediction.

 Future Tree Planting Predictions:
   Year  Polynomial Regression  Exponential Smoothing  LSTM (Neural Network)
0  2015             -45.350662              11.975701              18.843023
1  2016             -52.852989              12.041754              31.829594
2  2017             -60.867776              12.103973              34.010929
3  2018             -69.409718              12.162579              29.492290
4  2019             -78.493532              12.217783              32.962910
5  2020             -88.133957              12.269782              36.655102
6  2021             -98.345752              12.318762              31.549603
7  2022            -109.143697              12.364898              30.387236
8  2023            -120.542594              12.408356              35.930210
9  2024            -132.557266              12.449291              34.516663

Key Findings

Tree planting rates have fluctuated over time, with a noticeable decline in recent years.
Certain neighborhoods have significantly fewer trees, indicating potential areas for urban greening initiatives.
Larger trees (higher DBH) tend to be older, but there are variations based on species and location.
City-maintained trees make up a large portion of the dataset, but community caretakers also play a vital role.
Future tree planting trends suggest a potential decline, emphasizing the need for policy intervention.