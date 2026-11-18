# adms-4509-group2-term-project

## <ins>Method: Peaks-Over-Threshold (POT) approach with a generalized Pareto distribution (GPD)</ins>  

Week 6 p I slides describe it as a way to smooth and extrapolate the tail of an empirical distribution. Procedure outlined is to select a high threshold, examine observations exceeding it, and fit a generalized Pareto distribution using maximum likelihood. The right tail is of particular concern, on account of unusually large losses; with losses defined as the negative of returns.  


**1. Historical portfolio losses**  
With an initial portfolio value of $5 million, weights at 20% each across 5 stock-picks correspond to a $1 million position in each. I’ll use the five stocks’ adjusted-price histories to calculate aligned daily returns. For each day, I’ll construct the return on a hypothetical portfolio given weights described above and reverse the sign:  
Portfolio loss = -Portfolio return  

Using the time-series data supplied by Rowan, I’ll take the daily log returns and convert them to a simple return before applying the weights:  

Ri=eri-1,  
Rp=∑0.20Ri  

The series represents a portfolio rebalanced to 20% each day.  


**2. Risk date**  
Assuming that the estimate applies to the beginning of the October 8-November 12 holding period, I’ll fit the model using daily returns available before the Oct 8 investment decision, assuming that the positions were established at market open (i.e., exclude returns from Oct 8).   


**3. Threshold selection and tail-fitting**  
I’ll start with the 95th percentile of historical daily portfolio losses as threshold u. For each loss >u I'll calculate its excess over the threshold and fit a GPD to those excesses by maximum likelihood.  

Per course slides, GPD as two parameters:  
- Shape έ describes the tail’s form and heaviness.  
- Scale β describes the size of excesses above the threshold.  

I might fit the model again at nearby thresholds, such as 90% and 97.5%, to examine how much the results change. A higher threshold focuses more on extreme observations, implicitly leaving less data to estimate the model.  

**4. Estimation: one-day 99% VaR and ES**  
I’ll then combine the fitted tail distribution with the proportion above the threshold to estimate:  
- 99% VaR: the estimated one-day loss level exceeded with 1% probability.  
- 99% ES: the estimated average one-day loss when the loss exceeds that VaR.  

I’ll express both as a percentage of portfolio value and in dollars, using the $5 million initial value for the opening-date estimate. Since course-convention requires using a normal-distribution at 99%, using 99% for EVT would make the results more easily comparable.  

**5. Normal comparison and explanation**  
Subsequently, I’ll calculate an independent normal benchmark using the same portfolio series, estimation window, date, one-day horizon, and $5 million value. Later, I’ll add other group members’ normal, EWMA, or GARCH estimates as applicable and helpful (i.e., where assumptions match). 



## <ins>Software: Jupyter + SciPy</ins>  
I’ll use Jupyter/Python, extract/read the existing time-series supplied by Rowan, fit the GPD, repeat the fit at several thresholds, and create a comparison chart in a reproducible notebook. I’ll likely use Excel to share inputs and results with the group or otherwise. I believe the SciPy library may have the relevant tools for conducting analysis above.   



## <ins>Sources</ins>
1. [SciPy documentation: fitting continuous statistical functions](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.rv_continuous.fit.html)  

2. [The price and log returns .xlsx dataset Rowan thoughtfully shared.](/data/5 Year Historical Stock Price Data - ADMS4509.xlsx)  
