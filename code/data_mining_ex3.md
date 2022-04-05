Problem 1: What causes what?
============================

Why can’t I just get data from a few different cities and run the regression of “Crime” on “Police” to understand how more cops in the streets affect crime? (“Crime” refers to some measure of crime rate and “Police” measures the number of cops in a city.)
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Firstly, grouping data from different cities makes the incorrect
assumption that the data points are independently and identically
distributed among cities. Crime rates and police measures vary among
cities, and factors that influence these two variables, such as, police
budgets, population, income levels, criminal punishments, etc. also vary
amongst cities. As a result, combining data from different cities could
distort the outcome of the regression. Secondly, while police measures
affect crime rates, crime rates also affect the level of police
measures, leading to a simultaneous causality bias. Thirdly, there is a
lack of control variables in the regression as crime rates can be
influenced by several other variables as mentioned above; this could
lead to incorrect estimation of the effect of “Police” on “Crime”.

How were the researchers from UPenn able to isolate this effect? Briefly describe their approach and discuss their result in the “Table 2” below, from the researchers’ paper.
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The researchers from UPenn narrowed down their research to only one
city, Washington, D.C., assuming that the data points would be
identically distributed within a city. To deal with the simultaneous
causality bias, they chose Washington, D.C. because it is more likely to
be a terrorism target compared to other cities in the U.S. This allowed
the researchers to utilize the “High Alert” variable as the instrument
variable to address simultaneity. In other words, when there is High
Alert (High Alert = 1), extra police is deployed in the city to protect
against terrorists; in this setup the deployment of the extra police is
not directly related to the variable of interest, “Crime”. So, the High
Alert variable is able to capture the effect of police measures on crime
rates without crime rates affecting police measures. They also added the
log of midday ridership on the Metro as a control variable to test
whether there were fewer victims out in the city becuase of the High
Alert.

Table 2 summarizes their results as two regressions. The first
regression only utilizes the High Alert dummy variable to estimate the
effect of police on the daily total number of crimes in D.C. This leads
to -7.316 as the coefficient on High Alert which is significant at the
5% level. It means that on a High Alert day, the daily total number of
crimes in D.C. by 7.316 units, holding all else constant. The R-squared
for this regression is 0.14, which means only 14% of the variation in
crime rates in D.C. is described by the covariate in the model.

The second regression adds the log of midday ridership to the first
regression as a control variable. This leads to -6.046 as the
coefficient on High Alert at the 5% significance level, meaning that on
a High Alert day, the daily total number of crimes in D.C. falls by
6.046 units, holding all else constant. The coefficient on “Log(midday
ridership)” is 17.341 which is significant at the 1% level. This means
if midday ridership on the Metro increases by 1 percent, the daily total
number of crimes in D.C. increase by 0.173 units, holding all else
constant. The R-sqaured of this regression, 0.17, is slightly higher
than that of the first regression. It means only 17% of the varation in
crime rates in D.C. is described by the covariates in the model. Given
that, since both of the coefficients in this regression are
statistically significant at the 5% and 1% level, respectively, the
second regression performs better than the first regression, although by
only a small margin.

Why did they have to control for Metro ridership? What was that trying to capture?
----------------------------------------------------------------------------------

It is possible that on High Alert days, fewer people are out in the city
due to higher threat levels of terrorism. Fewer people out in the city
means fewer victims of crime which could lead to lower crime rates.
Therefore, to account for this effect, Metro ridership needs to be
controlled for. Metro ridership attempts to capture the number of
potential victims of crime based on the changes in ridership with
respect to High Alert days.

