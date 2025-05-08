# Predictive Analysis of Transit Reliability - Massachusetts Bay Transportation Authority (MBTA)

![MBTA Logo](MBTA.png)

## Overview

This project employs data mining techniques to examine the reliability of the Massachusetts Bay Transportation Authority (MBTA) public transit services[cite: 1, 3]. The primary focus is on identifying patterns that influence service punctuality and consistency, and building predictive models to forecast service reliability[cite: 3]. The analysis aims to provide actionable insights for the MBTA to optimize operations and enhance passenger experience[cite: 10, 85].

## Dataset

The analysis utilizes a comprehensive dataset provided by the Massachusetts Department of Transportation (MassDOT) detailing MBTA service performance[cite: 102].

* **Source:** [MBTA Bus, Commuter Rail, & Rapid Transit Reliability - MassDOT Open Data](https://mbta-massdot.opendata.arcgis.com/datasets/MassDOT::mbta-bus-commuter-rail-ra%0Apid-transit-reliability/about) [cite: 102]
* **Size:** Over 850,000 records[cite: 4, 22].
* **Features:** Includes details like service dates, routes (GTFS IDs, short/long names, descriptions), route categories, mode type (Bus, Rail, Commuter Rail), peak/off-peak indicator, performance metrics (OTP numerator/denominator, cancelled numerator), etc[cite: 4].

## Methodology

The project follows a standard data mining workflow:

1.  **Data Preprocessing:**
    * Handling missing values (e.g., imputing `otp_rate` using the mean)[cite: 5, 27].
    * Feature Engineering: Creating new features like `otp_rate` (On-Time Performance rate)[cite: 26, 28], `service_day`[cite: 29, 32], `peak_encoded` (binary peak indicator)[cite: 30, 31, 32], and the target variable `otp_label` (categorizing OTP rate as 'high' or 'low' based on the median)[cite: 36].
    * Dropping irrelevant or high-cardinality features (like `service_date`, `gtfs_route_id`)[cite: 33].
    * Encoding categorical variables using one-hot encoding for model compatibility[cite: 34, 35].
2.  **Exploratory Data Analysis (EDA):** Visualizations were used to understand data distributions and relationships (e.g., OTP rate distribution, average OTP by route category, transport mode frequency).
3.  **Model Building & Evaluation:**
    * The data was split into training, validation, and test sets.
    * Multiple classification models were applied, including:
        * **Logistic Regression:** Used for baseline prediction and interpretability[cite: 4, 23, 50, 51]. Feature selection (L1) and hyperparameter tuning (GridSearchCV) were performed.
        * **Random Forest:** An ensemble method reported in the abstract to provide robust performance[cite: 4, 6, 23, 46]. Hyperparameter tuning (GridSearchCV) was performed.
        * (The report also mentions Decision Trees and XGBoost were applied [cite: 4, 23, 44, 56]).
    * Models were evaluated using metrics like Accuracy, ROC-AUC, Precision-Recall AUC, Classification Reports, and Confusion Matrices.

## Key Findings

* **Model Performance:** The analysis reported in the project abstract indicated that the optimized Random Forest model demonstrated superior performance, achieving **98.5% accuracy** and a **ROC-AUC score of 0.99**[cite: 6]. The precision-recall curve AUC was also high at 0.98[cite: 7]. *(Note: Detailed notebook evaluations showed different performance metrics)*.
* **Key Reliability Factors:** The analysis consistently identified the following as critical factors influencing service reliability:
    * **Peak vs. Off-Peak Indicator (`peak_offpeak_ind`):** Services during peak hours are significantly more likely to experience delays[cite: 8, 69, 70].
    * **OTP Numerator (`otp_numerator`):** Past on-time performance metrics are predictive of future performance[cite: 8].
    * **Route Category:** The type of route (e.g., Key Bus, Express Bus) has a substantial impact on reliability[cite: 8, 73, 74].
    * **Service Day:** The day of the week influences performance patterns[cite: 71, 72].

## Recommendations for MBTA

Based on the data-driven insights, the following strategic enhancements are recommended[cite: 9, 86]:

1.  **Strategic Resource Allocation:** Focus additional resources (vehicles, staff) during identified peak periods and specific weekdays to mitigate common delays[cite: 76, 77].
2.  **Route Optimization:** Conduct thorough reviews and optimize schedules, frequencies, or alignments for route categories consistently showing lower reliability (e.g., Key Bus, Express Bus)[cite: 78, 79].
3.  **Data-Driven Scheduling:** Explore implementing more dynamic scheduling systems that can adapt based on collected performance data[cite: 80].
4.  **Continued Monitoring & Model Refinement:** Continuously monitor service performance and update predictive models with new data[cite: 81, 82], potentially incorporating external factors like weather or real-time traffic for improved accuracy[cite: 11, 83, 84].

## Files in Repository

* `Code.ipynb`: Jupyter Notebook containing the Python code for data analysis, model building, and evaluation.
* `Analysis_Report.pdf`: The detailed PDF report summarizing the project findings and methodology.
* `MBTA.png`: MBTA logo image file.
* `README.md`: This file, providing an overview of the project.

## How to Use

1.  **Review the Analysis:** Read the `Analysis_Report.pdf` for a detailed summary of the project.
2.  **Explore the Code:** Open `Code.ipynb` in a Jupyter environment (like Jupyter Lab, Jupyter Notebook, Google Colab, or VS Code with Python extensions) to see the implementation details.
3.  **Run the Code (Optional):** To run the notebook, you'll need the `mbta.csv` dataset (ensure the file path in the notebook matches its location) and the necessary Python libraries installed (see Dependencies). The dataset can be obtained from the MassDOT Open Data portal[cite: 102].

## Dependencies 

* pandas
* numpy
* scikit-learn (sklearn)
* matplotlib
* seaborn
* ipython (for display functions)

## Authors 

* Sai Sudheer Naraharisetty 
