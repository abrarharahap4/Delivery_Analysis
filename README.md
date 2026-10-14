# Delivery_Analysis
## Data-Driven Analysis of the Impact of Weather & Traffic Conditions on Food Delivery Time

### 📊 Interactive Dashboard
<img width="737" height="692" alt="image" src="https://github.com/user-attachments/assets/9fbda181-1c92-4b8e-9558-b8d5f42ac60b" />


### 📁 Repository
- [Cleaned Dataset](./Dataset_Uber_Eats_(Clean).csv)
- [Statistical Summary (Kruskal-Wallis & Effect Size)](./Dataset_Statistical_Summary_THT.csv)
- [Analysis Notebook](./Ghairandi_Al_Abrar_Delivery_Analysis_Notebook.ipynb)
- [Power BI Dashboard](./Dashboard_Delivery_Analysis.pbix)
- [Presentation Slides (pdf)](./Ghairandi_Al_Abrar_Presentation_Delivery_Analysis.pdf)
  

### 🎯 Business Problems & Project Goals
#### Business Problems
Delivery time is one of the main drivers of customer satisfaction in food delivery. The ETA shown to customers is usually static and does not adapt to field conditions such as weather and traffic. Both factors are often assumed to be major drivers of delay, but that assumption has not been tested with data, and the size of their impact has never been quantified. As a result, orders delayed by bad weather and heavy traffic are still judged as "late", which raises the risk of complaints and compensation costs.

Using 1,000 delivery records with weather, traffic, vehicle type, time of day, distance, preparation time, and courier experience, this project tests statistically which operational factors actually affect delivery time and how large their contribution is, as a basis for a more realistic ETA.

#### Project Goals
- Identify which operational factors (weather, traffic, vehicle type, time of day) have a statistically significant effect on delivery time.
- Quantify how large each factor's effect is compared to distance and preparation time.
- Measure the impact of combined bad conditions (e.g. high traffic + rain) to support proportional time buffers and a more adaptive ETA.
  

### 🧩 Features & Visualization
#### Key Features
- **Total Order** => Total number of delivery orders analyzed
- **Average Distance (km)** => The average delivery distance per order
- **Average Delivery Time (min)** => The average time from order to delivery
- **Median of Delivery Time (min)** => The median delivery time, less affected by extreme slow orders

#### Visualization
- **Average of Delivery Time by Traffic Level** => Clustered bar chart
- **Effect Size by Factors** => Clustered bar chart
- **Delivery Time vs Distance** => Scatter chart
- **Delivery Time by Traffic Level x Weather Condition** => Pivot table
- **Summary of H-statistic, Epsilon-squared, and % Variance Explained** => Table
- **Weather, Traffic Level, Vehicle Type, and Time of Day Filter** => Slicer


### Key Insights
- Distance is by far the dominant driver of delivery time: distance has a strong positive correlation with delivery time (r = 0.78, explaining ~61% of the variation), followed by preparation time (r = 0.31, moderate) while courier experience is practically irrelevant (r = −0.09). The average delivery time is 56.7 minutes (median 55.5), with 50% of orders delivered within 41–71 minutes.
- Weather and traffic are statistically significant, but individually small: Kruskal-Wallis confirms a significant effect for Weather (H = 37.05) and Traffic Level (H = 37.07), both p < 0.00001, with small effect sizes (ε² = 0.033 and 0.035, i.e. ~3.3% and ~3.5%). Vehicle type (p = 0.611) and time of day (p = 0.816) show no significant effect. Weather and traffic act as modifiers on a distance-based estimate, not as the main drivers.
- Bad conditions compound each other: High traffic + Rainy orders take 77 minutes on average, 54% slower than the best condition (Low traffic + Clear, 49.9 minutes). Rainy only spikes under heavy traffic (55 → 77 minutes), while Snowy is consistently heavy at every traffic level (68.2 minutes on average). A simple multiplier model misses the real value by 2.59 minutes on average and by up to +8.7 minutes for High + Rainy, so the combined effect must be treated as its own pattern, not as a sum of two separate factors.
- Suggestion, delivery estimates should be made adaptive: Use distance as the base of the ETA and apply a lookup table of historical delivery times per Traffic × Weather combination, with a consistent buffer for Snowy at any traffic level and a specific buffer for Rainy under High traffic. Stop spending optimization effort on vehicle type and time of day, since neither shows an effect. The dataset has no historical ETA data, so the expectation gap cannot be measured directly yet; the company should start logging the ETA shown to customers versus the actual delivery time to validate the adjustment.


### 🗂️ Data Source
The dataset used in this project (Dataset_Uber Eats.csv, 1,000 delivery records, 9 columns) can be downloaded through the link =>
https://www.kaggle.com/datasets/denkuznetz/food-delivery-time-prediction
