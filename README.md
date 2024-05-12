# Business Understanding

Life expectancy throughout the world varies drastically amongst countries due to several major factors, including healthcare, education and financial resources. This project predicts variables that affect the increase or decrease of life expectancy. Through the modeling of the project recommendations will be made to inform the United Nations (UN) with data that can lead to developing interventions to increase life expectancy.

![Screen Shot 2024-05-07 at 11 30 22 PM](https://github.com/jguzzo522/le/assets/75549456/5f994a7b-2aaf-4114-ad80-d71a7aec1032)

# Data Understanding

The dataset is from the World Organization of Health (WHO). In the dataset there are 193 countries, or al the countries in the UN, which contains data from 2000-2015. There are 22 columns and 2928 rows. The target variable in this project will be life expectancy.

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
