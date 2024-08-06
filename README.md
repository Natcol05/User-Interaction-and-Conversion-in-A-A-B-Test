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

As we had three different groups, we created dataframes for each sample:
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
    
You can find the original dataset here: [Click Here](https://github.com/Natcol05/project-1/blob/f0d815a6511195b94b5a2b00e0944e3bb5c2597d/logs_exp_us.csv)
