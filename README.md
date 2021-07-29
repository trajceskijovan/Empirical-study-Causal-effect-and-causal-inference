# Empirical-study-Causal-effect-and-causal-inference

**Topic:** COVID-19 mortality rate (study completed in Python). 

**Narative:** This is an original empirical study I have prepared and submitted for the Applied Predictive Modeling course during my second semester at HKBU - Master of Science in Data Analytics and Business Economics.

# Code, full research paper & empirical study (Jupiter Notebook):
https://github.com/trajceskijovan/Empirical-study-Causal-effect-and-causal-inference/blob/main/COVID-19%20mortality%20rate.ipynb

# Research question and motivation
The purpose of this project is to identify the factors correlated with the COVID-19 mortality rate. We hope to increase the level of understanding concerning factors that render some states more vulnerable to the virus than others. As coronavirus continues its spread across the globe, even modest, but early advances in such knowledge could lead to a significant reduction in loss of life.

The infection fatality rate, the probability of dying for a person who is infected, is one of the most important features of the coronavirus disease 2019 (COVID-19) pandemic. The expected total mortality burden of COVID-19 is directly related to the infection fatality rate. Moreover, justification for various non-pharmacological public health interventions depends on the infection fatality rate. Some stringent interventions that potentially also result in more noticeable collateral harms may be considered appropriate, if the infection fatality rate is high. Conversely, the same measures may fall short of acceptable risk–benefit thresholds, if the infection fatality rate is low .2 
We will examine Population Density and its effect on target variable - Fatality Rate.

Population density has a marked impact on spread of the pandemic. Population density can be defined as a measurement of the average number of individuals per unit of geographic area (Liu et al. 2020) The higher the population density, the faster diseases can spread. Population density is likely just one of many key factors that determine the vulnerability of a specific location to the virus. In smaller communities, the virus has targeted nursing homes, community houses, funeral parlors, and of course cruise ships, which are like dense small cities at sea.

We chose mortality rate as our target variable as it is less likely than case rates (e.g. infection rate) to be distorted by local variations in testing policy.
 
# Target and Focal Variables
Fatality Rate - Dependent Variable

Population Density (Social Variable) - the increased population density increases exposure to all communicable pathogens as it is getting more difficult for people to keep social distance. On the other side, people living in rural areas are more likely to maintain some sort of social distance. Therefore, people living in areas with high population density are more likely to be infected with a heavy viral load which could increase the severity of COVID-19 and lead to death. We expect the coefficient of this variable to be positive.

# Description of Datasets
COVID 19 Dataset:
- Collected 47 variables covering two data types: medical and demographic.
- The COVID 19 dataset was collected from different sources: CDC, Agency for Healthcare, Bureau of Health, Labor Statistics, Department of Labour, US Census Bureau, Kaiser Family Foundation, Johns Hopkins University, Wikipedia, YouGov, NBC News.
- The data is on a state level (51 states)

Policy Dataset:
- Dataset was collected from The Oxford COVID-19 Government Response Tracker (OxCGRT) website.
- OxCGRT provides information on 20 indicators of government responses.
- Eight of the policy indicators (C1-C8) record information on containment and closure policies, such as school closures and restrictions in movement.

# Visualization of Combined Datasets

# Models and Results

Simple Linear Regression:
Fatality Rate=𝛽0+𝛽1*𝑃𝑜𝑝𝑢𝑙𝑎𝑡𝑖𝑜𝑛𝐷𝑒𝑛𝑠𝑖𝑡𝑦+𝑒
 
with  𝛽  the average causal effect of Population Density on Fatality Rate

The null hypothesis is
ℍ0:𝛽=𝛽0
The alternative hypothesis is
ℍ1:𝛽≠𝛽0
Null hypothesis states that the true value of 𝛽 equals the hypothesized value 𝛽0. Alternative hypothesis states that the true value of 𝛽 does not equal the hypothesized value.

Our main goal is to assess whether or not a coefficient 𝛽 equals a specific value 𝛽0.

Simple Regression & Forward Selection:

