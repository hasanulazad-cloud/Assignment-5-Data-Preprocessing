What was done and what it showed
Step	Finding
Cleaning	3 rows had no Gender and were dropped, leaving 1,006. Gender “f” was fixed to “F”. CLASS had trailing spaces (“N “, “Y “), which created 5 labels instead of 3.
Missing values	15 missing numeric values across 9 columns, all under 0.3% of rows. They were filled with the column median.
Duplicates	duplicated() found 0 exact duplicates.
Outliers (lipids)	Z-score > 3 flagged VLDL (29 values), Chol (18), TG (17), HDL (15) and LDL (7). Removing every flagged row would drop 78 of 1,006 records (7.8%).
Outliers (Cr, Urea)	Cr has a median of 60 but a maximum of 800, and 7 values are at or above the 99.5th percentile (401). Urea has 2 values above the 99.9th percentile (26.4).
Outliers (kept)	AGE, HbA1c and BMI outliers were kept deliberately, because high HbA1c and BMI are clinically meaningful.
Encoding	Gender: F=0, M=1. CLASS: N=0, P=1, Y=2.
Feature selection	SelectKBest (ANOVA F-test, k=5) picked AGE, HbA1c, Chol, TG and BMI.
Split and scaling	80/20 split gave 804 training and 202 test rows. StandardScaler was fit on the training data only, which is the right approach.
Key findings
HbA1c is the dominant signal. Its mean is 8.28 and its median 8.0, and it was selected as a top feature, consistent with it defining diabetes status.
Several columns are heavily skewed. VLDL has a mean of 1.84 but a median of 0.9 and a maximum of 35. Cr and Patient_ID are similar. This justifies standardising rather than min-max scaling, as you argued.
Data quality problems were label-level, not missing data. Inconsistent casing and whitespace would have silently split the classes.
