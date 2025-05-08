#  Predictive Analysis of Transit Reliability - Massachusetts Bay Transportation Authority (MBTA) 🚦

![MBTA Logo](MBTA.png)

## 📝 Overview

Public transportation is vital for urban mobility, impacting daily commutes, economic activity, and environmental sustainability. In cities like Boston, the efficiency and reliability of services managed by the Massachusetts Bay Transportation Authority (MBTA) are crucial for residents and visitors alike. Consistent, on-time service enhances quality of life and supports the local economy.

This project dives deep into MBTA's operational data, employing data mining techniques to:
* Examine the factors influencing service reliability (punctuality and consistency). 📈
* Identify key patterns related to delays and disruptions.
* Build and evaluate predictive models to forecast service reliability. ⚙️
* Provide data-driven, actionable insights for potential service optimization. 💡

The goal is to leverage historical data to understand the complexities of transit operations and support the MBTA in making informed decisions to improve service for its passengers.

## 📊 Dataset

The analysis is powered by a large, publicly available dataset detailing MBTA service performance:

* **Source:** Massachusetts Department of Transportation (MassDOT) - MBTA Bus, Commuter Rail, & Rapid Transit Reliability Dataset. ([Link to Open Data Source](https://mbta-massdot.opendata.arcgis.com/datasets/MassDOT::mbta-bus-commuter-rail-rapid-transit-reliability/about))
* **Volume:** Contains over 850,000 individual records, providing a rich foundation for analysis.
* **Content:** Each record details specific service runs, including:
    * Service dates and times
    * Route information (GTFS IDs, descriptions)
    * Mode of transport (Bus, Rail, Commuter Rail)
    * Route categories (e.g., Key Bus, Other Bus, specific train lines)
    * Peak / Off-Peak service indicators
    * Performance metrics like OTP (On-Time Performance) numerators and denominators, and cancellation data.

## 🛠️ Methodology

The project employed a systematic data mining approach:

1.  **Data Preprocessing & Cleaning:**
    * **Handling Missing Values:** Identified and addressed missing data points, notably imputing the mean for missing `otp_rate` values to ensure data integrity.
    * **Feature Engineering:** Derived meaningful features from raw data:
        * Calculated `otp_rate` (OTP Numerator / OTP Denominator).
        * Extracted temporal features like `service_day` (day of the week), month, day, and time from the service date.
        * Created a binary `peak_encoded` feature (1 for PEAK, 0 for OFF_PEAK).
        * Developed the primary target variable `otp_label` by categorizing `otp_rate` into 'high' or 'low' based on the median performance, creating a balanced classification task.
    * **Feature Selection:** Dropped columns with excessive unique values or those deemed irrelevant to the predictive task (e.g., detailed GTFS route names, service date after feature extraction).
    * **Encoding:** Transformed categorical features (like route category, mode type, time of day) into a numerical format using one-hot encoding, making them suitable for machine learning models.
2.  **Exploratory Data Analysis (EDA):** Utilized visualizations (histograms, bar charts, boxplots) to explore the distribution of OTP rates, understand the frequency of different service types, and examine average performance across route categories.
3.  **Model Development:**
    * **Data Splitting:** Partitioned the data into training, validation, and testing sets using stratification to maintain the distribution of the 'high'/'low' OTP labels across sets.
    * **Model Selection:** Implemented and evaluated multiple classification algorithms, primarily focusing on:
        * **Logistic Regression:** A standard classification technique providing interpretable coefficients. Included L1 regularization for feature selection.
        * **Random Forest:** An ensemble learning method known for its robustness and ability to handle complex interactions.
    * **Hyperparameter Tuning:** Employed GridSearchCV to systematically search for the optimal parameters for both Logistic Regression (tuning `C` and `penalty`) and Random Forest (tuning `n_estimators`, `max_depth`, `min_samples_split`, `min_samples_leaf`), aiming to maximize predictive accuracy.
4.  **Model Evaluation:** Assessed model performance on the held-out test set using a range of metrics:
    * Accuracy
    * Confusion Matrix (to understand true/false positives and negatives)
    * ROC Curve and AUC score (to evaluate distinction capability)
    * Precision-Recall Curve and AUC score (useful for classification tasks)
    * Lorenz Curve (to assess accumulation of true positives)
    * Feature Importance / Coefficients (to identify key drivers)

## 💡 Key Findings

The analysis yielded significant insights into MBTA service reliability:

* **High Predictive Performance:** The optimized **Random Forest** model demonstrated exceptionally strong predictive power, reportedly achieving **98.5% accuracy** and a **ROC-AUC score of 0.99** according to the project abstract. This suggests the model was highly effective at identifying patterns linked to reliability in the historical data used.
* **Critical Factors Identified:** Several factors consistently emerged as the most influential predictors of service reliability:
    * **Peak Hours (`peak_offpeak_ind`):** 🕒 Services operating during peak commute times are significantly more likely to face delays and exhibit lower on-time performance. This was a dominant factor.
    * **Route Category:** 🚌🚆 The specific type of route (e.g., Key Bus routes vs. Other Bus routes, different train lines) plays a crucial role in determining reliability levels.
    * **Historical Performance (`otp_numerator`):** Metrics related to past on-time performance are strong indicators of future reliability.
    * **Day of the Week (`service_day`):** 📅 Reliability patterns differ depending on the day, reflecting varying ridership and traffic conditions.

## 🎯 Recommendations for MBTA

Leveraging these data-driven findings, the following actions are recommended to enhance MBTA service reliability:

1.  **Target Peak Hour Congestion:** ✅ Given the strong correlation between peak hours and lower reliability, strategically allocate extra resources (vehicles, personnel, potentially transit signal priority) during these specific times to mitigate delays where they are most likely to occur.
2.  **Optimize Specific Routes:** 🗺️ Conduct detailed reviews and implement targeted improvements for the route categories identified as having lower baseline reliability. This could involve schedule adjustments, increased frequency, route modifications to bypass chokepoints, or infrastructure investments.
3.  **Embrace Data-Driven Operations:** 💻 Implement systems for continuous performance monitoring using metrics like `otp_rate`. Consider using predictive models (potentially refined with more data) to inform dynamic scheduling and proactive disruption management.
4.  **Expand Data Integration:** ☁️ Enhance future analyses and models by incorporating additional relevant data sources, such as real-time traffic conditions, weather data, and information on special events or construction impacts.

## 🚀 Files in Repository

* `Code.ipynb`: The Jupyter Notebook containing all the Python code for data loading, preprocessing, EDA, model training, tuning, and evaluation.
* `MBTA.png`: Logo image for the Massachusetts Bay Transportation Authority.
* `README.md`: This overview document.

## ▶️ How to Use

1.  **Explore the Code:** Open `Code.ipynb` using Jupyter Notebook, Jupyter Lab, Google Colab, VS Code (with Python/Jupyter extensions), or any compatible environment. This allows you to examine the step-by-step analysis and model implementation.
2.  **Run the Analysis (Optional):**
    * You will need the `mbta.csv` dataset from the MassDOT Open Data portal (linked above).
    * Ensure the file path referenced in the notebook for loading the CSV is correct for your local setup.
    * Install the required Python libraries listed under Dependencies.
    * Execute the cells sequentially to replicate the analysis.

## ⚙️ Dependencies

* pandas
* numpy
* scikit-learn (sklearn)
* matplotlib
* seaborn
* ipython

## 🧑‍💻 Author

* Sai Sudheer Naraharisetty
