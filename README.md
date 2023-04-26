<img width="1337" src=images/Header1.jpg>

# Forecasting NYC Car Collisions: Steering Towards a Safer Future

Time Series Analysis of the Leading Collision Causes within the Top 5 High-Risk Zip Codes within Queens & Brooklyn

Author: [Annie Zheng](https://github.com/anniezhengaz/)

## Table of Contents

- [Overview](#overview)
- [Business Problem](#business-problem)
- [The Bottom Line](#the-bottom-line)
- [Data Understanding](#the-bottom-line)
- [Modeling](#modeling)
- [Visualizations](#visualization)
- [Conclusion](#conclusion)
- [Repository Structure](#repository-structure)


## Overview

This project analyzes car collision data aimed to analyze the leading causes of collisions and the top 5 high-risk zip codes within Queens and Brooklyn boroughs in order to identify accident types and driver behaviors. Analysis and modeling shows that certain causes and zip codes lead to greater risk of injury. This analysis can be used for developing target collision interventions and campaigns.

<img width="1337" src=images/Header2_QueensRoad.jpeg> 

## Business Problem
Car crashes have been happening every day all around the world ever since the invention of the very first car. These accidents pose a thread to everyone, but particularly to dense areas with large populations, such as Queens and Brooklyn boroughs within New York City whose population amounts to over 4 million people total. The New York City Department of Transportation may be able to mitigate preventable collisions and reallocate resources to cut down the amount of collisions that occur. In doing so, the current and future residents of Queens and Brooklyn could live in safer neighborhoods. Using NYC OpenData's data, leading causes of car collisions were identified as well as which neighborhoods are considered high-risk as a result of the number of injuries due to collisions.

## The Bottom Line
Before we proceed forth with the data, what's the bottom line up front?
Well, the top 5 zip codes that pose the greatest risk to drivers are 11236 (Brooklyn), 11207 (Brooklyn), 11234 (Brooklyn), 11368 (Queens), and 11385 (Queens). These 5 zip codes are considered high-risk due to their high injury to collision ratio based on 5-years worth of data.

The models exhibited an error of 3 crashes per day due to a moving violations and an error of 4 crashes per day due to driver inattention within these zip codes.

<img src=images/Map_Top5HighRiskZones.png>

## Data Understanding
This project utilizes data from [NYC OpenData](https://data.cityofnewyork.us/Public-Safety/Motor-Vehicle-Collisions-Crashes/h9gi-nx95) website with data received from the New York Police Department (NYPD). With nearly two million rows of collisions spanning from 2012 to 2023 within all five boroughs, the dataset provide additional information including location, number of injuries and casualities, contributing factors and vehicle types. Additional [Zip Code Boundaries](https://data.cityofnewyork.us/Business/Zip-Code-Boundaries/i8iw-xf4u) data was also provided by NYC OpenData for additional mapping efforts.

This analysis focused on the two NYC boroughs with the largest populations - Queens and Brooklyn with only collisions that occured within the last five years, 2018 to 2023. The target variable in the analysis was `CONTRIBUTING FACTOR VEHICLE 1` which laid a foundation for the rest of the analysis and modeling. The goal of this analysis to identify the leading factors in collisions and recommend the actions that could mitigate or prevent future collisions. Columns such as `ZIP CODE` and `NUMBER OF PERSONS INJURED` were vital in the identification of high-risk zip codes. The dataset contained a mixture of numerical and categorical data, however, it is important to understand that Time Series models require numerical data. 

### Data Cleaning & Preparation
To prepare the data for modeling, the following data cleaning steps were performed:
* Changing to DateTime index
* Filtering to collisions that occured between 2018-2023
* Borough selection - Queens & Brooklyn
* Removal of missing and outlier values
* Removal of columns with repetitive and non-relevant data to analysis
* Imputation of missing values

In addition to data cleaning, numerous features were engingeered, including:
* Main Collision Cause Categories (10 categories)
* Season
* Time of Day
* Rush Hour
* Injury/Collision Ratio

Time series models require numerical data and since the cause of a collision is categorical data, we must find a way to convert the data from categorical to numerical. Instead of performing the standard One Hot Encoder and resampling techniques, the groupby technique was utilized to resample the data from the time of occurence to daily and groupby each of those days by cause category to attain the number of collisions that occurred each day due to a specific cause. A pivot table was utilized to attain a more readable format. Lastly, for time series modeling, a datetime index is absolutely vital and was the last step in preparation for modeling. 

## Modeling
A total of 5 types of models, including the baseline were performed to forecast car collisions:
* Baseline Model - Naive Shift model
* First Model - ARIMA model 
* Second Model - SARIMA model
* Third Model - Prophet Model
* Fourth Model - Prophet Model with Holidays

The metric that will be used to determine the quality and effectiveness of the model will be Root Mean Squared Error (RMSE). 

Two separate datasets were modeled, one being daily Moving Violation collision count and the second being Driver Inattention collision count. As mentioned previously a datetime index is vital in time series modeling. The datetime index and the collision count collisions will be the basis of modeling.

| Model for Moving Violations | Error (Rounded) |
| ----------- | ----------- |
| Baseline Model      | 6 |
| ARIMA Model | 5 |
| SARIMA Model | 4 |
| Prophet Model | 3 |
| Prophet Model with Holidays | 3 |

The final model's predictions had an error of 3 car collisions per day caused by moving violations.

<img src=images/CollisionFrequency_MovingViolation.png>

| Model for Driver Error | Error (Rounded) |
| ----------- | ----------- |
| Baseline Model      | 5 |
| ARIMA Model | 4 |
| SARIMA Model | 6 |
| Prophet Model | 4 |
| Prophet Model with Holidays | 4 |

The final model's predictions had an error of 3 car collisions per day caused by driver inattention.

<img src=images/CollisionFrequency_DriverInattention.png>

## Visualizations
The following visuals were created to help us better understand the information at hand. These are a few of the plots made, to see more, please visit the [images](Capstone-NYC-Collisions/tree/master/your-images) folder. 

<img src=images/CollisionCauseFrequency.png>
Of the 10 collision cause categories, two top the charts. Moving violations make up nearly 50% of the car crashes within the dataset. This cateogry includes following too closely, improper turning, failure to stay in your lane. Driver Inattention/distractions make up 40% and consists of driver inexperience, road rage or eating behind the wheel. These two categories make up nearly 90% of the car crashes. Since they make up the vast majority, our analysis focused on these two causes.

<img src=images/Top5TotalInjuriesByZipCode.png>
This chart provides a visual representation of the distribution of injuries across different zip codes. The areas with the highest number of injuries may be particularly important to focus on for targeted interventions aimed at reducing the number of collisions and injuries. The blue line hovering around 1,500 injuries is the indicator of the mean number of injuries. Fun fact, 4 of the 5 zip codes are neighbors.

<img src=images/Map_CollisionHeatMap_Top10ZipCodes.png>
Since there are over 100 zip codes within Queens and Brooklyn, we’ve elected to map the top 10% of zip codes with the highest number of collisions caused by moving violations and friver unattention. We see the high frequency in crashes near the three large and heavy traffic bridges in/out of Manhattan.In Queens we see a lot of crashes near MetLife Stadium and LaGuardia Airport. In lower Brooklyn, we see an abundance of collisions around the Brooklyn coast near parks and beaches. 


## Conclusion
### Recommendations
Our analysis has lead us to these three recommendations aimed to mitigate car collisions. Implementing these efforts in the top 5 high-risk zip codes could be the start of a safer future.
* **Increase safety campaign efforts.** Posting safety campaign flyers locally such as at bus stops or street corners could increase exposure as they have a significant amount of foot traffic. Other areas of interest include advertising boards by major roadways and highway electric VMS (Variable Message Signs).
* **Improve the public transit system.** Reallocation of funds towards public transportation could reduce the number of drivers on the road. More reliable and cleaner transportation methods such as the MTA bus and subways could drastically increase the amount of public transit users. 
* **Create additional safety training programs** Many people begin to learn about driving in their late teens because that's when they can take the driver's test to get their license. However, good habits are developed over time. Teaching students good driving habits at a younger age will allow them to develop better driving habits earlier on and could be more likely to bring them with them to adulthood as well as build a better foundation. These additional safety programs could be in collaboration with driving schools or the public education system. Providing additional monetary incentives such as the driver safety course that provudes a 10% reduction in a driver's base insurance rates, could also incentivize drivers to partake in the training program. 

### Future Insights & Next Steps
To improve the accuracy and comprehensiveness of this project in the future, additional information such as the following can be included in analysis:
* **Weather conditions** Weather conditions such as snow or fog affects drivers' visibility as well as driving capabilities and road conditions. 
* **Road conditions** Potholes are not a driver's best friend. Potholes, narrow roads, and even road construction can affect a driver's ability to navigate the road safely.
* **Driver information/demographics** This would allow for us to determine whether specific age group or gender are more or less likely to cause or be included in collisions. 


## Repository Structure

```
├── data                                <- CSV data files
├── exploratory_files                   <- Jupyter notebooks dedicated to data exploration and modeling
├── images                              <- Data files used in analysis
├── Final_Notebook.ipynb                <- Narrative documentation of analysis in Jupyter notebook
├── README.md                           <- The top-level README for reviewers of this project
├── Presentation.pdf                    <- PDF version of project presentation
```
