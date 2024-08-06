<p align="center"><b>Analyzing User Interaction and Conversion in A/A/B Test for Font Implementation in an Online Application</b></p>

This project aims to analyze user interactions and their journey through the application's sales funnel. We begin by studying the funnel to understand how users progress towards making a purchase, identifying stages where users may drop off.

Additionally, we delve into the results of an A/A/B test to give useful information for the implementation changes to the application's fonts. 

These are some of the libraries used for: 

```python
import pandas as pd
import scipy.stats as stats
from scipy.stats import ttest_ind
from scipy.stats import levene
from matplotlib import pyplot as plt
import seaborn as sb
import math as mth
from scipy.stats import mannwhitneyu
```

The experiment divides users into three groups: two control groups using the old fonts and one test group using the new fonts.

```python
sample_246 = df_august[df_august['ExpId'] == 246]
sample_247 = df_august[df_august['ExpId'] == 247]
sample_248 = df_august[df_august['ExpId'] == 248]

events_per_user_246 = sample_246.groupby('UserId').size()
events_per_user_247 = sample_247.groupby('UserId').size()
events_per_user_248 = sample_248.groupby('UserId').size()
```

And we applied a mannwhitneyu test to check if there were a statistically significant difference between them: 

```python
stat, p_value = mannwhitneyu(events_per_user_246, events_per_user_247)

print(f'Valor p: {p_value}')

# Interpretación
if p_value < 0.05:
    print("There is a statistically significant difference between both samples.")
else:
    print("There isn't a statistically significant difference between both samples")
```
After conducting the tests, we concluded that it is premature to determine if the new fonts are well-accepted. Initially, when comparing the overall means of the control groups, we couldn't identify a statistically significant difference. However, when analyzed by event, we found significant differences in most cases. This discrepancy suggests the need to check for potential issues in the data collection process or other complications.

It is important to highlight that there were no significant differences between the second control group (sample 247) and the third group (sample 248), which isn't a control group.

Key points to note:

* The control groups have specific conditions for control tests. For instance, the difference between the population and key metrics isn't greater than 1%. However, we lack detailed information about the application process, such as whether all users stayed until the end, which could affect the results.

* We applied the Bonferroni test to avoid mistakes in mean comparisons, resulting in different significance levels for each comparison.

* Lastly, we excluded the data from users in July due to its lack of information, but this did not result in a significant data loss.
  
You can find the original dataset here: [Click Here](https://github.com/Natcol05/project-1/blob/f0d815a6511195b94b5a2b00e0944e3bb5c2597d/logs_exp_us.csv)
