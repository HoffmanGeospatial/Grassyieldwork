# Beginner Track Tutorial

## Tutorial Learning Goals

Welcome to the Open Climate Data Science Workshop beginner track tutorial. We are [Nick Gawron](https://www.linkedin.com/in/ngawrondata/) and [Livia Popa](https://www.linkedin.com/in/livia-popa-23a018183/), we will be working with you through today's tutorial.  We will be using R studio for today's session. 

We will be tackling these objectives:

- *Define* open data and reproducible science
- *Describe* how to navigate important aspects of the R/RStudio user-interface
- *Recall* how to extract public data from a web portal (Cardinal) and import it into a  data software (R/RStudio)
- *Demonstrate* understanding of dataset and statistical software through exploratory data analysis plots and numerical summaries

### Meet Mr. Wuf!

Mr. Wuf works for Mount Mitchell State Park in Burnsville, NC and was recently asked by his boss to write a report summarizing rainfall and temperature data for 2021. This report will be used to help optimize 2022 event planning (e.g., fall color viewing) for park visitors and maintenance scheduling for park staff. Mr. Wuf’s wife, Mrs. Wuf, recently told him about the State Climate Office of North Carolina’s new Cardinal and Station Scout data portals. He agrees with her that it would be a great opportunity to check out these new, free tools. After some preliminary sleuthing around Station Scout, he discovered there was a National Weather Service Cooperative Observer Program (COOP; https://www.weather.gov/rah/coop) station on park property (station # 315923). How did he miss this? Once he downloads these data from Cardinal, Mr. Wuf plans to put the skills he learned in an online R programming course to the test for this real-world, work-related project.\


![Mr. Wuf](images/mr_wuf.png)

## Open Data Science

### What is Open Data and Reproducible Science?

- Without looking at the section below, how would you define open data?

- How would you define reproducible (and open) science?

Open data documents and shares research data openly for re-use.

Open data research aims to transform research by pushing change in the way that research is carried out and disseminated by digital tools. Open data should be:

- Publicly available: Open data is freely available on the internet.
- Reusable: Proper licensing is essential for research outputs so that users know any limitations on re-use
- Transparent: With appropriate metadata to explain how research output was produced and what it contains
- You can easily share what you did with your colleagues, collaborators, etc. and it’s easy to make changes and rerun analysis with different settings.


We note that reproducible science is when an authors such as Mr. Wuf would be able to provide all the necessary data and the R code to run their analysis again, re-creating the results. 

When we combine these ideas together - we get the goals for this tutorial. 

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

    ── [1mAttaching packages[22m ─────────────────────────────────────── tidyverse 1.3.1 ──
    
    [32m✔[39m [34mtibble [39m 3.1.6     [32m✔[39m [34mdplyr  [39m 1.0.7
    [32m✔[39m [34mtidyr  [39m 1.1.4     [32m✔[39m [34mstringr[39m 1.4.0
    [32m✔[39m [34mreadr  [39m 2.1.2     [32m✔[39m [34mforcats[39m 0.5.1
    [32m✔[39m [34mpurrr  [39m 0.3.4     
    
    ── [1mConflicts[22m ────────────────────────────────────────── tidyverse_conflicts() ──
    [31m✖[39m [34mdplyr[39m::[32mfilter()[39m masks [34mstats[39m::filter()
    [31m✖[39m [34mdplyr[39m::[32mlag()[39m    masks [34mstats[39m::lag()
    
    
    Attaching package: ‘lubridate’
    
    
    The following objects are masked from ‘package:base’:
    
        date, intersect, setdiff, union
    
    
    Loading required package: viridisLite
    
    NOTE: Either Arial Narrow or Roboto Condensed fonts are required to use these themes.
    
          Please use hrbrthemes::import_roboto_condensed() to install Roboto Condensed and
    
          if Arial Narrow is not on your system, please see https://bit.ly/arialnarrow
    


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
sum(2, 2)
```


4



```R
# use the str() function to look at the structure of the input 2
str(2)
```

     num 2



```R
# use the str() function to look at the structure of the input "two"
str("two")
```

     chr "two"



```R
# assign a list (1, 2, 3) to the variable wuf using <- or =
wuf <- c(1, 2, 3)
wuf = c(1, 2, 3)
```

     num [1:3] 1 2 3



```R
# check the structure of wuf
str(wuf)
```


```R
# look at the length of wuf with the length() function
length(wuf)
```


3



```R
# examine a sample dataset called "iris" that comes with R using the head() function
head(iris)
```


<table class="dataframe">
<caption>A data.frame: 6 × 5</caption>
<thead>
	<tr><th></th><th scope=col>Sepal.Length</th><th scope=col>Sepal.Width</th><th scope=col>Petal.Length</th><th scope=col>Petal.Width</th><th scope=col>Species</th></tr>
	<tr><th></th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;fct&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>5.1</td><td>3.5</td><td>1.4</td><td>0.2</td><td>setosa</td></tr>
	<tr><th scope=row>2</th><td>4.9</td><td>3.0</td><td>1.4</td><td>0.2</td><td>setosa</td></tr>
	<tr><th scope=row>3</th><td>4.7</td><td>3.2</td><td>1.3</td><td>0.2</td><td>setosa</td></tr>
	<tr><th scope=row>4</th><td>4.6</td><td>3.1</td><td>1.5</td><td>0.2</td><td>setosa</td></tr>
	<tr><th scope=row>5</th><td>5.0</td><td>3.6</td><td>1.4</td><td>0.2</td><td>setosa</td></tr>
	<tr><th scope=row>6</th><td>5.4</td><td>3.9</td><td>1.7</td><td>0.4</td><td>setosa</td></tr>
</tbody>
</table>




```R
# check the structure of dataset iris
str(iris)

# what is a data frame? it's very similar to a table.
```

    'data.frame':	150 obs. of  5 variables:
     $ Sepal.Length: num  5.1 4.9 4.7 4.6 5 5.4 4.6 5 4.4 4.9 ...
     $ Sepal.Width : num  3.5 3 3.2 3.1 3.6 3.9 3.4 3.4 2.9 3.1 ...
     $ Petal.Length: num  1.4 1.4 1.3 1.5 1.4 1.7 1.4 1.5 1.4 1.5 ...
     $ Petal.Width : num  0.2 0.2 0.2 0.2 0.2 0.4 0.3 0.2 0.2 0.1 ...
     $ Species     : Factor w/ 3 levels "setosa","versicolor",..: 1 1 1 1 1 1 1 1 1 1 ...



```R
# check the length of the sampel dataset "iris"
length(iris)
```


5


###  Importing From Cardinal

- Cardinal is a high-powered, user-oriented, one-stop-shop for North Carolina weather and climate data housed at the North Carolina State Climate Office. 

- Cardinal makes weather and climate data more accessible to users, with features and prompts that take the guesswork out of station and parameter identification and selection.

- This is a great resource for Mr.Wuf!

- We can implement code to import our external data that is already included in this repository (see the panel on the left).
  - The file name is _"raw_coop_Data.csv"_.

- A link to the Cardinal Interface is [here](https://products.climate.ncsu.edu/cardinal/).


```R
# read in the coop data from cardinal
raw_coop_data <- readr::read_csv("raw_coop_data.csv", col_types = cols(Date = col_character()))
```

### Cleaning Data 

- The data in real world are usually a lot more messy.  
- R can handle a lot of small details to help the analysis easy and straightforward.



```R
# drop rows of missing values using the drop_na() function
coop_data <- drop_na(raw_coop_data)
```

    tibble [1,097 × 8] (S3: tbl_df/tbl/data.frame)
     $ Date                                                    : chr [1:1097] "2019-01-01" "2019-01-02" "2019-01-03" "2019-01-04" ...
     $ Maximum Air Temperature (F)                             : num [1:1097] 48 44 46 44 44 33 47 41 43 22 ...
     $ Mid-Range Air Temperature (F)                           : num [1:1097] 42 40 39.5 40 33.5 28 39.5 37 29 14 ...
     $ Minimum Air Temperature (F)                             : num [1:1097] 36 36 33 36 23 23 32 33 15 6 ...
     $ Accumulated Cooling Degree Days - Base 65F (Degree Days): num [1:1097] 0 0 0 0 0 0 0 0 0 0 ...
     $ Accumulated Growing Degree Days - Base 50F (Degree Days): num [1:1097] 0 0 0 0 0 0 0 0 0 0 ...
     $ Accumulated Heating Degree Days - Base 65F (Degree Days): num [1:1097] 23 25 25.5 25 31.5 ...
     $ Total Precipitation (in)                                : num [1:1097] 0.3 0.03 0.63 0.34 1 0 0 0 0 0 ...
    tibble [1,097 × 8] (S3: tbl_df/tbl/data.frame)
     $ date        : Date[1:1097], format: "2019-01-01" "2019-01-02" ...
     $ MaxT_degF   : num [1:1097] 48 44 46 44 44 33 47 41 43 22 ...
     $ AvgT_degF   : num [1:1097] 42 40 39.5 40 33.5 28 39.5 37 29 14 ...
     $ MinT_degF   : num [1:1097] 36 36 33 36 23 23 32 33 15 6 ...
     $ cool_degDays: num [1:1097] 0 0 0 0 0 0 0 0 0 0 ...
     $ grow_degDays: num [1:1097] 0 0 0 0 0 0 0 0 0 0 ...
     $ heat_degDays: num [1:1097] 23 25 25.5 25 31.5 ...
     $ TPrep_in    : num [1:1097] 0.3 0.03 0.63 0.34 1 0 0 0 0 0 ...



```R
# determine structure of all cols 
str(raw_coop_data)
```


```R
# changes the column names
colnames(coop_data) <- c("date","MaxT_degF","AvgT_degF","MinT_degF","cool_degDays","grow_degDays","heat_degDays","TPrep_in")
```


```R
# create a date column
coop_data$date <- as.Date(coop_data$date)
```


```R
# check structure of all data types
str(coop_data)
```

## Making New Data

### When does it rain ? 


```R
# Can we make new data to determine when it rains based on the data?
# make a new column called IfRain
coop_data$IfRain <- (coop_data$TPrep_in > 0)
```


<table class="dataframe">
<caption>A tibble: 10 × 11</caption>
<thead>
	<tr><th scope=col>date</th><th scope=col>MaxT_degF</th><th scope=col>AvgT_degF</th><th scope=col>MinT_degF</th><th scope=col>cool_degDays</th><th scope=col>grow_degDays</th><th scope=col>heat_degDays</th><th scope=col>TPrep_in</th><th scope=col>IfRain</th><th scope=col>month</th><th scope=col>TDiff_degF</th></tr>
	<tr><th scope=col>&lt;date&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2019-01-01</td><td>48</td><td>42.0</td><td>36</td><td>0</td><td>0</td><td>22.99</td><td>0.30</td><td>1</td><td>1</td><td>12</td></tr>
	<tr><td>2019-01-02</td><td>44</td><td>40.0</td><td>36</td><td>0</td><td>0</td><td>25.01</td><td>0.03</td><td>1</td><td>1</td><td> 8</td></tr>
	<tr><td>2019-01-03</td><td>46</td><td>39.5</td><td>33</td><td>0</td><td>0</td><td>25.49</td><td>0.63</td><td>1</td><td>1</td><td>13</td></tr>
	<tr><td>2019-01-04</td><td>44</td><td>40.0</td><td>36</td><td>0</td><td>0</td><td>25.01</td><td>0.34</td><td>1</td><td>1</td><td> 8</td></tr>
	<tr><td>2019-01-05</td><td>44</td><td>33.5</td><td>23</td><td>0</td><td>0</td><td>31.51</td><td>1.00</td><td>1</td><td>1</td><td>21</td></tr>
	<tr><td>2019-01-06</td><td>33</td><td>28.0</td><td>23</td><td>0</td><td>0</td><td>37.00</td><td>0.00</td><td>0</td><td>1</td><td>10</td></tr>
	<tr><td>2019-01-07</td><td>47</td><td>39.5</td><td>32</td><td>0</td><td>0</td><td>25.49</td><td>0.00</td><td>0</td><td>1</td><td>15</td></tr>
	<tr><td>2019-01-08</td><td>41</td><td>37.0</td><td>33</td><td>0</td><td>0</td><td>28.00</td><td>0.00</td><td>0</td><td>1</td><td> 8</td></tr>
	<tr><td>2019-01-09</td><td>43</td><td>29.0</td><td>15</td><td>0</td><td>0</td><td>36.01</td><td>0.00</td><td>0</td><td>1</td><td>28</td></tr>
	<tr><td>2019-01-10</td><td>22</td><td>14.0</td><td> 6</td><td>0</td><td>0</td><td>51.00</td><td>0.00</td><td>0</td><td>1</td><td>16</td></tr>
</tbody>
</table>




```R
# change data from TRUE or FALSE to a number (0 or 1) using the as.integer() and then change this to a factor (i.e., categorical variable) using the as.factor() function
# this is an example of nested functions
coop_data$IfRain <- as.factor(as.integer(coop_data$IfRain))
```


```R
# look at the first 10 rows
head(coop_data, 10)
```

### Month Factor variable

- Factor variable is a category or bin we can place a value in. 


```R
# create a month column using the month() function and change it to a factor
# (hint: this requires a nested function)
coop_data$month <- as.factor(month(coop_data$date))
```

    tibble [1,097 × 11] (S3: tbl_df/tbl/data.frame)
     $ date        : Date[1:1097], format: "2019-01-01" "2019-01-02" ...
     $ MaxT_degF   : num [1:1097] 48 44 46 44 44 33 47 41 43 22 ...
     $ AvgT_degF   : num [1:1097] 42 40 39.5 40 33.5 28 39.5 37 29 14 ...
     $ MinT_degF   : num [1:1097] 36 36 33 36 23 23 32 33 15 6 ...
     $ cool_degDays: num [1:1097] 0 0 0 0 0 0 0 0 0 0 ...
     $ grow_degDays: num [1:1097] 0 0 0 0 0 0 0 0 0 0 ...
     $ heat_degDays: num [1:1097] 23 25 25.5 25 31.5 ...
     $ TPrep_in    : num [1:1097] 0.3 0.03 0.63 0.34 1 0 0 0 0 0 ...
     $ IfRain      : Factor w/ 2 levels "0","1": 2 2 2 2 2 1 1 1 1 1 ...
     $ month       : Factor w/ 12 levels "1","2","3","4",..: 1 1 1 1 1 1 1 1 1 1 ...
     $ TDiff_degF  : num [1:1097] 12 8 13 8 21 10 15 8 28 16 ...



```R
# check the structure of the data now
str(coop_data)
```

###  Numerical Variable, Rain Difference

- Dollar sign + "Name of Variable" can be used to access a column in a data frame
- a data frame is a fancy name for a table (in R)


```R
# create a temperature difference in degrees column using the max and min temperature columns
coop_data$TDiff_degF <- coop_data$MaxT_degF - coop_data$MinT_degF
```


<table class="dataframe">
<caption>A tibble: 10 × 11</caption>
<thead>
	<tr><th scope=col>date</th><th scope=col>MaxT_degF</th><th scope=col>AvgT_degF</th><th scope=col>MinT_degF</th><th scope=col>cool_degDays</th><th scope=col>grow_degDays</th><th scope=col>heat_degDays</th><th scope=col>TPrep_in</th><th scope=col>IfRain</th><th scope=col>month</th><th scope=col>TDiff_degF</th></tr>
	<tr><th scope=col>&lt;date&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2019-01-01</td><td>48</td><td>42.0</td><td>36</td><td>0</td><td>0</td><td>22.99</td><td>0.30</td><td>1</td><td>1</td><td>12</td></tr>
	<tr><td>2019-01-02</td><td>44</td><td>40.0</td><td>36</td><td>0</td><td>0</td><td>25.01</td><td>0.03</td><td>1</td><td>1</td><td> 8</td></tr>
	<tr><td>2019-01-03</td><td>46</td><td>39.5</td><td>33</td><td>0</td><td>0</td><td>25.49</td><td>0.63</td><td>1</td><td>1</td><td>13</td></tr>
	<tr><td>2019-01-04</td><td>44</td><td>40.0</td><td>36</td><td>0</td><td>0</td><td>25.01</td><td>0.34</td><td>1</td><td>1</td><td> 8</td></tr>
	<tr><td>2019-01-05</td><td>44</td><td>33.5</td><td>23</td><td>0</td><td>0</td><td>31.51</td><td>1.00</td><td>1</td><td>1</td><td>21</td></tr>
	<tr><td>2019-01-06</td><td>33</td><td>28.0</td><td>23</td><td>0</td><td>0</td><td>37.00</td><td>0.00</td><td>0</td><td>1</td><td>10</td></tr>
	<tr><td>2019-01-07</td><td>47</td><td>39.5</td><td>32</td><td>0</td><td>0</td><td>25.49</td><td>0.00</td><td>0</td><td>1</td><td>15</td></tr>
	<tr><td>2019-01-08</td><td>41</td><td>37.0</td><td>33</td><td>0</td><td>0</td><td>28.00</td><td>0.00</td><td>0</td><td>1</td><td> 8</td></tr>
	<tr><td>2019-01-09</td><td>43</td><td>29.0</td><td>15</td><td>0</td><td>0</td><td>36.01</td><td>0.00</td><td>0</td><td>1</td><td>28</td></tr>
	<tr><td>2019-01-10</td><td>22</td><td>14.0</td><td> 6</td><td>0</td><td>0</td><td>51.00</td><td>0.00</td><td>0</td><td>1</td><td>16</td></tr>
</tbody>
</table>




```R
# look at the first 10 rows
head(coop_data, 10)
```

## Numerical Summaries


### What are they ?

- Help us determine basic trends in data from printouts. 

- Summary gives as a 5 number summary of numeric variables

- Basic counts of factor variables



```R
# use the summary() function to look at a summary of the data
summary(coop_data)
```


          date              MaxT_degF       AvgT_degF       MinT_degF    
     Min.   :2019-01-01   Min.   : 8.00   Min.   : 5.00   Min.   :-7.00  
     1st Qu.:2019-10-02   1st Qu.:44.00   1st Qu.:35.00   1st Qu.:26.00  
     Median :2020-07-02   Median :55.00   Median :47.00   Median :39.00  
     Mean   :2020-07-02   Mean   :53.17   Mean   :45.08   Mean   :36.99  
     3rd Qu.:2021-04-02   3rd Qu.:65.00   3rd Qu.:57.00   3rd Qu.:50.00  
     Max.   :2022-01-01   Max.   :75.00   Max.   :66.50   Max.   :58.00  
                                                                         
      cool_degDays     grow_degDays     heat_degDays      TPrep_in     IfRain 
     Min.   :0.0000   Min.   : 0.000   Min.   : 0.00   Min.   :0.000   0:597  
     1st Qu.:0.0000   1st Qu.: 0.000   1st Qu.: 8.00   1st Qu.:0.000   1:500  
     Median :0.0000   Median : 0.000   Median :18.01   Median :0.000          
     Mean   :0.0032   Mean   : 3.349   Mean   :19.92   Mean   :0.253          
     3rd Qu.:0.0000   3rd Qu.: 7.000   3rd Qu.:29.99   3rd Qu.:0.220          
     Max.   :1.5100   Max.   :16.510   Max.   :60.00   Max.   :9.200          
                                                                              
         month       TDiff_degF   
     1      : 94   Min.   : 2.00  
     3      : 93   1st Qu.:12.00  
     5      : 93   Median :16.00  
     7      : 93   Mean   :16.18  
     8      : 93   3rd Qu.:19.00  
     10     : 93   Max.   :44.00  
     (Other):538                  


- Frequency Table to compare categorical / factor variables.
  - Several kinds!
  - Depends on the number of categorical variables present. 


```R
# use the table() function to produce a frequency table of the IfRain column
table(coop_data$IfRain)
```


    
      0   1 
    597 500 


This table does not look very informative since not everyone knows what "0" and "1" means. So we can change it to make it easier to understand.


```R
# changes level names by assigning no and yes to the levels of the column
# use the levels() function to access the levels of the IfRain column
levels(coop_data$IfRain) < -c("No", "Yes")
```


    
     No Yes 
    597 500 



```R
# redisplay the frequency table (hint: see above for the function)
table(coop_data$IfRain)
```


```R
# create a two-level table with month and IfRain columns
tabl2Way <- table(coop_data$month, coop_data$IfRain)
```


        
         No Yes
      1  51  43
      2  41  44
      3  50  43
      4  56  34
      5  52  41
      6  43  47
      7  35  58
      8  35  58
      9  51  39
      10 57  36
      11 66  24
      12 60  33



```R
# look at two-level table result
tabl2Way
```

## Plotting Basics  

### Base R Plotting

- Simple visual of frequency count


```R
# base plots in R, categorical variables does a count using the plot() function
plot(coop_data$IfRain)
```


    
![png](output_45_0.png)
    


- This barplot shows the frequency of how many times it rained vs. did not rain. 
- This is for the entire dataset spanning across all years.
- In standard R, we can create a barplot with a standard table


```R
# plot the two-level table result, add a plot title, and add x and y labels
plot(tabl2Way,
    main ='Proportion Bar Plot of Rain Occurrence',
    xlab = "Occurrence of Rain (0-No, 1- Yes)",
    ylab = "Proportion of Days")

```


    
![png](output_47_0.png)
    


### GGPLOT Plotting

- Base R is limited in usage. 

- We will be using a package called `ggplot2`.

- Here is a good link: https://www.rstudio.com/resources/cheatsheets/

- Two basic functions: `ggplot()` & `geom_plottype`
  - Note we have not even had a title or label specs yet 


```R
# create a ggplot figure for time series of heat degree days
ggplot(data = coop_data,
    mapping = aes(x = date, y = heat_degDays)) + 
geom_point()
```


    
![png](output_49_0.png)
    


- This is a scatter plot showing the distribution of Heat Accumulation Days across all years. 
- The highest point is in January of each year. 
- We observes sinusoidal nature

How could we improve this plot?

#### How Would You Modify This?

- Let's say we wanted to plot Max temperature as a scatter plot over time? How would you modify the code from the above block?


```R
# create a ggplot figure for time series of maximum air temperature
ggplot(data = coop_data,
    mapping = aes(x = date ,y = MaxT_degF)) + 
geom_point()
```


    
![png](output_52_0.png)
    


#### plots with *Layers* in ggplot2

- We can also observe correlation and possible trend numerical variables

- Using the cheatsheet, we can find a lot more plot types and Layer Options!

  - Note the use of `labs` statement, we will use that next!


```R
# create a plot of average temperature vs date as a line plot
ggplot(data = coop_data,
        mapping = aes(x = date, y = AvgT_degF)) + 
    geom_line() + 
    labs(title = "Total Average Temperature by Date",
        x = "Date",
        y = "Average Temperature (F) ")
```


    
![png](output_54_0.png)
    


- This line graph shows the total average temperature by date. Temperature generally increases in the spring and summer months, with peaks and troughs within each month.

- options are very versatile inside a `+geom_statement()`, or a *plot layer*

- We can use the cheatsheet to find out information about this 

- Note how we change attributes inside the `aes` statement


```R
# plot a histogram of average temperature
ggplot(data = coop_data,
        mapping = aes(x=AvgT_degF)) + 
    geom_histogram(color = "green", fill = "orange") + 
    labs(x = "Average Temperature", y = "Day",
         title = "Histogram of Average Temperature in Lake Wheeler")
# title and all labels included in one more statement 
```

    `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
    



    
![png](output_56_1.png)
    


- This histogram shows the average temperature given a count of days. 

- Statistically we see this data is pretty right skewed- something we could look into is if this is the case for all months? (We will look into this later!)

- Below is a scatter plot

- Note we can save our plots with a variable name using the `<-` symbol 


```R
# point plot of max temperature vs min temperature
TempPlot <- ggplot(data = coop_data, 
        mapping = aes(x=MinT_degF,y=MaxT_degF)) + 
    geom_point()

# show plot
TempPlot
```


    
![png](output_58_0.png)
    


- One popular option is to color-code based off of a categorical / factor variable 

- See the difference when we include `aes(col = month)`



```R
# coloring by month to observe trends
ggplot(data = coop_data,
    mapping = aes(x = MinT_degF, y = MaxT_degF)) + 
    geom_point(aes(col = 
    month))
```


    
![png](output_60_0.png)
    


- This scatterplot shows the  Maximum temperature recorded in a day against the  minimum temperature recorded. We note this variable is color coded by month. 

#### Categorical Variables on an Axis

- Note we can save our plots with a variable name using the `<-` symbol 


```R
# make a box plot
boxpRain <- ggplot(data = coop_data,
        mapping = aes(x = month, y = TPrep_in)) +
    geom_boxplot()

# show the boxplot
boxpRain

# how do we interpret boxplots? what do the different parts of these plots mean?
```


    
![png](output_63_0.png)
    


- This is a boxplot of total precipitation within each month. 
- These dots indicate outliers in out data

- We can add edits, with new layers,  to a specific `ggplot2` object


```R
# we can limit the y-axis for the plot to make it better to understand details
boxpRain + ylim(0, 1.25) + labs()
```

    Warning message:
    “Removed 54 rows containing non-finite values (stat_boxplot).”



    
![png](output_65_1.png)
    


- By changing the range of the boxplots we can now see the distribution of the data more easily.

- Only issue is that boxplots can be confusing


- Mr. Wuf wants a more cumulative assessment for rainfall
- We want to create a barplot with total Rain Per Month

- This will require us to go outside of the `cardinal` data set we are working with!


```R
# create a data frame for just this one bar plot!
JustMonthRainTot <- coop_data %>%
    group_by(month) %>% 
    summarize(Rain = sum(TPrep_in))
```

    tibble [12 × 2] (S3: tbl_df/tbl/data.frame)
     $ month: Factor w/ 12 levels "1","2","3","4",..: 1 2 3 4 5 6 7 8 9 10 ...
     $ Rain : num [1:12] 21.9 27.1 17.3 23.3 21 ...


- With the new data set we created, `JustMonthRainTot`, we can now create the barplot!



```R
# make a bar plot of monthly rainfall total vs month
ggplot(data = JustMonthRainTot,
        mapping = aes(x = month, y = Rain)) + 
    geom_col() + 
    labs(y = "Total Rainfall (in)",x = "Month")
```


    
![png](output_69_0.png)
    


- What do we know about Bar Plots that could help us with this? **Text Poll Link Here**

- We somehow need to change how our data is being plotted. Let's look at `?geom_col`


- Thanks to our investigation, Mr.Wuf knows he cannot use `geom_col()` stated as is for this kind of plot. 


To quickly show the power of *ggplot*, observe how we can create this plot without the tidyverse commands from a few boxed above: 


```R
# add labels to the previous plot
ggplot(data = coop_data, 
        mapping = aes(x = month, y = TPrep_in)) + 
    geom_col() + 
    labs(y = "Total Rainfall (in)", x = "Month")
```


    
![png](output_72_0.png)
    


We can also use categorical variables on the x-axis, if they relate to a variable in our data frame!


```R
## geom_boxplot() is a great tool to observe spreads in your data
ggplot(data = coop_data,
        mapping = aes(x = month , y = TDiff_degF)) + 
    geom_boxplot()
```


    
![png](output_74_0.png)
    


- This boxplot shows the range of temperature across each month. In the summer the range decreases, meaning there is less variation in temperature when compared to winter months.

- Box-plots are cumbersome and not super helpful in visualization. 

- How could we improve this boxplot?

### How could we make boxplot better? 

- Note we are looking at average daily temperature


```R
# + geom_boxplot is a great tool to observe spreads
tempBox<- ggplot(data = coop_data,
    mapping = aes(x = month , y = AvgT_degF)) +
    geom_boxplot()

# show the plot
tempBox
```


    
![png](output_77_0.png)
    


We could add a title and approraite labels! 


```R
# add labels and a title and a theme to the previous plot
tempBox + 
    labs(x = "Month", y = " Average Temperature (F)",
        title="Distribution of Temperatures By Month") +
    theme_light()
```


    
![png](output_79_0.png)
    


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
ggplot(coop_data, aes(x = AvgT_degF, y = month, fill = ..x..)) +
  
  geom_density_ridges_gradient(scale = 2, rel_min_height = 0.01, gradient_lwd = 1.) +
  
  scale_x_continuous(expand = c(0.01, 0)) +
  
  scale_y_discrete(expand = c(0.01, 0)) +
  
  scale_fill_viridis(name = "Temp. [ºF]", option = "C") +
  
  labs(title = 'Temperatures at  Burnsville NC',
       subtitle = 'Mean temperatures (Fahrenheit) by month for 2020-2021\nData: COOP Station', 
       x = "Mean Temperature") +
  
  theme_ridges(font_size = 13, grid = TRUE) + theme(axis.title.y = element_blank())
```

    Picking joint bandwidth of 2.62
    



    
![png](output_84_1.png)
    


- This plot shows the distribution of temperature within each month. 

- The density plots are colored by temperature, making it easier to visualize the spread of temperature. 

## Bonus Section

Here we are applying very similar concepts to the tutorial above - with new a new data set! Here we are using an ECOnet station in Raliegh North Carolina. The data we are using this time is called `"cardinal_data.csv"` (see the left panel to find the file).


```R
econet_raw <- read_csv("cardinal_data.csv", 
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

    Warning message:
    “One or more parsing issues, see `problems()` for details”


### Cleaning Data 

- usually a lot more messy 
- R can handle a lot of small details 


```R
# drop rows of missing values 
econet_data <- drop_na(econet_raw)

#determine data types of all cols 
str(econet_data)
```

    tibble [729 × 11] (S3: tbl_df/tbl/data.frame)
     $ Date                                  : chr [1:729] "1/1/20" "1/2/20" "1/3/20" "1/4/20" ...
     $ Average Air Temperature (F)           : num [1:729] 43.1 44.9 52.8 57.2 42.1 44.1 41.4 42.5 40.4 52 ...
     $ Maximum Air Temperature (F)           : num [1:729] 53.6 55.4 64.9 65.1 50.5 58.5 52 57.6 50.5 65.8 ...
     $ Minimum Air Temperature (F)           : num [1:729] 35.1 35.2 45.7 42.6 34.9 32 31.3 29.7 31.3 38.1 ...
     $ Average Experimental Leaf Wetness (mV): num [1:729] 266 274 362 373 265 ...
     $ Total Precipitation (in)              : num [1:729] 0 0.05 0.95 0.52 0 0 0.07 0 0 0 ...
     $ Average Relative Humidity (%)         : num [1:729] 63.8 72 92.1 83.5 57 ...
     $ Average Soil Moisture (m3/m3)         : num [1:729] 0.28 0.28 0.29 0.35 0.33 0.31 0.3 0.3 0.3 0.29 ...
     $ Average Soil Temperature (F)          : num [1:729] 48.6 47.6 51 54.6 48.3 46.1 44.6 43.3 43.3 46.1 ...
     $ Average Solar Radiation (W/m2)        : num [1:729] 134.8 66 31.1 44.9 135.4 ...
     $ Average Station Pressure (mb)         : num [1:729] 999 1003 998 993 1005 ...



```R
#create a date 
econet_data$Date <- as.Date(econet_data$Date, tryFormat s= c("%m/%d/%y"))
head(econet_data, 10)
```


<table class="dataframe">
<caption>A tibble: 10 × 11</caption>
<thead>
	<tr><th scope=col>Date</th><th scope=col>Average Air Temperature (F)</th><th scope=col>Maximum Air Temperature (F)</th><th scope=col>Minimum Air Temperature (F)</th><th scope=col>Average Experimental Leaf Wetness (mV)</th><th scope=col>Total Precipitation (in)</th><th scope=col>Average Relative Humidity (%)</th><th scope=col>Average Soil Moisture (m3/m3)</th><th scope=col>Average Soil Temperature (F)</th><th scope=col>Average Solar Radiation (W/m2)</th><th scope=col>Average Station Pressure (mb)</th></tr>
	<tr><th scope=col>&lt;date&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2020-01-01</td><td>43.1</td><td>53.6</td><td>35.1</td><td>265.60</td><td>0.00</td><td>63.79</td><td>0.28</td><td>48.6</td><td>134.78</td><td> 999.13</td></tr>
	<tr><td>2020-01-02</td><td>44.9</td><td>55.4</td><td>35.2</td><td>274.22</td><td>0.05</td><td>71.95</td><td>0.28</td><td>47.6</td><td> 65.96</td><td>1002.54</td></tr>
	<tr><td>2020-01-03</td><td>52.8</td><td>64.9</td><td>45.7</td><td>362.06</td><td>0.95</td><td>92.13</td><td>0.29</td><td>51.0</td><td> 31.10</td><td> 998.46</td></tr>
	<tr><td>2020-01-04</td><td>57.2</td><td>65.1</td><td>42.6</td><td>373.00</td><td>0.52</td><td>83.46</td><td>0.35</td><td>54.6</td><td> 44.91</td><td> 993.43</td></tr>
	<tr><td>2020-01-05</td><td>42.1</td><td>50.5</td><td>34.9</td><td>264.75</td><td>0.00</td><td>56.97</td><td>0.33</td><td>48.3</td><td>135.38</td><td>1004.77</td></tr>
	<tr><td>2020-01-06</td><td>44.1</td><td>58.5</td><td>32.0</td><td>264.68</td><td>0.00</td><td>57.63</td><td>0.31</td><td>46.1</td><td>137.63</td><td>1004.80</td></tr>
	<tr><td>2020-01-07</td><td>41.4</td><td>52.0</td><td>31.3</td><td>273.52</td><td>0.07</td><td>75.20</td><td>0.30</td><td>44.6</td><td> 40.91</td><td>1002.46</td></tr>
	<tr><td>2020-01-08</td><td>42.5</td><td>57.6</td><td>29.7</td><td>313.64</td><td>0.00</td><td>58.86</td><td>0.30</td><td>43.3</td><td>135.65</td><td>1010.30</td></tr>
	<tr><td>2020-01-09</td><td>40.4</td><td>50.5</td><td>31.3</td><td>264.83</td><td>0.00</td><td>60.18</td><td>0.30</td><td>43.3</td><td>121.55</td><td>1022.39</td></tr>
	<tr><td>2020-01-10</td><td>52.0</td><td>65.8</td><td>38.1</td><td>265.81</td><td>0.00</td><td>73.49</td><td>0.29</td><td>46.1</td><td> 74.57</td><td>1019.34</td></tr>
</tbody>
</table>




```R
#changes col names
colnames(econet_data) = c("date","AvgT","MaxT","MinT","AvgLw","Tprep","AvgHum","AvgSm","AvgSt","AvgSr","AvgStp")
head(econet_data, 10)
```


<table class="dataframe">
<caption>A tibble: 10 × 11</caption>
<thead>
	<tr><th scope=col>date</th><th scope=col>AvgT</th><th scope=col>MaxT</th><th scope=col>MinT</th><th scope=col>AvgLw</th><th scope=col>Tprep</th><th scope=col>AvgHum</th><th scope=col>AvgSm</th><th scope=col>AvgSt</th><th scope=col>AvgSr</th><th scope=col>AvgStp</th></tr>
	<tr><th scope=col>&lt;date&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2020-01-01</td><td>43.1</td><td>53.6</td><td>35.1</td><td>265.60</td><td>0.00</td><td>63.79</td><td>0.28</td><td>48.6</td><td>134.78</td><td> 999.13</td></tr>
	<tr><td>2020-01-02</td><td>44.9</td><td>55.4</td><td>35.2</td><td>274.22</td><td>0.05</td><td>71.95</td><td>0.28</td><td>47.6</td><td> 65.96</td><td>1002.54</td></tr>
	<tr><td>2020-01-03</td><td>52.8</td><td>64.9</td><td>45.7</td><td>362.06</td><td>0.95</td><td>92.13</td><td>0.29</td><td>51.0</td><td> 31.10</td><td> 998.46</td></tr>
	<tr><td>2020-01-04</td><td>57.2</td><td>65.1</td><td>42.6</td><td>373.00</td><td>0.52</td><td>83.46</td><td>0.35</td><td>54.6</td><td> 44.91</td><td> 993.43</td></tr>
	<tr><td>2020-01-05</td><td>42.1</td><td>50.5</td><td>34.9</td><td>264.75</td><td>0.00</td><td>56.97</td><td>0.33</td><td>48.3</td><td>135.38</td><td>1004.77</td></tr>
	<tr><td>2020-01-06</td><td>44.1</td><td>58.5</td><td>32.0</td><td>264.68</td><td>0.00</td><td>57.63</td><td>0.31</td><td>46.1</td><td>137.63</td><td>1004.80</td></tr>
	<tr><td>2020-01-07</td><td>41.4</td><td>52.0</td><td>31.3</td><td>273.52</td><td>0.07</td><td>75.20</td><td>0.30</td><td>44.6</td><td> 40.91</td><td>1002.46</td></tr>
	<tr><td>2020-01-08</td><td>42.5</td><td>57.6</td><td>29.7</td><td>313.64</td><td>0.00</td><td>58.86</td><td>0.30</td><td>43.3</td><td>135.65</td><td>1010.30</td></tr>
	<tr><td>2020-01-09</td><td>40.4</td><td>50.5</td><td>31.3</td><td>264.83</td><td>0.00</td><td>60.18</td><td>0.30</td><td>43.3</td><td>121.55</td><td>1022.39</td></tr>
	<tr><td>2020-01-10</td><td>52.0</td><td>65.8</td><td>38.1</td><td>265.81</td><td>0.00</td><td>73.49</td><td>0.29</td><td>46.1</td><td> 74.57</td><td>1019.34</td></tr>
</tbody>
</table>



### Making New Data

#### When does it Rain ? 


```R
## making new data
econet_data$IfRain <- (econet_data$Tprep>0)
econet_data$IfRain <- as.factor(as.integer(econet_data$IfRain))
head(econet_data, 10)
```


<table class="dataframe">
<caption>A tibble: 10 × 12</caption>
<thead>
	<tr><th scope=col>date</th><th scope=col>AvgT</th><th scope=col>MaxT</th><th scope=col>MinT</th><th scope=col>AvgLw</th><th scope=col>Tprep</th><th scope=col>AvgHum</th><th scope=col>AvgSm</th><th scope=col>AvgSt</th><th scope=col>AvgSr</th><th scope=col>AvgStp</th><th scope=col>IfRain</th></tr>
	<tr><th scope=col>&lt;date&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;fct&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2020-01-01</td><td>43.1</td><td>53.6</td><td>35.1</td><td>265.60</td><td>0.00</td><td>63.79</td><td>0.28</td><td>48.6</td><td>134.78</td><td> 999.13</td><td>0</td></tr>
	<tr><td>2020-01-02</td><td>44.9</td><td>55.4</td><td>35.2</td><td>274.22</td><td>0.05</td><td>71.95</td><td>0.28</td><td>47.6</td><td> 65.96</td><td>1002.54</td><td>1</td></tr>
	<tr><td>2020-01-03</td><td>52.8</td><td>64.9</td><td>45.7</td><td>362.06</td><td>0.95</td><td>92.13</td><td>0.29</td><td>51.0</td><td> 31.10</td><td> 998.46</td><td>1</td></tr>
	<tr><td>2020-01-04</td><td>57.2</td><td>65.1</td><td>42.6</td><td>373.00</td><td>0.52</td><td>83.46</td><td>0.35</td><td>54.6</td><td> 44.91</td><td> 993.43</td><td>1</td></tr>
	<tr><td>2020-01-05</td><td>42.1</td><td>50.5</td><td>34.9</td><td>264.75</td><td>0.00</td><td>56.97</td><td>0.33</td><td>48.3</td><td>135.38</td><td>1004.77</td><td>0</td></tr>
	<tr><td>2020-01-06</td><td>44.1</td><td>58.5</td><td>32.0</td><td>264.68</td><td>0.00</td><td>57.63</td><td>0.31</td><td>46.1</td><td>137.63</td><td>1004.80</td><td>0</td></tr>
	<tr><td>2020-01-07</td><td>41.4</td><td>52.0</td><td>31.3</td><td>273.52</td><td>0.07</td><td>75.20</td><td>0.30</td><td>44.6</td><td> 40.91</td><td>1002.46</td><td>1</td></tr>
	<tr><td>2020-01-08</td><td>42.5</td><td>57.6</td><td>29.7</td><td>313.64</td><td>0.00</td><td>58.86</td><td>0.30</td><td>43.3</td><td>135.65</td><td>1010.30</td><td>0</td></tr>
	<tr><td>2020-01-09</td><td>40.4</td><td>50.5</td><td>31.3</td><td>264.83</td><td>0.00</td><td>60.18</td><td>0.30</td><td>43.3</td><td>121.55</td><td>1022.39</td><td>0</td></tr>
	<tr><td>2020-01-10</td><td>52.0</td><td>65.8</td><td>38.1</td><td>265.81</td><td>0.00</td><td>73.49</td><td>0.29</td><td>46.1</td><td> 74.57</td><td>1019.34</td><td>0</td></tr>
</tbody>
</table>



### Month Factor variable

- Factor variable is a category or bin we can place a value in.


```R
# month variable 
econet_data$month <- month(econet_data$date)
econet_data$month <- as.factor(econet_data$month)

# str factor
str(econet_data)
```

    tibble [729 × 13] (S3: tbl_df/tbl/data.frame)
     $ date  : Date[1:729], format: "2020-01-01" "2020-01-02" ...
     $ AvgT  : num [1:729] 43.1 44.9 52.8 57.2 42.1 44.1 41.4 42.5 40.4 52 ...
     $ MaxT  : num [1:729] 53.6 55.4 64.9 65.1 50.5 58.5 52 57.6 50.5 65.8 ...
     $ MinT  : num [1:729] 35.1 35.2 45.7 42.6 34.9 32 31.3 29.7 31.3 38.1 ...
     $ AvgLw : num [1:729] 266 274 362 373 265 ...
     $ Tprep : num [1:729] 0 0.05 0.95 0.52 0 0 0.07 0 0 0 ...
     $ AvgHum: num [1:729] 63.8 72 92.1 83.5 57 ...
     $ AvgSm : num [1:729] 0.28 0.28 0.29 0.35 0.33 0.31 0.3 0.3 0.3 0.29 ...
     $ AvgSt : num [1:729] 48.6 47.6 51 54.6 48.3 46.1 44.6 43.3 43.3 46.1 ...
     $ AvgSr : num [1:729] 134.8 66 31.1 44.9 135.4 ...
     $ AvgStp: num [1:729] 999 1003 998 993 1005 ...
     $ IfRain: Factor w/ 2 levels "0","1": 1 2 2 2 1 1 2 1 1 1 ...
     $ month : Factor w/ 12 levels "1","2","3","4",..: 1 1 1 1 1 1 1 1 1 1 ...


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


          date                 AvgT            MaxT            MinT      
     Min.   :2020-01-01   Min.   :29.20   Min.   :34.20   Min.   :21.20  
     1st Qu.:2020-07-03   1st Qu.:50.40   1st Qu.:60.80   1st Qu.:39.40  
     Median :2021-01-01   Median :62.30   Median :72.90   Median :52.90  
     Mean   :2020-12-31   Mean   :61.43   Mean   :71.61   Mean   :52.14  
     3rd Qu.:2021-07-03   3rd Qu.:73.80   3rd Qu.:84.20   3rd Qu.:66.20  
     Max.   :2022-01-01   Max.   :84.10   Max.   :95.00   Max.   :76.30  
                                                                         
         AvgLw           Tprep            AvgHum          AvgSm       
     Min.   :260.4   Min.   :0.0000   Min.   :26.36   Min.   :0.1300  
     1st Qu.:270.0   1st Qu.:0.0000   1st Qu.:62.10   1st Qu.:0.2700  
     Median :287.7   Median :0.0000   Median :71.95   Median :0.3000  
     Mean   :306.0   Mean   :0.1586   Mean   :69.93   Mean   :0.2975  
     3rd Qu.:322.7   3rd Qu.:0.0700   3rd Qu.:79.80   3rd Qu.:0.3300  
     Max.   :603.4   Max.   :4.3500   Max.   :95.03   Max.   :0.4500  
                                                                      
         AvgSt          AvgSr            AvgStp       IfRain      month    
     Min.   :37.9   Min.   :  6.33   Min.   : 986.0   0:449   1      : 63  
     1st Qu.:52.0   1st Qu.:107.62   1st Qu.: 999.9   1:280   3      : 62  
     Median :64.2   Median :166.82   Median :1003.6           8      : 62  
     Mean   :63.7   Mean   :175.05   Mean   :1003.9           10     : 62  
     3rd Qu.:76.9   3rd Qu.:247.28   3rd Qu.:1007.5           12     : 62  
     Max.   :86.0   Max.   :437.72   Max.   :1022.4           7      : 61  
                                                              (Other):357  
         TDiff      
     Min.   : 2.90  
     1st Qu.:15.00  
     Median :19.50  
     Mean   :19.47  
     3rd Qu.:23.60  
     Max.   :37.30  
                    


Frequency Table to compare categorical / factor variables.


```R
# Frequency Table 
table(econet_data$month, econet_data$IfRain)
```


        
          0  1
      1  34 29
      2  27 30
      3  39 23
      4  43 17
      5  37 23
      6  38 22
      7  35 26
      8  38 24
      9  38 22
      10 40 22
      11 39 21
      12 41 21


### Plotting Basics  


- Simple visual of frequency count


```R
# base plots in R, categorical variables
#does a count
plot(econet_data$IfRain, main = 'Frequency Bar Plot of Rain Occurance', xlab = "Occurence of Rain (0-No, 1- Yes)", ylab = "Number of Days")
```


    
![png](output_103_0.png)
    


- We will be using a package called `ggplot2`.

- Here is a good link: https://www.rstudio.com/resources/cheatsheets/

- Two basic functions: ggplot() & geom_plottype
  - Note we have not even had a title or label specs yet 


```R
# first ggplot figure

ggplot(econet_data, aes(x = date ,y = AvgLw))+ geom_point()
```


    
![png](output_105_0.png)
    


- Maybe show total precip vs month as bar chart.


```R
boxpRain <- ggplot(econet_data, aes(x = month, y = Tprep)) + geom_boxplot()
boxpRain
```


    
![png](output_107_0.png)
    


These dots indicate outliers in out data- we can make this plot easier to visualize manually


```R
boxpRain + ylim(0, .75)
```

    Warning message:
    “Removed 48 rows containing non-finite values (stat_boxplot).”



    
![png](output_109_1.png)
    


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


    
![png](output_111_0.png)
    


- options are very versatile inside a `+geom_statement()`

- We can use the cheatsheet to find out information about this 

- Note how we change atributes inside the `aes` statment


```R
# general plot
ggplot(econet_data, aes(x = AvgHum, y = AvgLw)) +
    geom_point()
```


    
![png](output_113_0.png)
    



```R
# coloring by month to observe trends
ggplot(econet_data, aes(x = AvgHum, y = AvgLw)) +
    geom_point(aes(col = month))
```


    
![png](output_114_0.png)
    


We can also use categorical variables on the x-axis



```R
# + geom_boxplot is a great tool to observe spreads

ggplot(econet_data, aes(x = month , y = TDiff)) + 
    geom_boxplot()
```


    
![png](output_116_0.png)
    


Box-plots are cumbersome and not super helpful in visalization.

### How could we make this boxplot better? 

- Note we are looking at average daily tempurature


```R
# + geom_boxplot is a great tool to observe spreads

ggplot(econet_data, aes(x = month , y = AvgT)) + geom_boxplot()
```


    
![png](output_119_0.png)
    


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

    Picking joint bandwidth of 2.54
    



    
![png](output_121_1.png)
    


## Closing & Resources

We tackled these objectives:

- *Define* open data and reproducible science
- *Describe* how to navigate important aspects of the R/RStudio user-interface
- *Recall* how to extract public data from a web portal (Cardinal) and import it into a  data software (R/RStudio)
- *Demonstrate* understanding of dataset and statistical software through exploratory data analysis plots and numerical summaries


Which plots do you think Mr. Wuf's boss will especially like for the report? What else should he try to include with a little more work?

### Resouces

- For a A Hydrologists Guide to Open Science, from the HESS Journal, click [here](https://hess.copernicus.org/articles/26/647/2022/). 

### Survey 

Thank you for attending the beginner track tutorial at the Open Climate Data Science Workshop. Please complete the voluntary feedback survey, linked [here](https://docs.google.com/forms/d/e/1FAIpQLSejTJjhvCLbCVKBotUa8VtDzYJBnMCilzPrB4VBzJrs7vXqIQ/viewform). The main purposes of this survey is to (1) determine we met specified teaching goals and (2) improve teaching materials for subsequent tutorial sessions.
