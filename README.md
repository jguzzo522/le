# Business Understanding

Life expectancy throughout the world varies drastically amongst countries due to several major factors including healthcare, education, and financial resources. This project predicts variables that affect the increase or decrease of life expectancy. Recommendations will be made using modeling to inform the United Nations (UN) with data that can lead to developing interventions to increase life expectancy.

![Screen Shot 2024-05-07 at 11 30 22 PM](https://github.com/jguzzo522/le/assets/75549456/5f994a7b-2aaf-4114-ad80-d71a7aec1032)

# Data Understanding

The dataset is from the World Health Organization (WHO). In the original dataset that contains data from 2000-2015, there were 193 countries, or all the countries in the UN. There were 22 columns and 2928 rows. The target variable in this project will be life expectancy. After removing outliers and missing data, and adding a datasheet for drinking water, there were 179 countires, 2,880 rows and 32 columns.

The intial columns were from a dataset from [Kagel]( https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who?resource=download), however additional data was added for drinking resources from [UNICEF Water](https://data.unicef.org/sdgs/goal-6-clean-water-sanitation/). 


| Column Name                        | Description                           |
|------------------------------------|---------------------------------------|
| Country                            | Name of the country                   |
| Year                               | Calendar year of the data             |
| Status                             | Developed or Developing status        |
| Life expectancy                    | Life expectancy in age                |
| Adult Mortality                    | Adult mortality rates per 1000 population |
| Infant deaths                      | Number of infant deaths per 1000 population |
| Alcohol                            | Alcohol consumption per capita (liters) |
| Percentage expenditure             | Expenditure on health as a % of GDP per capita |
| Hepatitis B                        | Hepatitis B immunization coverage among 1-year-olds (%) |
| Measles                            | Number of reported measles cases per 1000 population |
| BMI                                | Average Body Mass Index of entire population |
| Under-five deaths                  | Number of under-five deaths per 1000 population |
| Polio                              | Polio immunization coverage among 1-year-olds (%) |
| Total expenditure                  | Government expenditure on health as a % of total government expenditure |
| Diphtheria                         | Diphtheria immunization coverage among 1-year-olds (%) |
| HIV/AIDS                           | Deaths per 1000 live births HIV/AIDS (0-4 years) |
| GDP                                | Gross Domestic Product per capita    |
| Population                         | Population of the country             |
| Thinness 1-19 years                | Prevalence of thinness among children and adolescents 10-19 years (%) |
| Thinness 5-9 years                 | Prevalence of thinness among children 5-9 years (%) |
| Income composition of resources    | Human Development Index in terms of income composition of resources |
| Schooling                          | Average number of years of schooling of the population |

# Exploring the Data

An initial review of the target variable was conducted to show the distribution of life expectancy in the entire dataset. The max amount of life expectancy was 89 years, while the minimum was 36 years. The average for the entire dataset was 69 years. However, there is a standard deviation of 9.5 years, indicating the distribution of life expectancy has a wide range across countries.

The top 5 countries with the highest average life expectancy were Japan, Sweden, Iceland, Switzerland, and France. All of these countries had average life expectancies in the 80's.

The bottom 5 countries with the lowest average life expectancy were Sierra Leone, Central African Republic, Lesotho, Angola, and Malawi. All of these countries had an average life expectancy in the 40's.

![Screen Shot 2024-05-11 at 9 09 59 PM](https://github.com/jguzzo522/le/assets/75549456/d7ef50c2-eaad-4565-a182-1796326ebf6e)


# Data Preperation

The initial step in the data preparation was to search for NAN values, and place holders in the life expectancy column.

There were 10 NaN values, upon further investigation as to what countries had these NaN values, Cook Islands, Dominica, Marshall Islands, Monaco, Nauru, Niue, Palau, Saint Kitts and Nevis, San Marino, and Tuvalu were identified. Further investigation into these countries, indicated substantial missing data in many columns for the year 2013. The decision was made to remove these 10 countries from further analysis for year 2013.

Every column was throughly explored, and missing values, and place holders were removed and or changed. In addition, the orginal dataset had a large amount of missing data. Due to this issue, more data was merged from database websites from UNICEF, The WHO, and the World Bank. 

Most columns were able to be salvaged, using outside data, however some columns were removed from the database. Diphtheria, HIV/AIDS, BMI and Income Composition of Resources were the columns that were removed from this project.

Somalia, North Korea and Sudan were also removed from the dataset due to the many NaN values, as well as not being able to find the missing data from the databases of the UNICEF, WHO, and the World Bank.

# Modeling
Multiple Linear Regression is a statistical method used to analyze the relationship between a dependent variable and two or more independent variables. It estimates how changes in the independent variables are associated with changes in the target variable, enabling predictions and insights into complex relationships.

In this project, we utilize Multiple Linear Regression to examine the relationship between various factors and life expectancy (target variable). Key findings from the regression analysis include:

# Model Evaluation:

- **Model Fit**: The model explains approximately 51% of the variance in life expectancy, as indicated by the medium R-squared value of 0.510.
- **Overall Significance**: The model is highly significant (F-statistic = 186.5, p < 0.00), suggesting that the included predictors collectively contribute to explaining life expectancy.

The bar chart indicates which coefficents have the largest impact on life expectancy. The coefficents 'Alcohol', and 'schooling' had the largest impact on life expectancy.

Key Factors

- **Alcohol**: (-0.3) indicates that for every liter consumed per capita, we can expect the country to have around 0.3 less years of life expectancy.

- **Schooling**: (3.2) indicates that for each additional year of school a country can expect to see an additional 3.2 years added to the life expectancy.
- 
![Screen Shot 2024-05-13 at 11 22 40 PM](https://github.com/jguzzo522/le/assets/75549456/336f430b-c2b9-4269-a46e-b38ae38eac83)

![Screen Shot 2024-05-13 at 11 23 03 PM](https://github.com/jguzzo522/le/assets/75549456/a56c9491-37ca-4511-885b-b020f4d67923)

Homoscedasticity Testing was conducted to test for normality. The Q-Q plot indicates that the model is following a normal distribution except on its uper tail. The tail indicate that the model deviates from a normal distribution due to its maximum values. This could indicate there are outliers in the data. The Anderson-Darling statistic of 19.43 indicates the model is mostly normally distributed. 

![Screen Shot 2024-05-13 at 11 23 47 PM](https://github.com/jguzzo522/le/assets/75549456/f185c05b-aba3-4f15-b52e-f9a228564aa7)

# Time Series Modeling 

Predictive time series modeling was applied the life expectancy data to forecast future trends. A Prophet forecasting model to predict life expectancy up to the year 2025. The model was fitted with data that includes yearly life expectancy values for all the countires in the df_cleaned dataset. The model predicts that life expectancy will increase through the year 2025(last year selected). In this analysis life expectancy is expected to grow by over 3 years globally. 

![Screen Shot 2024-05-13 at 11 27 41 PM](https://github.com/jguzzo522/le/assets/75549456/964cd9e7-bd04-4b40-8cdf-604300b1a314)

# Time Series Africa vs Europe

Time Series modeling was conducted to compare the life expectancy for Africa and Europe. In order to run this time series, the appropriate countries had to be defined into Africa and Europe. 

After defining Africa and Europe, a time-series was for forecasted and the plot shows the large difference of life expectancy between Europe and Africa. Africa in 2000 was expected to live 20 years less than the average European country. However, in 2025 the difference is about 10 years.

In this timeseries a rolling mean was used to smooth the life expectancy data, which helps to reduce short-term fluctuations.

![Screen Shot 2024-05-13 at 11 36 23 PM](https://github.com/jguzzo522/le/assets/75549456/934db3c6-550a-4593-9fe6-ed1471f55500)

# Time Series Modeling Including Schooling

The mean was calculated for the number of school years in the entire dataset, Europe, and Africa. Africa was then increased to match the average European School years. Once the school years were updated a Time-series model was ran to predict life expectancy for Africa. 

The chart below shows that the life expectancy is predicted to increase by around 6 years from 2016-2025, if the schooling years are increased to match the European school years. 

This indicates that the UN should greatly increase funding for schools in African countries, in attempt to increase life expectancy. 

![Screen Shot 2024-05-13 at 11 28 40 PM](https://github.com/jguzzo522/le/assets/75549456/fd3bbdfd-3c50-47e5-a08f-eeddb9c0cf6f)

# Conclusion

![Screen Shot 2024-05-14 at 5 09 35 PM](https://github.com/jguzzo522/le/assets/75549456/fba8d7ed-a6c8-4d86-829c-73cbb31fe6ff)

## Model Evaluation

The significant model, although having a lower adjusted R-squared and F-statistic compared to the initial model, signifies a reduction in the explanatory power and overall significance of the model. This decrease is primarily due to the removal of several independent variables. However, despite these reductions, the refined model presents a notable advantage—it comprises only statistically significant coefficients with p-values less than 0.05. This suggests that the variables retained in the refined model have a stronger association with the dependent variable, life expectancy, and provide more reliable insights into its determinants.

The Anderson-Darling test statistic for both models assesses the normality of residuals. A lower Anderson-Darling test statistic indicates a better fit to the normal distribution, implying stronger evidence for normality. In this comparison, the refined model exhibits a substantially lower Anderson-Darling test statistic, suggesting a better fit to the normal distribution for its residuals. This signifies that the residuals of the refined model are more closely aligned with the assumptions of normality, enhancing the model's reliability for statistical inference and prediction.

In summary, while the refined model sacrifices some overall explanatory power and significance, its focus on statistically significant coefficients and improved normality of residuals enhances its robustness and reliability for understanding and predicting life expectancy variations.


| Model                        | Initial                   | Significant Model        |
|------------------------------|---------------------------|--------------------------|
| Adjusted R-squared           | 0.953                     | 0.510                    |
| F-statistic                  | 2232.0                    | 228.2                    |
| Anderson-Darling Test Stat   | 68.20                     | 19.43                    |

## Limitations of the Model¶
Although, the model only deals with significant coefficients, the R- squared, shows that the model only accounts for 51% of the variance in life expectancy. This indicates that 50% of the variance is not explained by this model.

This model also has questionable data, such as the water resource groupings. This model indicates that unimproved water sources produce a positive effect on life expectancy, while water sources free from contamination actually decrease life expectancy. From general knowledge, we can assume this is incorrect. This indicates that the data about drinkable water may need to be adjusted, and or reviewed more throughly. It’s possible that some of the water columns should have been combined, or deleted from this project.

Another limitation for this model is that some of the original columns, such as HIV/AIDS were removed from the dataset. It’s possible that this missing data could explain more of the variance in life expectancy.

One further limitation was the data itself. Life expectancy could have been analyzed in different manner. For instance, removal of outliers may have been appropriate. For instance, Haiti had one very low life expectancy year in 2010 due to the earthquake that killed many of the population. However, the year before and after were both in the 50's. It may have been helpful to remove more outliers to make a more reliable dataset
## Time Series Africa Schooling

A time series analysis was run using the prophet package. In this Timeseries analyis schooling was added to predict the life expectancy for Africa. Schooling was added becasue in the previous Multiple Linear Regression model, schoolng was one of the most important coefficets for increasing life expectancy. 

All African countires and European countires were catagoreized into their correct continents. After this catagorization was completed, the average for schooling years in the UN, Europe and Africa was calculated. It was found that Africa averaged around 10 schooling years, while Europe averaged around 20. Europe averaged more schooling years than the mean of the world which was around 15. 

Africa was then increased to match the average European School years. Once the school years were updated a Time-series model was ran to predict life expectancy for Africa. 

This model showed that when increasing the number of schooling years to match that of Europe, life expactancy greatly increased in Africa by around 6 years.

# Limitations, Next Steps, and Reccomendations

Altough this project looked at many important variables, there were many not considered. The next project could look at the years 2016-2023. The data does not have to be limited to just UN countires. Other variables could be added such as access to healthcare, or post 2020 data on Covid's impact on life expectancy.

Other area of study could include the diffrences in gender and life expectancy. Or how the ongoing wars in Ukraine and Isreal are impacting life expectancy. There were also columns in the water catagory that included access to water in hospitals, or personal hegine. These topics could be explored. 

More data on HIV/AIDs and other dieseases can also be analyzed.

The next steps should be for the UN to provide further data for analuzaion. 

Reccommendations

- **Increase Schooling**
- **Decrease Alcohol Consumption**
- **Focus on developing countries**
- **Ensure access to atleast basic water**

# Repo Sturcture
 
├── gitgnore

├── [README.md](https://github.com/jguzzo522/le/blob/main/README.md)

├── [le notebook](https://github.com/jguzzo522/le/blob/main/le.ipynb).

└── [lifeexpectancyslides.pdf](https://github.com/jguzzo522/le/blob/main/lifeexpectancy.pdf)
