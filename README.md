# Affordable Connectivity Program (ACP) Analysis
 Details and methdology supporting the ACP Dashboard  
 https://apps.communitynets.org/acpdashboard/
 
 

# ACP_Dashboard.Rmd
This script is set up to summarize & estimate enrollment in ACP, estimate ACP expenditures, and estimate when the fund is likely to run out. It includes code to model various scenarios of enrollment (36 - unlimited) based on the number of households (HH) that qualify for ACP (annual HH income within 200% of the poverty line (FPL)), and when the funds would be depleted according to those scenarios.

## Percent of Eligible Households Enrolled
Datasets:   
  Household income - Table B19001 of the American Community Survey(ACS) 5 Year (2015 - 2019)  
  Average HH size - Variable B25010_001 of ACS 5yr 2015-2019
  
Method:  
Our estimate of eligible HHs was calculated using the average HH size for the geography of interest (state or zcta). We used the federal poverty line guidelines from 2019 to determine zipcode/state specific annual income levels (based on the respective average HH size) that fall within 200% of the FPL. Different FPL's exist for Alaska, Hawaii, and the remaining 48 states, so we created an equation for each FPL (see below) which represent a modification of the equation developed by Rural LISC. For any zcta's that did not have an average HH size, we used the national average which was 2.62 in 2019. All income brackets that fell within the 200% FPL were included in our calculation of total households eligible for ACP.  

x = average household size for a given state/zcta  
Alaska FPL = 31200 + 11060*(x - 1)  
Hawaii FPL = 28760 + 10160*(x - 1)  
lower48 = 24980 + 8840*(x - 1)  

PREDICTIONS - When Will ACP Funds Be Depleted?  
The nationwide enrollment data for the Emergency Broadband Benefit and the Affordable Connectivity Program (combined) were used as the response variable in a linear regression model. A numeric index value representing the month-year (i.e., 1 - 12) of the fund since its start was used as the predictor variable. The resulting beta estimate from this model was used to generate several enrollment predictions in which we limit enrollment to some percentage of the eligible HHs. We modeled the current percent enrolled of eligible HHs, 40%, 45%, 50%, and continuous enrollment. For each prediction, we also calculated the proportion of the fund ($15.5B [remaining EBB + ACP]) spent, up to 36 months to estimate when the fund would be depleted if we reach and maintain (but do not exceed) that level of enrollment.

Important note: 
While 200% FPL is a generous guideline to include HHs beyond those that already qualify for other income- and disability- based programs. However, it is important to keep in mind that additional households may not fall within the 200% FPL, but may still qualify for other government programs that automatically qualify them for ACP. These HHs are not yet included in our estimates and therefore our estimates of HH eligibility are likely lower than the true population of eligible HHs. This is something we plan to incorporate in future versions of this dashboard. 




Data Sources:
1. Universal Service Administrative Co. ACP Enrollment and Claims Tracker (https://www.usac.org/about/affordable-connectivity-program/acp-enrollment-and-claims-tracker/#enrollment-by-state)
2. Emergency Broadband Benefit Program Enrollments and Claims Tracker (https://www.usac.org/about/emergency-broadband-benefit-program/emergency-broadband-benefit-program-enrollments-and-claims-tracker/)
3. American Community Survey (5-year 2016 - 2020; Table B19001)
4. Dept. of Health and Human Services Poverty Guidelines for 2019 #https://aspe.hhs.gov/topics/poverty-economic-mobility/poverty-guidelines/prior-hhs-poverty-guidelines-federal-register-references/2019-poverty-guidelines

 