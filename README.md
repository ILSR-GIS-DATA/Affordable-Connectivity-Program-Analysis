# Affordable Connectivity Program (ACP) Analysis

Details and methodology supporting the [ACP Dashboard](acpdashboard.com)

**To cite the dashboard:** Parker, C., Gautier, E., and Marcattilio, R. 2022. ACP Dashboard. Institute for Local Self Reliance. <https://www.acpdashboard.com>

# ACP_Dashboard.Rmd

This script is set up to summarize & estimate enrollment in ACP, estimate ACP expenditures, and estimate when the fund is likely to run out. It includes code to model various scenarios of enrollment (current - 100%) based on the number of households (HH) that qualify for ACP (annual HH income within 200% of the poverty line (FPL) or enrollment in federal assistance programs (e.g., SNAP, Medicare/Medicaid, free school lunch program), and when the funds would be depleted according to those scenarios.

## Percent of Eligible Households Enrolled

**Datasets:**\
Household income - Table B19001 of the American Community Survey(ACS) 5 Year (2017 - 2021)\
Household/individual microdata - ACS PUMS 5 Year (2017 - 2021)\
Average HH size - Variable B25010_001 of ACS 5yr 2017 - 2021

**Method (Income only):**\
Our estimate of eligible HHs was calculated using the average HH size for the geography of interest (state or zcta). We used the federal poverty line guidelines from 2021 to determine zipcode/state specific annual income levels (based on the respective average HH size) that fall within 200% of the FPL. Different FPL's exist for Alaska, Hawaii, and the remaining 48 states, so we created an equation for each FPL (see below) which represent a modification of the equation developed by Rural LISC. For any zcta's that did not have an average HH size, we used the national average which was 2.60 in 2021. All income brackets that fell within the 200% FPL were included in our calculation of total households eligible for ACP.

x = average household size for a given state/zcta\
Alaska FPL = 31200 + 11060*(x - 1)\
*Hawaii FPL = 28760 + 10160(x - 1)\
lower48 = 24980 + 8840\*(x - 1)

**Method (Income + Program):**\
We estimated eligible HHs at the state level using ACS micro-data, specifically using the variables listed below. We first evaluated individual-level eligibility where an individual was eligible if: HINS4 == 1 OR POVPIP == between(0,200) OR PAP \> 0 OR SSIP \> 0. We retained all individuals that were eligible and joined those data with the full household-level data-set. Finally, we evaluated the household-level factor and determined households could be eligible if: FS == 1. We grouped this data-set by a household id number (SERIALNO) and state (ST), and calculated the sum of PWGTP (HH weight) to determine the estimated number of households that are eligible by income (POVPIP) & program (FS, HINS4, PAP, SSIP).

Variables*: RT,ST, SERIALNO, SPORDER, PWGTP, PAP, HINS4, SSIP, POVPIP*\

Since micro-data are not available at the zip code level, we used an adjustment factor defined by [Galperin 2022](https://arnicusc.org/wp-content/uploads/2022/10/Policy-Brief-2-ACP-eligibility-final.pdf) to generate more accurate estimates of eligibility at the zip code level. We determined an adjustment factor for each state by calulcating the ratio of the income-only enrollment rate to the income+program enrollment rate. We then applied this ratio to our income-only eligibility estimates at the zip code level. This method does assume that the rate of under counted households is constant across the state.

To estimate household eligibility and enrollment within congressional districts, we used the [congressional district to ZCTA relationship file](https://www2.census.gov/geo/docs/maps-data/data/rel2020/cd-sld/tab20_cd11820_zcta520_natl.txt) to associate zip code data with congressional districts. We grouped the data by congressional district to calculate district level estimates of eligibility and enrollment rates.

**Important note:** The estimates provided within the congressional district map should be used with the knowledge that some zip codes were double counted between districts. Zip codes can overlap congressional district boundaries and because there are currently no more granular data available, we allowed this double counting to occur. Summaries across districts should not be attempted because they would exaggerate any overestimates. Please refer to the state or zip code level data-sets to generate other summaries. We do intend to refine these estimates in time.

**PREDICTIONS - When Will ACP Funds Be Depleted?**\
The nationwide enrollment data for the Emergency Broadband Benefit and the Affordable Connectivity Program (combined) were used as the response variable in a linear regression model. A numeric index value representing the month-year (i.e., 1 - 12) of the fund since its start was used as the predictor variable. The resulting beta estimate from this model was used to generate several enrollment predictions in which we limit enrollment to some percentage of the eligible HHs. We modeled the current enrollment rate, 40%, and continuous enrollment growth. For each prediction, we also calculated the proportion of the fund (\$15.5B [remaining EBB + ACP]) spent, up to 36 months to estimate when the fund would be depleted if we reach and maintain (but do not exceed) that level of enrollment.

**Data Sources:**

1.  Universal Service Administrative Co. ACP Enrollment and Claims Tracker (<https://www.usac.org/about/affordable-connectivity-program/acp-enrollment-and-claims-tracker/#enrollment-by-state>)

2.  Emergency Broadband Benefit Program Enrollments and Claims Tracker (<https://www.usac.org/about/emergency-broadband-benefit-program/emergency-broadband-benefit-program-enrollments-and-claims-tracker/>)

3.  American Community Survey (5-year 2017 - 2021; Table B19001)

4.  Dept. of Health and Human Services Poverty Guidelines for 2021 <https://aspe.hhs.gov/sites/default/files/private/aspe-files/107166/2021-percentage-poverty-tool_0.pdf>

5.  American Community Survey Microdata (5-year 2017 - 2021)

## Versioning

**v2:** Update March 2023: Previous versions of the ACP Dashboard included estimates of household eligibility that were based on income alone. In this version, we have adjusted our estimates to include eligibility based on enrollment in a government assistance program such as SNAP or Medicare/Medicaid. Another change we made in this version was the addition of a congressional district map that includes enrollment estimates and expenditures (as of Dec 2022). Estimates for the congressional district should be used with the understanding that zip codes can overlap district boundaries, and as a result those zip codes are currently counted in both districts. Thus, summarizing across districts in the same state will produce incorrect results.

**v1.3:** Update November 2022: A previous version of the ACP Dashboard was based on an incorrect understanding of the Enrolled and Claimed household numbers. At the time, we believed that these two values (as reflected in the publicly available USAC releases) represented an important (and increasingly so) reality where a large number of the households that were eligible and enrolling in the benefit were not using (or claiming) the benefit. Thus, the data seemed to show that millions of households who had been cleared to use the program were not getting the benefit each month. In the story below, we highlight what looked like gaps in major metropolitan areas, including places like Baltimore, Detroit, Washington D.C., and elsewhere. After further conversation with administration representatives regarding the ACP data releases, it seems this is not the case. Instead, the difference between Enrolled and Claimed households only reflects the procedure via which ISPs participating in the program are submitting payment claims to USAC at irregular intervals. ISPs have six months to submit data to USAC for reimbursement - here, according to administration officials, is where this gap originates from. Rather than reflecting enrolled households not using the benefit, instead it reveals where ISPs are waiting (or have failed) to claim households that are in fact participating. Why this seems to be taking place at larger rates in some metro areas as opposed to others, we do not yet know. If you have additional insight, please reach out to use at [broadband\@muninetworks.org](mailto:broadband@muninetworks.org){.email}. Once we know more, we will update this story. To reiterate: according to administration sources, all Enrolled households should be using the benefit, and reflect the best numbers for understanding how much of the fund is being used at present. We have adjusted the dashboard to reflect this, but preserve the original story below.

**v1.2:** Update, October 2022: In addition to including the most recent USAC numbers, this dashboard has been adjusted to use the Total Claimed Subscriber number (e.g. 8.9 million households nationwide as of the most recent dataset, which is August 2022) to calculate ACP usage rates and predict future funding levels. A previous version used the Total Subscriber number (e.g. 14.5 million nationwide as of August 2022). This was because a) we believed the fact that ISPs have six months to request reimbursement meant that the Claimed Subscriber values were likely less reflective of reality, and b) the two values were much closer together when this dashboard launched than they are today. However, with recent purges of Lifeline-verified enrollees and an increasing gap between the number of those who have enrolled in the ACP but are not taking the benefit, we are moving to use the Total Claimed Subscriber number as the basis for our comparisons and prediction. We believe this reflects a more faithful representation of usage rates and the rate of funds being disbursed. The Percent of Eligible Enrolled values have been preserved in the tooltips where applicable. The policy implications and our analysis of the efficacy and future of this program stand; if anything, the new numbers reflect less success in education and outreach efforts nationwide. For instance, compared to the previous version of this dashboard, values at the county, metro-area, and state are lower than before. For instance, Detroit currently has 58 percent of eligible households enrolled in the program, but only 27 percent of eligible households as claimed subscribers. In Nashville, where only 21 percent of eligible households are enrolled, just 9 percent of eligible households are taking the benefit as claimed subscribers. One significant change from the previous version of this dashboard is the predicted end date of the program. Using the Claimed Subscriber numbers to project the life left in the ACP fund shifts the end of the program significantly. For instance, under the previous most-generous model (with 36 percent of Eligible Households Enrolled), the fund ends in January of 2025. Under our new model (with 24.1 percent of households claiming the benefit), the fund will end in April of 2026. Special thanks to Drew Garner for his insight and feedback on the USAC data.

**v1:**This dashboard was built using Census Bureau data to determine eligibility, and displayed using the Tableau platform. Households can qualify for the Affordable Connectivity Program in a number of ways - from falling under the threshold for 200 percent of the value of the annual federal poverty level (FPL), to receiving a Pell grant in the previous year, to participation in one of the array of federal assistance programs (e.g., SNAP, WIC, Medicaid, the National School Lunch Program). In this visualization, we have only used the 200 percent FPL value to determine the number of eligible households that can take the ACP benefit: 36.6 million. This number is derived using annual household income estimates from the 2015-2019 American Community Survey (ACS) 5-Year tables at the Zip Code Tabulation Area (ZCTA)-level. Only annual household incomes that fell within the 2019 value for 200 percent FPL (e.g. for a household of three, this would be \$42,660 in the continental United States) were included in our calculations. Our estimates are based on a modified version of the methodology used by Rural LISC. We incorporated slight upward adjustments for Alaska and Hawaii). An important note: This methodology undercounts the total number of households eligible for the ACP, and therefore over-represents the enrollment rate (36.5 percent as of August 29, 2022), because it does not include those households whose annual income exceeds 200 percent of the FPL but who still qualify for one of the other assistance programs and thus the ACP. For example, the White House cites a recent Columbia University study which places the total number of eligible households at 48 million. The study calculates the number of households above the 200 percent FPL threshold who still qualify at roughly 12 million, using microdata from the Census Bureau. While our estimate includes households below the 200 percent FPL who may qualify for additional federal programs, it does not include the households above 200 percent FPL. We acknowledge this over-representation of the enrollment rate results in the appearance that the program is doing a better job than the reality of signing up households. We are working to build these additional households into the next revision of this dashboard, once we believe we can faithfully represent the remaining additional households that are eligible with as much nuance as is possible. At the same time, this should have no impact on the accuracy of the predictive model for higher enrollment caps, since the continuous growth trend (in red) shows that only 73 percent of the current model's number of households can sign up before the fund runs out in April 2024.
