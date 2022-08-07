# Will Your Flight be Delayed?

*MIDS W261: Machine Learning at Scale | UC Berkeley School of Information | Spring 2022 | Final Project Report*

**Team 12: "CAWVS"** | *Sections: 3 and 4*

Stephen **C**hen | Mahesh **A**rumugam | Radia **W**ahab | Jericho **V**illareal | Ramanuj **S**ingh

## 1. Introduction

Air travel has a significant role in shaping economies of states and thus it is important to optimize every aspect of the flight cycle to increase the quality of airline's services, most especially the consistent on-time departure flights. However, due to multiple variables and external factors, airline flight delay is inevitable, and thus have to be accounted for by the airline company executives in order to optimize value to multiple stakeholders -- from the shareholders to the customers. 

Fortunately, since June 2003, airlines that report on-time data also report the causes of delays and cancellations to the Bureau of Transportation Statistics. The airlines report the causes of delay in broad categories created by Air Carrier On-Time Reporting Advisory Committee. Specifically these categories are the following [1]  

- Air Carrier: delays due to circumstanes within the airline's control such as maintenance problems, baggage loading, aircraft fueling, etc.
- Extreme Weather: actual or forecasted significant meterorological conditions, such as blizzard or hurricane, that prevents airline operations  
- National Aviation System (NAS): delays and cancellations attributable to a broader set of conditions like air traffic control
- Late-arriving aircraft: previous flight with the same aircraft arrived late, causing the present flight to depart late (knock-on effect)
- Security: delays and cancellations caused by evacuation of aircraft or terminal and inoperative screening equipment and/or long lines in excess of 29 minutes at screening areas.

#### How do airlines think about flight delays?

Based on data gathered from the Bureau of Transportation Statistics (BTS.gov) across the major airport hubs in the United States from 2015 to 2018, at least 10% of the flights get delayed on a daily basis, and has seen this rate to increase to about 35% to 40% daily. Some of the major airlines have made strides in reducing their own delayed rate or even keeping it at a steady rate, while others have increases in flight delays which in turn affect the airline company's financials. 