In order to alleviate omitted variables bias, we need to think about finding control variables, which may directly correlated to focal 𝑥 (Population Density) and directly influence 𝑦(Fatality Rate from COVID-19). We will discuss each of the variables separately. Here you can see a list of confounding variables:

 - Population Density - DEN
 - Population Ages 65+% - AGELevelShare
 - Health Care Expenditures per Capita - HC
 - Bachelors Degree Graduate Rate - EDUC
 - SeverelyObese% - OBESE
 - Life Expectancy at Birth - LIFE
 - Infection Rate -IR

Multiple Regression: FatalityRate=𝛽0+𝛽1*𝐷𝐸𝑁+𝛽2*𝐴𝐺𝐸𝐿𝑒𝑣𝑒𝑙𝑆ℎ𝑎𝑟𝑒+𝛽3*𝐻𝐶+𝛽4*𝐸𝐷𝑈𝐶+𝛽5*𝑂𝐵𝐸𝑆𝐸+𝛽6*𝐿𝐼𝐹𝐸+𝛽7*𝐼𝑅+𝑒

# Hypothesis Testing
Result: We can see that in hypothesis testing for Population Density we will reject H0 in favor of H1 and conclude that beta j is significantly different from zero.
P-value is below 0.05 so we reject Null Hypothesis and conclude that beta is significantly different from zero.

# Endogeneity Handling
We need to consider if both the dependent variable and a regressor are simultaneously determined or they can theoretically affect each other in different scenarios. If this is the case, then the variables should be treated as endogenous.

Fatality Rate=𝛽0+𝛽1*𝑃𝑜𝑝𝑢𝑙𝑎𝑡𝑖𝑜𝑛𝐷𝑒𝑛𝑠𝑖𝑡𝑦+𝑒
If COVID-19 Fatality Rate is affected by unobserved 'Wealth of the population' in a particular state, and individuals with higher wealth choose to live in bigger cities with higher Population Density, then 𝑒 contains unobserved Wealth, so Popultion Density and 𝑒 will be positively correlated.

Hence Population Density is endogenous.

In order to identify the unknown  𝜷  in structual model, we need the help of IVs to converse the structual model into two linear projection models.

In order to handle endogeneity, we need to find instruments, which are determined outside the system for  (𝑦𝑖,𝒙2𝑖) , causally determine  𝒙2𝑖 , but do not causally determine  𝑦𝑖  except through  𝒙2𝑖 .

Presents of IV can be used to estimate consistently the parameters in equation.

The reason for choosing 2SLS over OLS is that we think OLS estimators beta0 and beta1 are inconsistent due to correlation between x and u.

IV must be: 
1) Uncorrelated with other unobserved factors affecting FatalityRate
2) It should not have direct affect on FatalityRate
3) It must be correlated with Population Density

Null Hypothesis: 𝐇0:𝛿1=0
Failing to reject 𝐇0:𝛿1=0 indicates that no obvious evidence for endogeneity of 𝑦2
We reject the null hypothesis that DEN is exogenous and conclude that DEN is indeed an endogenous variable.

# IV Selection
An ideal instrumental variable affects the regressor (Population Density) but does not directly influence the dependent variable (Covid-19 Fatality Rate) except through the indirect effect on the regressor.

Median Income Annual and Gini Index are potential IV choices:

If a state has High Annual Median Income, it indicates that Population Density will be higher in that state as more people will migrate to the state trying to find a job.

However, Median Income Annual does not directly affect if a person gets infected by Covid-19 and dies from it, so should not have a direct effect on Covid-19 Fatality Rate

Gini Index - is a measure of statistical dispersion intended to represent the income inequality or wealth inequality within a nation or any other group of people.

To get the consistent estimator for  𝜷 , we introduce Two-Stage Least Squares.

We completed 2SLS using two different OLSs as well as utilizing a package -IV2SLS. Both of the approaches provided us with similar results for beta for log Density, beta=1.0791. However, there is a difference in Standard Error. Standard Error of automatic 2SLS is 0.2121 and Standard Error using two separate OLS is 0.1495. Standard Error using two OLS is misleading as the computer treats each of the OLSs, 1st and 2nd OLS, separately. Therefore, we choose to use automatic 2SLS approach using the package IV2SLS.

Solution for beta using OLS is smaller than it is in 2SLS. It appears that OLS underestimates true effect of beta.

