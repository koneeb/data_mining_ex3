Problem 1
=========

1. Why can’t I just get data from a few different cities and run the regression of “Crime” on “Police” to understand how more cops in the streets affect crime? (“Crime” refers to some measure of crime rate and “Police” measures the number of cops in a city.)
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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

2. How were the researchers from UPenn able to isolate this effect? Briefly describe their approach and discuss their result in the “Table 2” below, from the researchers’ paper.
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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

3. Why did they have to control for Metro ridership? What was that trying to capture?
-------------------------------------------------------------------------------------

It is possible that on High Alert days, fewer people are out in the city
due to higher threat levels of terrorism. Fewer people out in the city
means fewer victims of crime which could lead to lower crime rates.
Therefore, to account for this effect, Metro ridership needs to be
controlled for. Metro ridership attempts to capture the number of
potential victims of crime based on the changes in ridership with
respect to High Alert days.

4. Below I am showing you “Table 4” from the researchers’ paper. Just focus on the first column of the table. Can you describe the model being estimated here? What is the conclusion?
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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

Problem 2
=========

CART model: Regression Tree
---------------------------

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-1-1.png)

### Pruned regression tree at the 1 standard error complexity level

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-2-1.png)

### RMSE of predicting the regression tree on the test set

    ## [1] 32.89083

Random Forests
--------------

### RMSE of predicting randam forest on the test set

    ## [1] 31.72132

Gradient-Boosted Trees
----------------------

### Gaussian distribution

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-5-1.png)

    ## [1] 245

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

    ## [1] 32.54443

### Possion distribution

This gbm model assumes poisson distibution since the variable of
interest is a count variable. All parameters are the same as for the
model shown above, except the number of trees is 100 based on the loss
function above. The RMSE between the predicted total number cases of
dengue from the chosen gbm model and the actual total number of cases of
dengue from the test set is shown below.

    ## [1] 32.72318

Since, the RMSE for the second gbm model is the lowest out of all the
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

### tdtr\_k"

The average Diurnal Temperature Range (DTR) for the week. DTR is the
difference between the maximum and minimum temperature for a single day.

![](data_mining_ex3_files/figure-markdown_strict/unnamed-chunk-10-1.png)
