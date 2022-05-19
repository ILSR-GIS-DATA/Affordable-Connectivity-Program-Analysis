# Affordable Connectivity Program Analysis
 Details about ACP maps and analysis 
 

# ACP_Enrollment.Rmd
This script is set up to summarize & estimate the total ACP funds that have been used. It also includes code to model various scenarios of enrollment (35 - 75%) based on the number of households (HH) that qualify for ACP (HH income within 200% of the poverty line), and when the funds would be depleted according to those scenarios.

# MAP - Percent of Eligible Households Enrolled
The values displayed in this map were calculated by first determining the number of households (HHs) eligible for ACP in each state, and then dividing the total number of HHs enrolled per state by that value. At the time of this writing, the mean national household size is 2.51, so we rounded up to a 3 person household and determined the threshold value for ACP eligibility based on annual HH income was 43,920. We combined estimated numbers of households from the ACS table B19001, combining variables B19001_002 - B19001_009, to determine the total number of households that have an income that is less than or equal to $44,999 (the maximum value in the income range of B19001_009). We used this combined value as the total HHs eligible for ACP in the equation below.  

Percent eligible HHs (per state) = (Total HHs enrolled / Total HHs eligible) * 100

# PREDICTIONS - When Will ACP Funds Be Depleted?
We collected data from:
1. Universal Service Administrative Co. ACP Enrollment and Claims Tracker (https://www.usac.org/about/affordable-connectivity-program/acp-enrollment-and-claims-tracker/#enrollment-by-state) (last updated on 25 APR 2022)
2. Emergency Broadband Benefit Program Enrollments and Claims Tracker (https://www.usac.org/about/emergency-broadband-benefit-program/emergency-broadband-benefit-program-enrollments-and-claims-tracker/)
3. American Community Survey (5-year 2016 - 2020; Table B19001)

 
The nationwide enrollment data for the Emergency Broadband Benefit and the Affordable Connectivity Program (combined) were used as the response variable in a linear regression model. A numeric index value representing the month-year (i.e., 1 - 12) of the fund since its start was used as the predictor variable. The resulting beta estimate from this model was used to generate several enrollment predictions ranging from 35 - 75%. For each prediction, we summarized the proportion of the fund ($14.2B) spent, up to 36 months.


