ACP Dashboard Data Definitions

Summary of fields in ACP_enroll.xlsx

Sheet - HH_enrollBYzip

	zipcode: zipcode (formatted as character)
	enrollments: number of households enrolled in ACP
	totalHH: Total estimated number of HH in that zip code according to ACS 2016-2020
	HHqualify: Total estimated number of HH in that zip code that are eligible for ACP based on household income (<$45k annually)
	HHqualify_perc: Estimated percent of HH in that zip code that are eligible for ACP
	HHEoE_perc: Estimated percent of HH in that zip code that are enrolled in ACP of the HH that are eligible.
	
	
Sheet - ACPmodel

  *The monthly enrolled values for which there are no lwr/upr values represent observed values, except for expendeture values which are estimated.*
  month: numerical index of month number starting with Jan 2022 (when EBB changed to ACP)
  enrolled: predicted number of enrolled households 
  lwr: Lower 95% confidence interval
  upr: Upper 95% confidence interval
  perc.enrolled: Estimated percent of households enrolled relative to households eligible to enroll.
  month.spent: Estimated funds spent per month on Internet access subscription (at $30/mo/HH).
  cum.spent: Estimated cumulative funds spent per month on Internet access subscription (at $30/mo/HH).
  perc.used: Estimated percent of $14.2 B spent on Internet access subscription.
  cum.spent25: Estimated cumulative funds spent per month on Internet access subscription + additional 2.5%  to incorporate  Tribal subscription      ($75/mo/HH) and device expenditures.
  perc.used25: Estimated percent of $14.2 B spent on Internet access subscription, with additional 2.5% + additional 2.5%  to incorporate  Tribal subscription      ($75/mo/HH) and device expenditures.