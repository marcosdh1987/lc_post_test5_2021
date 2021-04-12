# lc_post_test5_2021
for testing proposal


# data analysis libraries
import numpy as np
import pandas as pd

# data visualization libraries
import seaborn as sn
import matplotlib.pyplot as plt
%matplotlib inline


# Checking missing values in each variable
plt.figure(figsize=(10,10))
sn.heatmap(data.isnull(), yticklabels = False, cbar = False)





