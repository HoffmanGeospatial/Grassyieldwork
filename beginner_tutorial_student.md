# Beginner Track Tutorial

## Tutorial Learning Goals

Welcome to the Open Climate Data Science Workshop beginner track tutorial. We are [Nick Gawron](https://www.linkedin.com/in/ngawrondata/) and [Livia Popa](https://www.linkedin.com/in/livia-popa-23a018183/), we will be working with you through today's tutorial.  We will be using R studio for today's session. 

We will be tackling these objectives:

- *Define* open data and reproducible science
- *Describe* how to navigate important aspects of the Notebook Enviornment user-interface for R (and /RStudio if time permits)
- *Recall* how to extract public data from a web portal (Cardinal) and import it into a  data software (R/RStudio)
- *Demonstrate* understanding of dataset and statistical software through exploratory data analysis plots and numerical summaries

### Meet Mr. Wuf!

Mr. Wuf works for Mount Mitchell State Park in Burnsville, NC and was recently asked by his boss to write a report summarizing rainfall and temperature data for 2021. This report will be used to help optimize 2022 event planning (e.g., fall color viewing) for park visitors and maintenance scheduling for park staff. Mr. Wuf’s wife, Mrs. Wuf, recently told him about the State Climate Office of North Carolina’s new Cardinal and Station Scout data portals. He agrees with her that it would be a great opportunity to check out these new, free tools. After some preliminary sleuthing around Station Scout, he discovered there was a National Weather Service Cooperative Observer Program (COOP; https://www.weather.gov/rah/coop) station on park property (station # 315923). How did he miss this? Once he downloads these data from Cardinal, Mr. Wuf plans to put the skills he learned in an online R programming course to the test for this real-world, work-related project.\


![Mr. Wuf](images/mr_wuf.png)

## Open Data Science

### What is Open Data and Reproducible Science?

- Without looking at the section below, how would you define open data? Answer [here](https://www.PollEv.com/ngawron226).

- How would you define reproducible (and open) science? Answer [here](https://www.PollEv.com/ngawron226).

Open data documents and shares research data openly for re-use.

Open data research aims to transform research by pushing change in the way that research is carried out and disseminated by digital tools. Open data should be:

- Publicly available: Open data is freely available on the internet.
- Reusable: Proper licensing is essential for research outputs so that users know any limitations on re-use
- Transparent: With appropriate metadata to explain how research output was produced and what it contains
- You can easily share what you did with your colleagues, collaborators, etc. and it’s easy to make changes and rerun analysis with different settings.


We note that reproducible science is when an authors such as Mr. Wuf would be able to provide all the necessary data and the R code to run their analysis again, re-creating the results. 

When we combine these idea together - we get the goals for this tutorial. 

For more information go to this [handbook](https://the-turing-way.netlify.app/reproducible-research/reproducible-research.html) on the subject. 

## R Basics 

### What are libraries?


- Part of the reason `R` has become so popular is the vast array of packages available at the cran and bioconductor repositories. 

- In the last few years, the number of packages has grown exponentially!

- Helpful tools to do data analysis. 

- Lets Install One: 

Use this code for the first time
`install.packages("ggplot2")`

- Once we have this package installed from the internet, all we need to do in the future on our machine is call it
  - This is done with the `library` command
  - So at the start of your script you should: `library(ggplot2)`


```R
## Now we can set up the environment for this tutorial by loading required libraries

# basic libraries
library(ggplot2) ## this library is for making plots
library(tidyverse) ## this library is for cleaning and processing data
library(lubridate) ## this library is for handling date and time of the data
library(readxl) 

# for advanced pretty plot
library(viridis)     ## color palette
library(ggridges)    ## ridges
library(hrbrthemes)  ## plot theme
```

### Data Types

- Date: this data type is assigned to dates such as 2022-03-02 for March 2, 2022
- Character (also displayed as "chr"): `"a"`, `"NC State"`
- Numeric (real or decimal, also displayed as "num"): `2`, `13.6`
- Integer: `2L` (the `L` tells R to store this as an integer)
- Logical: `TRUE`, `FALSE`
- Complex: `1+4i`(complex numbers with real and imaginary parts)

### Using data Inspection Functions / functions in General 

- A function is helper code that will take an input and give an output

- One useful pair of functions we can use are:  `getwd()` and `setwd()`
  -`getwd()` is a command that tells you the current file location, and where R will save  project files you create. 
  -`setwd()` is a function that will let you input a file directory, in quoted string, inside the parenthesis 
 
- `str` is a powerful function that allows you to determine what kind of variable we are working with

- `length` is a function that tells you how long objects are Examples:


```R
# add 2 and 2 with the sum() function

```


```R
# use the str() function to look at the structure of the input 2

```


```R
# use the str() function to look at the structure of the input "two"

```


```R
# assign a list (1, 2, 3) to the variable wuf using <- or =

```


```R
# check the structure of wuf

```


```R
# look at the length of wuf with the length() function

```


```R
# examine a sample dataset called "iris" that comes with R using the head() function

```


```R
# check the structure of dataset iris


# what is a data frame? it's very similar to a table.
```


```R
# check the length of the sampel dataset "iris"

```

###  Importing From Cardinal

- Cardinal is a high-powered, user-oriented, one-stop-shop for North Carolina weather and climate data housed at the North Carolina State Climate Office. 

- Cardinal makes weather and climate data more accessible to users, with features and prompts that take the guesswork out of station and parameter identification and selection.


![All Cardinal Stations thru North Carolina](images/All_card.PNG)


- This is a great resource for Mr.Wuf!

- We can implement code to import our external data that is already included in this repository (see the panel on the left).
  - The file name is _"raw_cardinal_Data.csv"_.

- A link to the Cardinal Interface is [here](https://products.climate.ncsu.edu/cardinal/).


```R
# read in the coop data from cardinal
raw_coop_data <- read_csv()
```

### Cleaning Data 

- The data in real world are usually a lot more messy.  
- R can handle a lot of small details to help the analysis easy and straightforward.



```R
# drop rows of missing values using the drop_na() function
coop_data ??
```


```R
# determine structure of all cols 

```


```R
# changes the column names
#("date","MaxT_degF","AvgT_degF","MinT_degF","cool_degDays","grow_degDays","heat_degDays","TPrep_in")
```


```R
# create a date column

```


```R
# check structure of all data types

```

## Making New Data

### When does it rain ? 


```R
# Can we make new data to determine when it rains based on the data?
# make a new column called IfRain

```


```R
# change data from TRUE or FALSE to a number (0 or 1) using the as.integer() and then change this to a factor (i.e., categorical variable) using the as.factor() function
# this is an example of nested functions

```


```R
# look at the first 10 rows

```

### Month Factor variable

- Factor variable is a category or bin we can place a value in. 


```R
# create a month column using the month() function and change it to a factor
# (hint: this requires a nested function)

```


```R
# check the structure of the data now

```

###  Numerical Variable, Rain Difference

- Dollar sign + "Name of Variable" can be used to access a column in a data frame
- a data frame is a fancy name for a table (in R)


```R
# create a temperature difference in degrees column using the max and min temperature columns

```


```R
# look at the first 10 rows

```

## Numerical Summaries


### What are they ?

- Help us determine basic trends in data from printouts. 

- Summary gives as a 5 number summary of numeric variables

- Basic counts of factor variables



```R
# use the summary() function to look at a summary of the data

```

- Frequency Table to compare categorical / factor variables.
  - Several kinds!
  - Depends on the number of categorical variables present. 


```R
# use the table() function to produce a frequency table of the IfRain column

```

This table does not look very informative since not everyone knows what "0" and "1" means. So we can change it to make it easier to understand.


```R
# changes level names by assigning no and yes to the levels of the column
# use the levels() function to access the levels of the IfRain column
# Use Sols as the names for the variable labels
Sols <- c("No","Yes")

```


```R
# redisplay the frequency table (hint: see above for the function)

```


```R
# create a two-level table with month and IfRain columns
# name this table tabl2Way

```


```R
# look at two-level table result

```

## Plotting Basics  

### Base R Plotting

- Simple visual of frequency count


```R
# base plots in R, categorical variables does a count using the plot() function

```

- This barplot shows the frequency of how many times it rained vs. did not rain. 
- This is for the entire dataset spanning across all years.
- In standard R, we can create a barplot with a standard table


```R
# plot the two-level table result, add a plot title, and add x and y labels


```

### GGPLOT Plotting

- Base R is limited in usage. 

- We will be using a package called `ggplot2`.

- Here is a good link for [a cheatsheet on common commands](https://www.rstudio.com/resources/cheatsheets/).

- Two basic functions: `ggplot()` & `geom_plottype`
  - Note we have not even had a title or label specs yet 


```R
# create a ggplot figure for time series of heat degree days
# scatter plot
ggplot() + 

```

- This is a scatter plot showing the distribution of Heat Accumulation Days across all years. 
- The highest point is in January of each year. 
- We observes sinusoidal nature

How could we improve this plot?

#### How Would You Modify This?

- Let's say we wanted to plot Max temperature as a scatter plot over time? How would you modify the code from the above block?


```R
# create a ggplot figure for time series of maximum air temperature
ggplot(data = ,)
```

#### plots with *Layers* in ggplot2

- We can also observe correlation and possible trend numerical variables

- Using the cheatsheet, we can find a lot more plot types and Layer Options!

  - Note the use of `labs` statement, we will use that next!
  - Also note that we are creating a line plot!
  


```R
# create a plot of average temperature vs date as a line plot
ggplot(data = ,)
```

- This line graph shows the total average temperature by date. Temperature generally increases in the spring and summer months, with peaks and troughs within each month.

- options are very versatile inside a `+geom_statement()`, or a *plot layer*

- We can use the cheatsheet to find out information about this 

- Note how we change attributes inside the `aes` statement


```R
# plot a histogram of average temperature
# We want the bars filled with organe & outlined in green 
ggplot(data = coop_data,
        mapping = aes()) + 
    geom_histogram() + 
    labs(title = "Histogram of Average Temperature in Lake Wheeler")
# title and all labels included in one more statement 
```

- This histogram shows the average temperature given a count of days. 

- Statistically we see this data is pretty right skewed- something we could look into is if this is the case for all months? (We will look into this later!)

- Below is a scatter plot

- Note we can save our plots with a variable name using the `<-` symbol 


```R
# point plot of max temperature vs min temperature
# Save it as a variable called TempPlot
ggplot(data = )

# show plot

```

- One popular option is to color-code based off of a categorical / factor variable 

- See the difference when we include `aes(col = month)`

    - But where? 



```R
# coloring by month to observe trends

```

- This scatterplot shows the  Maximum temperature recorded in a day against the  minimum temperature recorded. We note this variable is color coded by month. 

#### Categorical Variables on an Axis

- Note we can save our plots with a variable name using the `<-` symbol 


```R
# make a box plot
ggplot(data = coop_data,)

# show the boxplot


# how do we interpret boxplots? what do the different parts of these plots mean?
```

- This is a boxplot of total precipitation within each month. 
- These dots indicate outliers in out data


- What can we do to make this plot better, [answer here](PollEv.com/ngawron226)? 



- We can add edits, with new layers,  to a specific `ggplot2` object


```R
# we can limit the y-axis for the plot to make it better to understand details
??? + labs() + ???
```

- By changing the range of the boxplots we can now see the distribution of the data more easily.

- Only issue is that boxplots can be confusing


- Mr. Wuf wants a more cumulative assessment for rainfall
- We want to create a barplot with total Rain Per Month

- This will require us to go outside of the `cardinal` data set we are working with!


```R
# create a data frame for just this one bar plot!
JustMonthRainTot <- cardinal %>%
    group_by() %>% 
    summarize()
```

- With the new data set we created, `JustMonthRainTot`, we can now create the barplot!



```R
# make a bar plot of monthly rainfall total vs month
ggplot(,)
```

- What do we know about Bar Plots that could help us with this? 

- We somehow need to change how our data is being plotted. Let's look at `?geom_col`


- Thanks to our investigation, Mr.Wuf knows he cannot use `geom_col()` stated as is for this kind of plot. 


To quickly show the power of *ggplot*, observe how we can create this plot without the tidyverse commands from a few boxed above: 


```R
# Use Cardinal Data Set to create the same plot!
# add labels to the previous plot
ggplot(data = cardinal, 
        mapping = aes() + 
    geom_col() + 
    labs(y = "Total Rainfall (in)", x = "Month")
```

We can also use categorical variables on the x-axis, if they relate to a variable in our data frame!


```R
## geom_boxplot() is a great tool to observe spreads in your data
ggplot(data = cardinal,
        mapping = aes()) + 
    
```

- This boxplot shows the range of temperature across each month. In the summer the range decreases, meaning there is less variation in temperature when compared to winter months.

- Box-plots are cumbersome and not super helpful in visualization. 

- How could we improve this boxplot?

### How could we make boxplot better? 

- Note we are looking at average daily temperature


```R
# + geom_boxplot is a great tool to observe spreads
# Add the Variables to that will let us examine the Avergae Temp Acorss Each Month
# We want the box plots to be positions vertically

 ggplot(,)

# show the plot

```

We could add a title and approraite labels! 


```R
# add labels and a title and a theme to the previous plot

```

This is a boxplot showing the spread of average temperature across months. There are a few outliers in some months and the range of values is smaller in the summer.

### Fancy Plot Time

- Inspiration from ggridges documentation

- We want to stylize the boxplot from the above statement       

- We will be using a few libraries here: remember to use `install.packages("library_name")` first before running the library statement. 

- The below panel shows us libraries we need


```R
# add libraries that we'll need for the fancy plots
library(viridis)     ## color palette
library(ggridges)    ## ridges
library(hrbrthemes)  ## plot theme
```

- we will walk you through the ggplot options for this plot!  


```R
# fancy plot!
ggplot(coop_data, aes(x = ??, y = ?? , fill = ..x..)) +
  
  geom_density_ridges_gradient(scale = 2, rel_min_height = 0.01, gradient_lwd = 1.) +
  
  scale_x_continuous(expand = c(0.01, 0)) +
  
  scale_y_discrete(expand = c(0.01, 0)) +
  
  scale_fill_viridis(name = "Temp. [ºF]", option = "C") +
  
  labs(title = 
       subtitle = , 
       x = ) +
  
  theme_ridges(font_size = 13, grid = TRUE) + theme(axis.title.y = element_blank())
```

- This plot shows the distribution of temperature within each month. 

- The density plots are colored by temperature, making it easier to visualize the spread of temperature. 

## Bonus Section

Here we are applying very similar concepts to the tutorial above - with new a new data set! Here we are using an ECOnet station in Raliegh North Carolina. The data we are using this time is called `"cardinal_data.csv"` (see the left panel to find the file).


```R
econet_data_raw <- read_csv("cardinal_data.csv", 
     col_types = list(`Average Air Temperature (F)` = col_number(), 
         `Maximum Air Temperature (F)` = col_number(), 
         `Minimum Air Temperature (F)` = col_number(), 
         `Average Experimental Leaf Wetness (mV)` = col_number(), 
         `Total Precipitation (in)` = col_number(), 
         `Average Relative Humidity (%)` = col_number(), 
         `Average Soil Moisture (m3/m3)` = col_number(), 
         `Average Soil Temperature (F)` = col_number(), 
         `Average Solar Radiation (W/m2)` = col_number(), 
         `Average Station Pressure (mb)` = col_number()))
```

### Cleaning Data 

- usually a lot more messy 
- R can handle a lot of small details 


```R
# drop rows of missing values 
econet_data <- drop_na(econet_data_raw)

#determine data types of all cols 
str(econet_data)
```


```R
#create a date 
econet_data$Date <- as.Date(econet_data$Date, tryFormat s= c("%m/%d/%y"))
head(econet_data, 10)
```


```R
#changes col names
colnames(econet_data) = c("date","AvgT","MaxT","MinT","AvgLw","Tprep","AvgHum","AvgSm","AvgSt","AvgSr","AvgStp")
head(econet_data, 10)
```

### Making New Data

#### When does it Rain ? 


```R
## making new data
econet_data$IfRain <- (econet_data$Tprep>0)
econet_data$IfRain <- as.factor(as.integer(econet_data$IfRain))
head(econet_data, 10)
```

### Month Factor variable

- Factor variable is a category or bin we can place a value in.


```R
# month variable 
econet_data$month <- month(econet_data$date)
econet_data$month <- as.factor(econet_data$month)

# str factor
str(econet_data)
```

###  Numerical Variable, Rain Difference

- Dollar sign + "Name of Variable"


```R
econet_data$TDiff <- econet_data$MaxT - econet_data$MinT
```

### Numerical Summaries

Let's check the summary of the data set


```R
summary(econet_data)
```

Frequency Table to compare categorical / factor variables.


```R
# Frequency Table 
table(econet_data$month, econet_data$IfRain)
```

### Plotting Basics  


- Simple visual of frequency count


```R
# base plots in R, categorical variables
#does a count
plot(econet_data$IfRain, main = 'Frequency Bar Plot of Rain Occurance', xlab = "Occurence of Rain (0-No, 1- Yes)", ylab = "Number of Days")
```

- We will be using a package called `ggplot2`.

- Here is a good link: https://www.rstudio.com/resources/cheatsheets/

- Two basic functions: ggplot() & geom_plottype
  - Note we have not even had a title or label specs yet 


```R
# first ggplot figure

ggplot(econet_data, aes(x = date ,y = AvgLw))+ geom_point()
```

- Maybe show total precip vs month as bar chart.


```R
boxpRain <- ggplot(econet_data, aes(x = month, y = Tprep)) + geom_boxplot()
boxpRain
```

These dots indicate outliers in out data- we can make this plot easier to visualize manually


```R
boxpRain + ylim(0, .75)
```

- Observe correlation and possible trend numerical variables

- Using cheatsheet, we can find a lot more plot types and options!

  - Note the use of `labs` statement


```R
ggplot(econet_data, 
    aes(x = date, y = AvgT)) + 
geom_line() + 
labs(title = "Total Daily Rainfall by Date",
        y = "Average Tempurature (F) ", 
        x =  "Date")

```

- options are very versatile inside a `+geom_statement()`

- We can use the cheatsheet to find out information about this 

- Note how we change atributes inside the `aes` statment


```R
# general plot
ggplot(econet_data, aes(x = AvgHum, y = AvgLw)) +
    geom_point()
```


```R
# coloring by month to observe trends
ggplot(econet_data, aes(x = AvgHum, y = AvgLw)) +
    geom_point(aes(col = month))
```

We can also use categorical variables on the x-axis



```R
# + geom_boxplot is a great tool to observe spreads

ggplot(econet_data, aes(x = month , y = TDiff)) + 
    geom_boxplot()
```

Box-plots are cumbersome and not super helpful in visalization.

### How could we make this boxplot better? 

- Note we are looking at average daily tempurature


```R
# + geom_boxplot is a great tool to observe spreads

ggplot(econet_data, aes(x = month , y = AvgT)) + geom_boxplot()
```

### Extra Bonus Plot Time


- Inspiration from ggridges documentation

- We want to stylize the boxplot from the above statement       

- We will be using a few libraries here: remember to use `install.packages("library_name")` first before running the library statment. 

- we will walk you through the ggplot options for this plot! 



```R
ggplot(econet_data, aes(x = AvgT, y = month, fill = ..x..)) +
  geom_density_ridges_gradient(scale = 2, rel_min_height = 0.01, gradient_lwd = 1.) +
  scale_x_continuous(expand = c(0.01, 0)) +
  scale_y_discrete(expand = c(0.01, 0)) +
  scale_fill_viridis(name = "Temp. [ºF]", option = "C") +
  labs(title = 'Temperatures at Lake Wheeler Station',
       subtitle = 'Mean temperatures (Fahrenheit) by month for 2019-2021\nData: ECOnet Station', 
       x = "Mean Temperature") +
  theme_ridges(font_size = 13, grid = TRUE) + theme(axis.title.y = element_blank())
```

## Closing & Resources

We tackled these objectives:

- *Define* open data and reproducible science
- *Describe* how to navigate important aspects of the R/RStudio user-interface
- *Recall* how to extract public data from a web portal (Cardinal) and import it into a  data software (R/RStudio)
- *Demonstrate* understanding of dataset and statistical software through exploratory data analysis plots and numerical summaries


Which plots do you think Mr. Wuf's boss will especially like for the report? What else should he try to include with a little more work?

### Resouces

- For a A Hydrologists Guide to Open Science, from the HESS Journal, click [here](https://hess.copernicus.org/articles/26/647/2022/). 
- Stepping thru Cardinal [here](https://www.youtube.com/watch?v=UW95MTXEl4k).
- See the attached CSV file in this binder environment: NCSCO Additional Resources.csv

### Survey 

Thank you for attending the beginner track tutorial at the Open Climate Data Science Workshop. Please complete the voluntary feedback survey, linked [here](https://docs.google.com/forms/d/e/1FAIpQLSejTJjhvCLbCVKBotUa8VtDzYJBnMCilzPrB4VBzJrs7vXqIQ/viewform). The main purposes of this survey is to (1) determine we met specified teaching goals and (2) improve teaching materials for subsequent tutorial sessions.
