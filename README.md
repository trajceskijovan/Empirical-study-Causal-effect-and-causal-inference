# Empirical-study-Causal-effect-and-causal-inference
Topic: COVID-19 mortality rate (study completed in Python)

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
- We collected 47 variables covering two data types: medical and demographic.
- The COVID 19 dataset was collected from different sources: CDC, Agency for Healthcare, Bureau of Health, Labor Statistics, Department of Labour, US Census Bureau, Kaiser Family Foundation, Johns Hopkins University, Wikipedia, YouGov, NBC News.
- The data for collected on a state level (51 states)

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




















