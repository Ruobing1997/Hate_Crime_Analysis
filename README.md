# DPSS_Summer_Capstone

![UChicago Harris](https://github.com/wang8063/DPSS_Summer_Capstone/blob/master/IMAGES/DPSS.png)
  
  This is the capstone of DPSS in 2019 about Hate Crime in USA which is designed by Daniel Snow

## Background:

  Recent years, according to the FBI or Justice Research and Statistics Association data published, we can see the hate crime rate is increasing and each year, across America, an average of 250,000 people are victimized by hate crimes – criminal expressions of bigotry that terrorize entire communities and fray the social fabric of our country. In order to figure out what is the most important feature in the hate crime and in what extend this feature influences the hate crime rate, we run multi linear regression from income equality, degree, race raio, religious, citizen and non- citizen ratio to build the regression model. As well as demographat and republican ratio and Jewish people.
  
  The purpose of making such a policy is to establish guidelines for identifying and investigating hate crimes and assisting victimized individuals and communities. A swift and strong response by law en- forcement can help stabilize and calm the city as well as aid in a victim’s recovery.

## Main Purpose 
  
  The following is the purpose of this capstone:

  In this Capstone Project, you will examine the potential causes/correlates of hate crimes in the United States. The goal is to replicate this analysis from FiveThirtyEight using updated hate crime data and additional regressors. Prior to starting your project, please read this Southern Poverty Law Center brief which provides background information on hate crimes and hate crime data collection in the United States.
  
  Data for this project will be collected the Kaiser Family Foundation, FBI, and U.S. Census. You will also need to gather two additional state-level metrics to include in your analysis (from any source).
  
In two pages, describe the nature of hate crime data in the United States, including how it is collected and its potential biases (1-2 paragraphs). Next, describe your findings from the tasks below (3-4 paragraphs). Clearly outline your regression specification and detail why you chose your two additional regressors. Suc- cinctly interpret your map as well, noting any geographic anomalies and their potential causes. Embed your regression table, map, and plot in your final memo.

In this project, you can expenct to see how I answer the following questions:

## Tasks:

* 1. loading data and combine the acs and all other variables

* 2. Create a regression incorporating each of your downloaded variables and think about do we need interaction terms? Fixed effects? Include the results of our regression as a nicely formatted table using stargazer.

* 3. Using state-level geographic data from the Census, create a map of hate crimes per 100k population. It should look close to the map in the original article, but with a different style/theme and with potentially different trends.

* 4. Create one additional non-map plot using your state-level data. Try to make something that is mean- ingful and visually striking. Here is where your choice of regressor can really have a large benefit.

* 5. using the FBI hate crimes website, gather the aggregate number of hate crimes for each year since 2008 and create a plot that displays the change in hate crimes per 100k over time.


### Environment

We will mainly use R studio and the version of R for this project is 3.6.0. And use the packages of tidyverse, tidycensus and ggplot

```{r include=FALSE, warning=FALSE, message=FALSE}
library(tm)
library(SnowballC)
library(wordcloud)
library(RColorBrewer)
library(tidyverse)
library(tidycensus)
library(stargazer)
library(ggplot2)
library(gganimate)
library(ggrepel)
library(reshape2)
```

These are all the packages for this project you can install in this way:

### Installing

```r
install.packages("tidyverse")
install.packages("tidycensus")
install.packages("ggplot")
```

And after these steps, we are good to go!

## Loading data:

At first I loaded the acs data of 2016 by the state level which includes the total population. By using the total population we can get unemploy rate,  only high school degree rate, and white people below the poverty line rate, and the people who has the median household income rate.

## Data

  We will use the data from 2016 ACS 5-year data for Census variables and 2017 data for
  
  * [GINI index](https://factfinder.census.gov/bkmk/table/1.0/en/ACS/17_1YR/B19083/0100000US.04000)
  * [Pct. of pop. that is non-citizen](https://www.kff.org/a4327ef/)
  * [Avg. annual hate crimes per 100k pop.](https://ucr.fbi.gov/hate-crime/2017/topic-pages/jurisdiction)
  * [Jewish and Democrat](https://www.gallup.com/home.aspx)
  
  And then combine these variables to one dataframe.

## Glimpse of the Hate Crime

At the very begining, I randomly grab the article about the hate crime from website and use Natural Language Process to see what causes people have the hate crime and in what situation people will think about the hate crime:

![CloudWord](https://github.com/wang8063/DPSS_Summer_Capstone/blob/master/IMAGES/WechatIMG2.jpeg)

(You really hate trump, don’t you?)

We can see the words: University, Muslim, State, etc are very common in the hate crime. Thus, I will use the varibles about degree, race, and religous from the state level and build our regression model. 

In order to build our model, we need to load all of the variables we need and try to combine them in a single dataframe:

## Exploratory Data Analysis:

In this part, I will talk about how I load the data and will give a breifly overview of the data.

At first, I loaded the ACS data of 2016 by the state level, which includes the total population. By using the entire community, we can get the unemploy rate, only a high school degree rate, and white people below the poverty line rate, and the people who have the median household income rate. And then, I loaded the data of the Gini index, which can enhance the income inequality. And, similarly, loading the data of the noncitizen. At last, combine all the datasets we collect together. My goal is creating a dataset, which is a panel data from 2012-2016. Also, for plotting, I will create a Hate Crime data from 2008- 2017.

When I collected the data, I found the potential bias is from the following two parts:

The data about the annual hate crimes we are using is from the FBI, which collected from law enforcement agencies. However, these data are collected spontaneously which means the data can be potentially fake or not precise. Also, we do not have the data from Hawaii, and these data are collected on only prosecutable hate crimes. Sometimes the hate crime is complicated to characterize the hate crime.

On the other hand, the data from the Southern Poverty Law Center combine both hate crimes and hate incidents, but the news reports that strengthen hate after the election may encourage people to report incidents that they would not have reported which will cause awareness bias. Do not even say some local officials do not have the training to tell what the hate crime is.

## The Hate Crime over all the USA

![Whole USA]()

In some states, in recent years, the hate crime has a huge fluctuation, and some states suffering high hate crime rate. We can see that Kentucky has a severe problem in the hate crime, and Massachusetts New Jersey, Vermont, and Washington have the highest average annual hate crimes. Also, for the state, Alabama, North Dakota, etc. They have a vast difference year to year.


![Highest](https://github.com/wang8063/DPSS_Summer_Capstone/blob/master/IMAGES/Highest%20Average%20Annual%20Hate%20Crimes.png)
![Lowest](https://github.com/wang8063/DPSS_Summer_Capstone/blob/master/IMAGES/Lowest%20Average%20Annual%20Hate%20Crimes.png)
![overall](https://github.com/wang8063/DPSS_Summer_Capstone/blob/master/IMAGES/Hate%20Crimes%20overall.png)

### The trend of the hate crime from 2012- 2016

![trend](https://github.com/wang8063/DPSS_Summer_Capstone/blob/master/IMAGES/Hate%20Crime%20Changes%20by%20State(2008-2017).png)

But why? What kind of factors influence these states? To solve this question, I create a regres- sion model.
Before creating the model, we need to check the correlation between each variable we will use:

![Correlation table](https://github.com/wang8063/DPSS_Summer_Capstone/blob/master/IMAGES/correlation.png)

It is no surprise to see that the white people who have meager income related to the median income but, surprisingly, the Gini index has no relationship with people who own high school degree only. I think this is suspicious and keep this idea in mind.

## Model

![stargazer table](https://github.com/wang8063/DPSS_Summer_Capstone/blob/master/IMAGES/WechatIMG5.png)

From the result, we can see that the income inequality play an important role in the Hate Crime Rate.

![regression line](https://github.com/wang8063/DPSS_Summer_Capstone/blob/master/IMAGES/WechatIMG6.png)

## gganimation

![Animation!](https://github.com/wang8063/DPSS_Summer_Capstone/blob/master/IMAGES/file17d1025388fca.gif)

![LGBT](https://github.com/wang8063/DPSS_Summer_Capstone/blob/master/IMAGES/LGBT%20HATE%20CRIME.gif)

## Recommendations

Our goal is to reduce or fix income inequality. Thus, we can do this from the following policies: 

 - Education policies matter. We can see from the correlation table; high degree always leads to top pay.

 - Well-designed labor market policies and institutions.

 - Removing product market regulations that stifle competition can reduce labor income inequality by boosting employment.
 
 - Tax and transfer systems play a crucial role in lowering overall income inequality. 
 
 - The personal income tax. We can apply the tax rate classification system.
 
## Authors

* **Ruobing Wang** - *Initial work* - [Ruobing Wang's website](https://github.com/wang8063)

## Thanks

* **Dan Snow** [!Dan's Github](https://github.com/dfsnow)