Below I am showing you “Table 4” from the researchers’ paper. Just focus on the first column of the table. Can you describe the model being estimated here? What is the conclusion?
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The researchers are estimating the district-specific effects of High
Alert days on the daily total number of crimes in D.C., while
controlling for Metro ridership using a multiple regression approach
with heteroscedastic errors. They introduce two district dummy
variables, “District 1” and “Other Districts” and interact both the
district dummy variables with the the High Alert variable to estimate
district-specific effects. The coefficient on “High Alert x District 1”
shows that on a High Alert day in District 1, the daily total number of
crimes in D.C. falls by 13.679 units, holding all else constant. This
coefficient is statistically significant at the 1% level. Similarly, the
coefficient on “High Alert x Other Districts” shows that on a High Alert
day in any other district, the daily total number of crimes in D.C.
falls by 11.629 units, holding all else constant. These results reflect
that a High Alert day in District 1 reduces crime rates more than a High
Alert day in any other district. However, the coefficent on “High Alert
x Other Districts” is not statistically significant. Lastly, the
coefficient on “Log (midday ridership)” reflects that a 1 percent
increase in midday ridership on the Metro increases the daily total
number of crimes in D.C. 2.477 units, holding all else constant. This
coefficient is statistically significant at the 5% level.

Given the statisical significance of the coefficients, it can be
concluded that having a High Alert day in District 1 reduces the daily
total number of crimes in D.C. by 13.679 units, holding all else
constant. However, a comparison between District 1 and Other Districts
cannot be made due the lack of significance of the “High Alert x Other
Districts” coefficient.

Problem 2: Tree modeling: dengue cases
======================================

CART model: Regression Tree
---------------------------

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-1-1.png)

### Pruned regression tree at the 1 standard error complexity level

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-2-1.png)

### RMSE of predicting the regression tree on the test set

    ## [1] 26.21029

Random forest
-------------

### RMSE of predicting random forest on the test set

    ## [1] 24.0171

Gradient-Boosted Trees
----------------------

### Gaussian distribution

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-5-1.png)

    ## [1] 67

The figure above displays a loss function as a result of n trees added
to the ensemble for the chosen gradient boosted machine (gbm) model .
The model assumes gaussian distibution with 500 trees. The squared error
loss is shown on the y-axis and numbers of trees is on the x-axis. It
can be seen that the cross-validated errors represented by the green
line are minimized between 40 to 90 trees. Therefore, the ideal number
of trees to minimize error while accounting for overfitting would be
100.

The RMSE between the predicted total number cases of dengue from the
chosen gbm model and the actual total number of cases of dengue from the
test set is shown below.

    ## [1] 25.23003

### Poisson distribution

This gbm model assumes poisson distibution since the variable of
interest is a count variable. All parameters are the same as for the
model shown above, except the number of trees is 100 based on the loss
function above. The RMSE between the predicted total number cases of
dengue from the chosen gbm model and the actual total number of cases of
dengue from the test set is shown below.

    ## [1] 24.57142

Since, the RMSE for the random forest model is the lowest out of all the
models observed above, it will be utilized to create partial dependence
plots for the following variables: specific\_humidity,
precipitation\_amt, and tdrk\_k.

Partial dependence plots
------------------------

### specific\_humidity

The average specific humidity in grams of water per kilogram of air for
the week. This is a raw measure of humidity based purely on how much
water is in the air.

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-8-1.png)

### precipitation\_amt

Rainfall for the week in millimeters.

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-9-1.png)

### tdtr\_k

The average Diurnal Temperature Range (DTR) for the week. DTR is the
difference between the maximum and minimum temperature for a single day.

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-10-1.png)

Problem 3: Predictive model building: green certification
=========================================================

Goal
----

The goal is to build the best predictive model possible for revenue per
square foot per calendar year, and to use this model to quantify the
average change in rental income per square foot associated with green
certification, holding other features of the building constant.

Data Pre-processing
-------------------

I first created a new data frame with a ***revenue*** column which is a
product of the ***Rent*** and ***leasing\_rate***/100 variables. Since
***leasing\_rate*** is a percentage, I divided it by 100 to only get the
factor effect. I also removed ***Rent*** and ***leasing\_rate*** from
the new data frame to prevent multicollinearity and eliminate the need
to remove these two variables from the models specified below. As a
final pre-processing step, I excluded any missing values in the dataset
and split 80% of the data into the training set and 20% of the data into
the test set.

Modeling approach
-----------------

### Linear Model (Baseline)

In order to have a baseline to compare other models to, I performed a
multiple regression on all the features except ***total\_dd\_07***, and
***green\_rating*** (to avoid multicollinearity) in the training set.
The RMSE of predicting the linear model on the test set is shown below.

    ##   result 
    ## 10.53993