# Sargant Test
We need to test the assumption that IVs are not correlated with the error term in the equation of interest. If IVs are endogenous than we need to find different IVs. Since we have overidentifying restrictions, we are going to perform the Sargan–Hansen test.

The test of overidentifying restrictions regresses the residuals from an 2SLS regression on all instruments and exogenous variables. It is based on the observation that the residuals should be uncorrelated with the set of exogenous variables if the instruments are truly exogenous.

Null Hypothesis: All IVs are exogenous (IVs are uncorrelated to Error Term)
Alternative Hypothesis: IVs are correlated to Error Term.

Result: P-Value is above 0.05, therefore, we cannot reject Null Hypothesis and may conclude that IVs are not correlated to Error. It supports the validity of IVs we found.

# Testing for Endogeneity
Next, we can use Hausman-Wu test to test for Endogeneity.

The 2SLS estimator is less efficient than OLS estimator when the explanatory variables are exogenous

Therefore, if no endogeneity problem occurs, then we prefer OLS estimator.

Suppose the structural model:
𝑦1=𝛽0+𝛽1𝑦2+𝛽2𝑧1+𝛽3𝑧2+𝑢1
where 𝑦2(Population Density) is suspected endogenous

We also have available IVs 𝑧3 (Gini Index) and 𝑧4(Income) excluded from the above model. In terms of the first stage linear prediction model of
𝑦2=𝜋0+𝜋1𝑧1+𝜋2𝑧2+𝜋3𝑧3+𝜋4𝑧4+𝑣2
we know that 𝑦2 (Population Density) is not endogenous if and only if 𝑣2 is uncorrelated to 𝑢1 in the structural model. Idealy speaking, we can just test the statistical significance of 𝛿1 in the simple projection model:
𝑢1=𝛿1𝑣2+𝑒1
In practice, we will collect the first stage linear prediction model residuals and conduct the following auxiliary regression:
𝑦1=𝛽0+𝛽1𝑦2+𝛽2𝑧1+𝛽3𝑧2+𝛿1𝑣̂ 2+ error 

𝐇0:𝛿1=0
Failing to reject 𝐇0:𝛿1=0 indicates that no obvious evidence for endogeneity of Population Density (y2)*

We can reject Null Hypothesis and conclude that we have evidence for endogeneity of Population Density, therefore, we need to continue our research to find more IVs.

Because of this result, we will explore other variables as IVs for 2SLS. We add Unemployment and Urbanization as IVs. Both of those variables affects the regressor (Population Density) but do not directly influence the dependent variable (Covid-19 Fatality Rate) except through the indirect effect on the regressor.

# Additional IVs
We fail to reject Null Hypothesis at 1% and 5% when we change the IVs. We conclude that there are no evidence for endogeneity of Population Density when we use IVs such as Unemployment and Urbanization.

We conclude that the population density has a significant effect on Fatality Rate and by using the following variables such as AGELevelShare, HC , EDUC, OBESE, LIFE, IR and IVs being Urban and Unemployment rates, the focal X remains stable.

One of the limitations is that our dataset has a lot of variables but limited rows due to number of US States.

# Conclusion and Limitations
This project estimates and analyzes the causal effect of Population Density on the COVID-19 mortality rate. COVID-19 has been more fatal than many recent epidemics, which makes its death toll relevant to understanding the pandemic more broadly and help to better prepare for future pandemics.

Understanding the reasons behind Fatality Rate being high in some of the areas and not others will help Government to come up with measurements to mitigate the pressure on the Health Care system during pandemic outbreak and potentially save lives of millions.

The estimated results suggest that the population density has a statistically significant positive effect on the COVID-19 mortality rate.

IV Limitations: In a small sample, the IV estimator can have a substantial bias. According to the law of large numbers, IV estimator is consistent for b1:plim(b1^)=b1, provided assumptions are satisfied. If either assumptions fails, the IV estimators are not consistent. One feature of the IV estimator is that, when x and u in fact correlated so that IV Estimation is actually needed - it is essentially never unbiased. IV estimator has an approximate normal distribution in large sample size.

There are considerable limitations to any study employing data aggregated to the state level. Ours is no exception. Such data will likely not capture factors relevant to our research question that more refined data would reveal. Despite these limitations, we hope that this study will serve as the basis for future research in this area.