The business case is that in 2018 the total cost of flight delays has been estimated at [$28 billion](https://www.airlines.org/dataset/u-s-passenger-carrier-delay-costs/#:~:text=Assuming%20%2447%20per%20hour*%20as,2018%20to%20be%20%2428%20billion). In aviation, an airline departure are considered to be "on-time" when they depart within 15 minutes of the scheduled flight. This is the basis of the airline's proposition to its customers and also a huge factor in measuring an airline’s On-Time Performance (OTP) metric. OTP is a widely used metric for airlines and is an outward demonstration of reliability which can affect multiple facets of the company like sales, branding, and customer satisfaction. In optimizing OTP metric, some airlines would rather create ‘ghost flights’ than not have to give up airport slots, which is set of permissions to schedule landing or departure at the airport during specific time period.

### 1.1. Datasets

There were three main datasets used in this project.

1. Airlines dataset from the United States Department of Transportation, utilizing the Bureau of Transportation Statistics (BTS.gov)[__1__]. The size of the data set is 31,746,841 rows x 109 columns ([documentation](https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FGJ)). This dataset comprises of per-flight data of departure time* from 2015 to 2019. Data includes variables which classify a flight to be delayed or on-time and other metadata concerning each of the flights.  

2. Weather dataset from the National Oceanic and Atmospheric Administration (NOAA)[__2__]. The size of the data set is 630,904,436 rows x 177 columns. This data set comprises Spatio-temporal weather attributes across multiple geographic regions. Examples include precipitation, snow depth, wind speed, and air temperature.

3. Weather station dataset from the National Weather Service NWS.gov. The size of the data set is 5,004,169 rows x 12 columns. This data set comprises Spatial data on the location of weather stations across multiple geographic regions. We joined this dataset with a weather dataset to find the closest weather station to an airport. 

### 1.4. Databricks Spark Cluster: Configuration

|Parameter |	Value |	Description |
|-----------------|---------------|-----------------|
|**Cluster Name** |	team12	|Cluster name for the team |
|**Custer Policy** |	Unrestricted |	A cluster policy limits the ability to configure clusters based on a set of rules. Unrestricted policy allows to  create fully-configurable clusters and  does not limit any cluster attributes or attribute values.|
|**Cluster Mode** |	High Concurrency |	Databricks supports three cluster modes: Standard, High Concurrency, and Single Node. The default cluster mode is Standard. A High Concurrency cluster is a managed cloud resource. The key benefits of High Concurrency clusters are that they provide fine-grained sharing for maximum resource utilization and minimum query latencies.|
|**Cluster Driver Size** |	Standard_D4s_v3 <br/>16 GB Memory, 4 Cores	| The node type of the Spark driver |
|**Cluster Worker Size** |	Standard_D4s_v3 <br/>16 GB Memory, 4 Cores	| The node type of the Spark worker |
|**Cluster Workers Quantity** |	min_workers: 1 <br/> max_workers: 6	| Number of worker nodes that this cluster should have. Autoscaling is enabled.|
|**Spark Version** |	9.1.x-cpu-ml-scala2.12	| Version of Spark |
|**Databricks Runtime Version** | 9.1 LTS ML (includes Apache Spark 3.1.2, Scala 2.12) |	The runtime version of the cluster.|

### 1.6. Links to Notebooks 

* [Exploration](https://github.com/skchen999/Will-Your-Flight-be-Delayed/blob/main/supplemental%20notebooks/Exploration.ipynb)
* [Airlines Dataset: Transformation and Feature Engineering](https://github.com/skchen999/Will-Your-Flight-be-Delayed/blob/main/supplemental%20notebooks/Full%20Dataset_%20Airlines.ipynb)
* [Weather Dataset: Transformation and Feature Engineering](https://github.com/skchen999/Will-Your-Flight-be-Delayed/blob/main/supplemental%20notebooks/Full%20Dataset%20_%20Weather.ipynb)
* [Joins](https://github.com/skchen999/Will-Your-Flight-be-Delayed/blob/main/supplemental%20notebooks/Joins.ipynb)
* [Machine Learning Models](https://github.com/skchen999/Will-Your-Flight-be-Delayed/blob/main/supplemental%20notebooks/Models_%20Full%20Dataset.ipynb)
* [Support Vector Machines: Native Implementation on RDDs](https://github.com/skchen999/Will-Your-Flight-be-Delayed/blob/main/supplemental%20notebooks/SVM%20Implementation%20and%20Evaluation%20on%20Toy%20Dataset.ipynb)
* 2020 Model Evaluation
   * [2020 Airlines Data: Transformation and Feature Engineering](https://github.com/skchen999/Will-Your-Flight-be-Delayed/blob/main/supplemental%20notebooks/2020%20Airlines.ipynb)
   * [2020 Weather Data: Transformation and Feature Engineering](https://github.com/skchen999/Will-Your-Flight-be-Delayed/blob/main/supplemental%20notebooks/2020%20Weather.ipynb)
   * [2020 Model Evaluation: Joins, Pipeline Transformation and Model Evaluation](https://github.com/skchen999/Will-Your-Flight-be-Delayed/blob/main/supplemental%20notebooks/Model%20Evaluation_%202020%20Dataset.ipynb)
   
## 7. Conclusions

Our main evaluation metric was Area Under PR Curve due to the imbalanced nature of our dataset and also as we wanted to focus more on the positive cases than the negative cases. To recap the results from all the models implemented, please refer to the table below:

##### Test Metrics on 2019 heldout dataset

|   Model               | Area Under PR     | F1 score       | Recall          |  Precision     |
|-----------------------|-------------------|----------------|-----------------|----------------|
|Logistic Regression    | \\(0.362964\\)    | \\(0.389682\\) | \\(0.591144\\) | \\(0.290633\\)  |
|Decision Trees         | \\(0.317968\\)    | \\(0.383275\\) | \\(0.592206\\) | \\(0.283319\\)  |
|Gradient Boosted Trees | \\(0.346511\\)    | \\(0.375564\\) | \\(0.515503\\) | \\(0.295380\\)  |
|XGBoost                | \\(0.386705\\)    | \\(0.400001\\) | \\(0.612218\\) | \\(0.297037\\)  |

Our best model used XGBoost and had an Area Under PR Curve around 38%. Logistic Regression was the second-best model with Area Under PR Curve around 36%.

During the evaluation with 2019 held-out dataset, across our models, our precision was around 30% and area under PR curve was around 32-38%. One thing that we feel that might be impacting our results is that we did not do any dimensionality reduction such as PCA, to reduce the number of features in our model. That could be the reason why our model performance suffered from overfitting. Please refer to Section 4 for Area Under the PR Curve plots and the Confusion Matrices for various models.

We also evaluated our models against 2020 data and we noticed that the models performed worse than 2019 data evaluation. The precision is around 12-18% across our models with area under PR curve around 10-20%. We feel that this is due to the anamolous nature of the year 2020, there were other external factors like Covid-19 and related government measures like global shutdown etc that have not been represented in the features that we have considered. Please refer section 4.7.3 for the Area Under PR Curve plot and the Confusion Matrix plots. Please refer below table for 2020 results:

##### Test Metrics on 2020 dataset

|   Model               | Area Under PR     | F1 score       | Recall          |  Precision     |
|-----------------------|-------------------|----------------|-----------------|----------------|
|Logistic Regression    | \\(0.108296\\)    | \\(0.197873\\) | \\(0.514534\\)  | \\(0.122490\\)  |
|Decision Trees         | \\(0.136206\\)    | \\(0.204086\\) | \\(0.373189\\) | \\(0.140446\\)  |
|Gradient Boosted Trees | \\(0.170174\\)    | \\(0.214192\\) | \\(0.265589\\) | \\(0.179462\\)  |
|XGBoost                | \\(0.195725\\)    | \\(0.226878\\) | \\(0.386395\\) | \\(0.160583\\)  |


Going back to the business case, these models are not used solely to predict flight delay but rather an accompanying datapoint on top of the specific domain knowledge held by stakeholders (flight control attendants, airline employees, etc). These models will complement their decision-making capabilities in making the announcement whether to delay a flight or not.