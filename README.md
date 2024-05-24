# Increasing Life Expectancy
by Jessica Guzzo
05/20/2024

# Business Understanding

Life expectancy throughout the world varies drastically amongst countries due to several major factors including healthcare, education, and financial resources. This project predicts variables that affect the increase or decrease of life expectancy. Recommendations will be made using modeling to inform the United Nations (UN) with data that can lead to developing interventions to increase life expectancy.

## Life Expectancy Globally 

![Screen Shot 2024-05-07 at 11 30 22 PM](https://github.com/jguzzo522/le/assets/75549456/5f994a7b-2aaf-4114-ad80-d71a7aec1032)

# Data Understanding

The dataset is from the World Health Organization (WHO). In the original dataset that contains data from 2000-2015, there were 193 countries, or all the countries in the UN. There were 22 columns and 2928 rows. The target variable in this project will be life expectancy. After removing outliers and missing data, and adding a dataset for drinking water, there were 179 countries, 2,880 rows and 32 columns.

The intial columns were from a dataset from [Kaggle]( https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who?resource=download), however additional data was added for drinking resources from [UNICEF Water](https://data.unicef.org/sdgs/goal-6-clean-water-sanitation/). 


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


#  Data Preparation

This dataset contained many missing data points. There were many dataset imported in and merged to correct missing or incorrect data. The following are datasets that were merged onto df_cleaned. The websites used to gather this data are further defined below. Each website had a database where the topic, countries and years could be selected. I gathered data from the years 2000-2015, for the 193 countries in the United Nations.

## Water Availability
Water was not originally in this dataset, but general knowledge indicates that water is crucial for survival. Using the UNICEF website UNICEF Water, drinking water and access were included in this analysis. To keep the data in line with the original dataset, the years 2000-2015 were imported.

To merge this dataset with the df_cleaned dataset, several steps were completed. First, the water.csv data sheet was uploaded into the notebook. To do this, water.csv was saved into the desktop folder where the original project data was stored. Then, the folder path was defined, and the data was uploaded as water.csv.

The next step was to adjust the names of the countries in the water.csv data. The water data had countries displayed as a three-letter abbreviation followed by a colon and then the capitalized country name. To match the df_cleaned data, the apply function was used to split each value in the ‘Country’ column. The first part was everything before the colon, and the second part was the country name without the abbreviation. The code then takes only the second part and removes the first part of the country name. For instance, the 'Country' column for water.csv originally had a country named "CRI : Costa Rica"; after the lambda function was applied, the country became "Costa Rica".

To merge the water data with the original data, the 'country' column was changed to lowercase, and all spaces were replaced with underscores. "Costa Rica" was converted to "costa_rica". Adjustments to other water columns were needed before merging with the original dataset. The 'water_indicator' column was updated to remove the prefix before the word "Proportion". For instance, “WS_PPL_W-ALB of population using at least basic water" became "Proportion of population using at least basic water". Then underscores were added, and the column names were converted to lowercase.

The pivot method was used to change the shape of the df_water_merged. During the pivot, the 'water_indicator' column became several columns: proportion_of_population_using_at_least_basic_drinking_water_services proportion_of_population_using_basic_drinking_water_services proportion_of_population_using_improved_drinking_water_sources proportion_of_population_using_improved_drinking_water_sources_available_when_needed proportion_of_population_using_improved_drinking_water_sources_located_on_premises proportion_of_population_using_limited_drinking_water_services proportion_of_population_using_non-piped_improved_drinking_water_sources proportion_of_population_using_of_improved_drinking_water_sources_free_from_faecal_and_priority_chemical_contamination proportion_of_population_using_piped_drinking_water_sources proportion_of_population_using_safely_managed_drinking_water_services proportion_of_population_using_surface_water proportion_of_population_using_unimproved_drinking_water_sources

The index parameter was set to 'Country' and 'Year', the columns parameter was set to 'water_indicator', and the values parameter was set to 'rate_of_water'.

Before the final merge, the country names were checked to ensure they matched the country names in df_cleaned. There were 10 countries with slightly different spellings, which were adjusted to match the correct country names. Additionally, some countries found in water.csv were not in df_cleaned and were removed. After final confirmation, a merge was completed to add the different water availability columns to df_cleaned. The df_water_pivot was merged into df_cleaned based on the ‘country’ and ‘year’ columns using a left join. This merge kept all the original columns in df_cleaned and added the new water columns.

## Population
The population column was missing many values. In oder to adjust this data from the WHO, was manually entered. The data replaced questionable and missing data from 2000-2015.

## Vaccine Data
After a thorough review of the original Hepatitis B, Polio, and Measles columns, it was evident that the dataset was missing a significant amount of data. To address this, data from UNICEF was used.

The columns were deleted and replaced with data from UNICEF. To keep the data in line with the original dataset, the years 2000-2015 were imported. Several countries had different spellings or characteristics. The names were standardized to fit the original dataset.

I defined the folder path and loaded the vaccines.csv file into my notebook. The file was saved in the same folder as the original project data on my desktop.

Next, I needed to clean the 'Country' column in the vaccines.csv data to match the format in df_cleaned. The country names in vaccines.csv were displayed as three-letter abbreviations followed by a colon and the capitalized country name. I used the apply function to split each value in the 'Country' column, extracting only the country name and converting it to lowercase. For example, "CRI : Costa Rica" became "costa_rica".

To ensure all combinations of countries and years from 2000 to 2015 were present, I created a DataFrame with these combinations and merged it with the original df_vaccines DataFrame. Any missing values were filled with 0. I verified the changes by displaying the merged DataFrame.

For Afghanistan, I filtered the DataFrame to find the specific indicator 'IM_HEPBB' and extracted the years present. This helped me understand the vaccination data coverage for Afghanistan.

I also created an updated DataFrame by iterating over each combination of country, year, and indicator to ensure all possible combinations were included. If a combination did not exist in the original DataFrame, I added a placeholder row with NaN values. The DataFrame was then sorted and the index reset to maintain order.

To clean up the data further, I dropped the 'DATAFLOW' column and pivoted the DataFrame to convert indicators into separate columns. I renamed these columns to more concise names like 'hepatitis_b', 'polio', and 'measles'.

I checked for any missing values in these columns, interpolated missing values using linear interpolation, and filled NaN values with 0 for Afghanistan specifically. This was done because there were no vaccines identified for Afghanistan for those years. I also excluded certain countries from the DataFrame and replaced spaces with underscores in the 'Country' column.

After ensuring that country names matched between df_vaccines and df_cleaned, I renamed some country entries in df_vaccines for consistency. This involved mapping certain names to their counterparts in df_cleaned.

I addressed missing vaccination data for Cabo Verde by manually adding values for hepatitis B, polio, and measles from 2000 to 2015. These values were assigned to a new DataFrame and concatenated with df_vaccines.

Finally, I dropped the 'hepatitis_b', 'measles', and 'polio' columns from df_cleaned and merged it with the updated df_vaccines DataFrame on 'country' and 'year', ensuring that the merged DataFrame was properly structured and verified.

## Adult Mortality
After a thorough review of the original Hepatitis B, Polio, and Measles columns, it was evident that the dataset was missing a significant amount of data. To address this, data from UNICEF was used.

The columns were deleted and replaced with data from UNICEF. To keep the data in line with the original dataset, the years 2000-2015 were imported. Several countries had different spellings or characteristics. The names were standardized to fit the original dataset.

First, I defined the folder path and loaded the xmart.csv file into my notebook, skipping the first row and manually setting the column headers. This allowed me to format the dataset correctly from the start.

Next, I removed special characters from the country names and converted them to lowercase to ensure consistency with the df_cleaned dataset. I then compared the unique country names from the original and modified DataFrames to identify any discrepancies.

To address these discrepancies, I used a mapping dictionary to standardize the country names, ensuring they matched the conventions in df_cleaned. This included handling various country name variations like "guineabissau" to "guinea_bissau" and "new zealand" to "new_zealand".

After mapping the country names, I rechecked for any remaining differences. I dropped countries like 'south_sudan' and 'somalia' from the modified DataFrame to match the original dataset. I also filtered out rows where the year was 2016, as they were outside the target range.

For Afghanistan, I specifically compared the 'adult_mortality' values between df_cleaned and the modified dataset to ensure the new data accurately reflected the adult mortality rates.

I then renamed columns in the modified dataset to match those in df_cleaned, ensuring smooth integration. This included renaming 'Country' to 'country' and 'Year' to 'year'. I dropped the old 'adult_mortality' column from df_cleaned and replaced it with the updated 'adult_mortality' data from the WHO dataset.

Finally, I merged the two DataFrames on the 'country' and 'year' columns, ensuring all updated adult mortality data was included in df_cleaned. I verified the updated DataFrame to confirm the changes were correctly applied.

## Underfive Mortality Rate
After reviewing the Under Five Deaths column, I noticed that for a majority of countries, the data was incorrect. I replaced the erroneous values with data from UNICEF.

First, I defined the folder path and loaded the underfive.csv file into my notebook. The file was saved in the same folder as the original project data on my desktop.

Next, I selected specific columns from the loaded DataFrame: 'REF_AREAarea', 'TIME_PERIODperiod', and 'OBS_VALUE Value'. These columns contained the relevant data for geographic areas, time periods, and under-five mortality values.

I printed the unique values and their counts for the 'REF_AREAarea' column to ensure that all country names were correctly loaded and to understand the distribution of the data.

To prepare for merging with df_cleaned, I renamed the 'REF_AREAarea' column to 'country'. I then cleaned the country names by splitting at the colon, taking the last part, stripping any whitespace, converting them to lowercase, and replacing spaces with underscores. This ensured consistency with the country naming conventions in df_cleaned.

I renamed the 'TIME_PERIODperiod' column to 'year' and the 'OBS_VALUEValue' column to 'underfive_deaths'. This made the column names more intuitive and aligned with the existing dataset.

I compared the unique country names between the modified DataFrame and df_cleaned to identify any discrepancies. I found several differences, so I replaced specific country names in the modified DataFrame to match those in df_cleaned. This included changes like 'netherlands_(kingdom_of_the)' to 'netherlands' and 'north_macedonia' to 'the_former_yugoslav_republic_of_macedonia'.

After verifying the changes, I dropped the 'under-five_deaths' column from df_cleaned to avoid any conflicts during the merge. Finally, I merged the modified DataFrame into df_cleaned on the 'country' and 'year' columns using a left join. This ensured that the under-five mortality data was accurately integrated into the existing dataset.

## Life Expectancy
The initial step in the data preparation was to search for NAN values, and place holders in the life expectancy column.

There were 10 NaN values, upon further investigation as to what countries had these NaN values, Cook Islands, Dominica, Marshall Islands, Monaco, Nauru, Niue, Palau, Saint Kitts and Nevis, San Marino, and Tuvalu were identified. Further investigation into these countries, indicated substantial missing data in many columns for the year 2013. The decision was made to remove these 10 countries from further analysis for year 2013.

Every column was throughly explored, and missing values, and place holders were removed and or changed. In addition, the original dataset had a large amount of missing data. Due to this issue, more data was merged from database websites from UNICEF, The WHO, and the World Bank. 

Most columns were able to be salvaged, using outside data, however some columns were removed from the database. Diphtheria, HIV/AIDS, BMI and Income Composition of Resources were the columns that were removed from this project.

Somalia, North Korea and Sudan were also removed from the dataset due to the many NaN values, as well as not being able to find the missing data from the databases of the UNICEF, WHO, and the World Bank.

# Modeling 

Multiple Linear Regression is a statistical method used to analyze the relationship between a dependent variable and two or more independent variables. It estimates how changes in the independent variables are associated with changes in the target variable, enabling predictions and insights into complex relationships.

This forth model only focused on developing nations. In an effort to better understand what coefficients impact life expectancy for developing nations, developed nations were removed from the model.

In this project, we utilized Multiple Linear Regression to examine the relationship between various factors and life expectancy (target variable). Key findings from the regression analysis include:

- **Model Fit**: The model explains approximately 97% of the variance in life expectancy, as indicated by the R-squared value of 0.970.
- **Overall Significance**: The model is highly significant (F-statistic = 5754, p < 0.00), suggesting that the included predictors collectively contribute to variations in life expectancy.

The bar chart indicates which coefficients have the largest impact on life expectancy. The coefficients 'Alcohol' , 'under five deaths' and 'Schooling' had the largest impact on life expectancy. In the previous two models 'Alcohol was found to decrease life expectancy, however in this model it was shown to increase life expectancy. It is important to note that because some developing nations are religious, their cultural beliefs forbid them from drinking alcohol. For this reason, and the inconsistency with the previous models, we decided to focus on total expenditure as our third most important coefficient. 

![Screen Shot 2024-05-17 at 10 09 53 AM](https://github.com/jguzzo522/le/assets/75549456/4af39d48-b6ba-430c-96d0-29341038ba6a)

Key Factors
- **Total Expenditure**: (0.0491) indicates that for each 1 percentage point increase in the total government expenditure spent on healthcare, the life expectancy is expected to increase by approximately 0.0491 years, holding all other variables constant.

- **Under Five Deaths**: (-0.0703) indicates each additional death per 1,000 population in the under-five mortality rate, the life expectancy is expected to decrease by approximately 0.0703 years, holding all other variables constant

- **Schooling**: (0.1704) indicates that for each additional year of schooling, a country can expect to see an additional .17 years added to the life expectancy. 


This model has only significant coefficients (p < .05).

![Screen Shot 2024-05-13 at 11 23 03 PM](https://github.com/jguzzo522/le/assets/75549456/a56c9491-37ca-4511-885b-b020f4d67923)


Homoscedasticity Testing was conducted to test for normality. The Q-Q plot indicates that the model t following a normal distribution, except on its upper tail. The tail indicate that the model deviates from a normal distribution due to its maximum values. This could indicate that there are outliers in the maximum values. 

![Screen Shot 2024-05-17 at 10 11 15 AM](https://github.com/jguzzo522/le/assets/75549456/91d01c27-0637-4933-87b3-2dc917f582c3)


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

![Screen Shot 2024-05-20 at 11 37 36 AM](https://github.com/jguzzo522/le/assets/75549456/38879498-6c27-4cbd-92b4-2bfbec200bc6)

# Conclusion

![Screen Shot 2024-05-14 at 5 09 35 PM](https://github.com/jguzzo522/le/assets/75549456/fba8d7ed-a6c8-4d86-829c-73cbb31fe6ff)

## Model Evaluation

The model selected was the 4th model Developing Countries with Significant Coefficients. Using Multiple Linear Regression as a statistical method to analyze the relationship between the target variable Life Expectancy, with all other variables, predictions and insights were made.  The R-Squared, while the second lowest of the entire project, was still very high at 0.970. This indicates that 97% of the variance in life expectancy is explained by this model.

This specific model only focused on what could increase life expectancy in developing nations. This was instrumental in the analysis, because the data indicates that developing nations have a much lower life expectancy than do developed nations. This model also only focused on significant coefficients (p <.05). 

The model showed many important coefficients:

Key Factors
- **Total Expenditure**: (0.0491) indicates that for each 1 percentage point increase in the total government expenditure spent on healthcare, the life expectancy is expected to increase by approximately 0.0491 years, holding all other variables constant.

- **Under Five Deaths**: (-0.0703) indicates each additional death per 1,000 population in the under-five mortality rate, the life expectancy is expected to decrease by approximately 0.0703 years, holding all other variables constant

- **Schooling**: (0.1704) indicates that for each additional year of schooling, a country can expect to see an additional .17 years added to the life expectancy. 

Homoscedasticity Testing was conducted to test for normality. The Q-Q plot indicates that the model t following a normal distribution, except on its upper tail. The tail indicate that the model deviates from a normal distribution due to its maximum values. This could indicate that there are outliers in the maximum values. 

| Model | Description                                       | R-squared | Adjusted R-squared | F-statistic |
|-------|---------------------------------------------------|-----------|--------------------|-------------|
| 1     | Basic Model                                       | 0.953     | 0.953              | 2232        |
| 2     | Significant Coefficients                          | 0.991     | 0.991              | 20520       |
| 3     | Developing Countries Only                         | 0.971     | 0.971              | 3554        |
| 4     | Developing Countries with Significant Coefficients| 0.970     | 0.970              | 5754        |

## Recommendations

Based on this project, it could be suggested that the UN should look to increase education (average years of schooling) in developing nations, as well as encourage nations to spend more of their total expenditure on healthcare. This is where the UN can also allocate additional resources to ensure money is spent in the healthcare field. Additionally under five deaths is an issue in developing nations. The UN should help ensure that hospitals, have correct funding, the appropriate healthcare can be performed on children. These improvements would have positive impacts on average life expectancy.

## Limitations of the Model

A limitation for this model is that some of the original columns, such as HIV/AIDS were removed from the dataset. It’s possible that this missing data could explain more of the variance in life expectancy. 

One further limitation was the data itself.  Life expectancy could have been analyzed in different manner. For instance, removal of outliers may have been appropriate. For instance, Haiti had one very low life expectancy year in 2010 due to the earthquake that killed many of the population. However, the year before and after were both in the 50's. It may have been helpful to remove more outliers to make a more reliable dataset.

## Time Series Africa Schooling

A time series analysis was run using the prophet package. In this Time-series analysis schooling was added to predict the life expectancy for Africa. Schooling was added because in the previous Multiple Linear Regression model, schooling was one of the most important coefficients for increasing life expectancy. 

All African countries and European countries were categorized into their correct continents. After this categorization was completed, the average for schooling years in the UN, Europe and Africa was calculated. It was found that Africa averaged around 10 schooling years, while Europe averaged around 20. Europe averaged more schooling years than the mean of the world which was around 15. 

Africa was then increased to match the average European School years. Once the school years were updated a Time-series model was ran to predict life expectancy for Africa. 

This model showed that when increasing the number of schooling years to match that of Europe, life expectancy greatly increased in Africa by around 6 years.

## Limitation and Next Steps

Altough this project looked at many important variables, there were many not considered. The next project could look at the years 2016-2023. The data does not have to be limited to just UN countries. Other variables could be added such as access to healthcare, or post 2020 data on Covid's impact on life expectancy.

Other area of study could include the differences in gender and life expectancy. Or how the ongoing wars in Ukraine and Israel are impacting life expectancy. There were also columns in the water category that included access to water in hospitals, or personal hygeine. These topics could be explored. 

More data on HIV/AIDs and other diseases can also be analyzed.


# Repo Sturcture
 
├── gitgnore

├── [README.md](https://github.com/jguzzo522/le/blob/main/README.md)

├── [le notebook](https://github.com/jguzzo522/le/blob/main/le.ipynb)

└── [lifeexpectancyslides.pdf](https://github.com/jguzzo522/le/blob/main/lifeexpectancy.pdf)
