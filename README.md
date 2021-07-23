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











