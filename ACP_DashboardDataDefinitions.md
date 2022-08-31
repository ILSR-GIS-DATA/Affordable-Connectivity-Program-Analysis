# ACP Dashboard Data Definitions

## ACP_DASHBOARD_EnrollByState.csv - data set used for the state map of enrollment

**geoid:** 2 digits code representing the state state: state name\

**totalHH:** estimated total households in the state\

**HHqualify:** estimated households that qualify for ACP\

**HHqualify_perc:** estimated percent of households that qualify for ACP\

**HH_aug22:** number of households enrolled in ACP\

**HHEoE_perc:** estimated percent of households enrolled in ACP of the households eligible

## ACP_DASHBOARD_ZipData.shp (and associated files) - data set used for the zipcode map & graphic/map of cities reported in Benton analysis (link below)

**zipcode:** zipcode (formatted as character) enrollments: number of households enrolled in ACP\

**totalHH:** Total estimated number of HH in that zip code according to ACS 2015-2019

**HHqualify:** Total estimated number of HH in that zip code that are eligible for ACP based on household income\

**HHqualify_perc:** Estimated percent of HH in that zip code that are eligible for ACP\

**HHEoE_perc:** Estimated percent of HH in that zip code that are enrolled in ACP of the HH that are eligible     

**city:** City name at that zipcode - only reported for cities that were included in this analysis by Benton Foundation for Broadband and Society: <https://www.benton.org/blog/affordable-connectivity-plan-enrollment-and-digital-equity-planning>

## ACP_DASHBOARD_ModelData.csv - data set used in the model dashboard element

**month:** month-year starting with Jan 2022 (when EBB changed to ACP)\

**enrolled:** predicted number of enrolled households\

**lwr:** Lower 95% confidence interval\

**upr:** Upper 95% confidence interval\

**perc.enrolled:** Estimated percent of households enrolled relative to households eligible to enroll.\

**month.spent:** Estimated funds spent per month on Internet access subscription (at \$30/mo/HH).\

**cum.spent:** Estimated cumulative funds spent per month on Internet access subscription (at \$30/mo/HH).  

**perc.used:** Estimated percent of \$15.5 B spent on Internet access subscription.\

**month.spent25:** Estimated funds spent per month on Internet access subscription (at \$30/mo/HH) + additional 2.5% to incorporate Tribal subscription (\$75/mo/HH) and device expenditures.\

**cum.spent25:** Estimated cumulative funds spent per month on Internet access subscription + additional 2.5% to incorporate Tribal subscription (\$75/mo/HH) and device expenditures.\

**perc.used25:** Estimated percent of \$15.5 B spent on Internet access subscription, with additional 2.5% to incorporate Tribal subscription (\$75/mo/HH) and device expenditures.