### Random forest (Model of Choice)

I chose the random forest technique as it is quite robust, quick, and
basically eliminates the need for cross-validation due to its
“out-of-bag” predictions. I utilized all of the features in the training
set except ***total\_dd\_07***, and ***green\_rating*** (to avoid
multicollinearity) and calculated the resulting RMSE between the
predcited revenue from the model and the actual revenue from the test
set which is shown below. It can be seen that the random forest model
performs better than the linear model based on the RMSE difference
between the two.

    ## [1] 8.893612

To identify the important variables in the random forest model, I built
the variable importance plot shown below. It can be seen that
***hd\_total07*** ***LEED***, ***Energystar***, and ***net*** are the
least important variables, in that order (decreasing in importance).

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-14-1.png)

Since ***net*** is the least important variable, I attempted to further
improve the current random forest model by removing it. The RMSE of the
new model is shown below. Based on the RMSE, this model does not
necessarily perform better than the previous random forest model;
however, it still outperforms the multiple regression model.

    ## [1] 8.918045

To quantify the average change in revenue per square foot I decided to
build partial dependence plots (pdp) associated with green
certifications using the first random forest model. The pdp’s for the
***LEED*** and ***Energystar*** variables are shown below.

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-16-1.png)![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-16-2.png)

#### Conclusion

The pdp for LEED shows that when LEED = 0, the predicted revenue per
square foot per calendar year is slightly over 24 and when LEED = 1, the
predicted revenue per square foot per calendar year is approximately 26.
Likewise, the pdp for Energystar shows that when Energystar = 0, the
revenue per square foot per calendar year is slightly above 24.05 and
when Energystar = 1, the revenue per square foot per calendar year is
approximately 24.4.

These plots reflect that although the revenue predictions for buildings
with green ratings are higher than buildings without green ratings, they
are higher by only a small margin. For instance, buildings with a LEED
certification are predicted to only make ~2 dollars more in revenue on
average than buildings without a LEED certification. Likewise, buildings
with an Energystar certification are predicted to only make ~35 cents
more in revenue on average than buildings without an Energystar
certification.

Hence, it can be concluded that energy certifications do not influence
building revenue per square foot per calendar year very significantly.

Problem 4:Predictive model building: California housing
-------------------------------------------------------

### Goal

The goal is to build the best predictive model for median house values
in California.

Data Pre-processing
-------------------

I created a new data frame with standardized versions of
***totalRooms*** and ***totalBedrooms*** obtained by dividing the two
variables by the ***households*** variable to get averages instead of
totals. Additionally, I removed ***totalRooms*** and ***totalBedrooms***
from the new data frame to avoid multicollinearity and save writing in
model specification. Lastly, I excluded any missing values and split 80%
of the data into the training set and 20% of the data into the test set.

### Linear Model (Baseline)

In order to have a baseline to compare other models to, I performed a
multiple regression on all the features in the training set. The RMSE of
predicting the linear model on the test set is shown below.

    ##   result 
    ## 69731.69

### Random Forest

I utilized all of the features in the training set and calculated the
resulting RMSE between the predcited revenue from the random forest
model and the actual revenue from the test set which is shown below. It
can be seen that the random forest model significantly outperforms the
linear model based on the RMSE difference between the two (~18000).

    ## [1] 49701.57

### Gradient-Boosted Trees (Model of Choice)

I used all of the features in the training set and assumed a Gaussian
distibution for the gradient boosted model with 10-fold
cross-validation. The parameters for this model are as follows:
interaction.depth = 4, n.trees = 3000, shrinkage = .05. I ended up
choosing such a high number of trees becuase the loss function kept
showing the n-th tree as the mean-squared-error minimizer until I chose
3,000 and received a 2,900+ number as the mean-squared-error minimizer.
The number of trees that minimized the mean-squared-error and a plot of
the loss function is displayed below.

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-20-1.png)

    ## [1] 2995

The RMSE between the predicted revenue and the actual revenue from the
test set is displayed below. It is lower than that of the random forest
model. Therefore, this model will be the model of choice.

    ## [1] 46611.1

Map Plots
---------

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-22-1.png)

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-23-1.png)
![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-24-1.png)
