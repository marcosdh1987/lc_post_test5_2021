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



![image](https://user-images.githubusercontent.com/31476977/114443167-beeb5380-9ba3-11eb-86d3-9c3846ca99b4.png)

well = data[['DATE & TIME', 'CHOKE', 'WELL Name', 'Test', 'Well Head Pressure  psig',
       'Well Head Temp deg C', 'Sep. Static Pressure psig',
       'Sep. Gas Temp deg C', 'Gas Rate Sm3/d',
       'Gas Cumm. Sm3', 'GOR (Gas/Oil Ratio) m3/m3', 'Oil Density  g/cm3',
       'Oil Temp deg C', ' Raw Oil Flow  m3/d', 'Oil Flow Sm3/d',
       'Water Flow Rate m3/d', 'WaterDensity Kg/m3', 'Flow Water Cut  %']]

well = well[well['CHOKE']!='-']

#for print
import matplotlib.pyplot as plt
# Import necessary packages
import os
import matplotlib.pyplot as plt
import matplotlib.dates as mdates
from matplotlib.dates import DateFormatter
import seaborn as sns
import pandas as pd

# Handle date time conversions between pandas and matplotlib
from pandas.plotting import register_matplotlib_converters
register_matplotlib_converters()

# Use white grid plot background from seaborn
sns.set(font_scale=1.5, style="whitegrid")

def well_print(well):
    fig, ax = plt.subplots(3,figsize=(22,8),sharex=True)
    wellname = 'Well Name: ' + well['WELL Name'].iloc[1]
    fig.suptitle(wellname)

    well.plot(x='DATE & TIME', y='Gas Rate Sm3/d',color='orange',ax=ax[0])
    well.plot(x='DATE & TIME', y='Oil Flow Sm3/d',color='green',ax=ax[1])
    well.plot(x='DATE & TIME', y='Water Flow Rate m3/d',color='blue',ax=ax[2])

    ax[0].set(title="Gas Flow Rate")
    ax[1].set(title="Oil Flow Rate")
    ax[2].set(title="Water Flow Rate")
   
    plt.show()
    
    
    
#to avoid no flow moments

well = well[well['CHOKE']!='-']
well.dropna(subset=['Gas Rate Sm3/d', 'Oil Flow Sm3/d'], axis=0, inplace=True)
well.isnull().sum()

well['GOR'] = well['Gas Rate Sm3/d'] / well['Oil Flow Sm3/d']
well['WGR'] = well['Water Flow Rate m3/d'] / well['Gas Rate Sm3/d']
well['WLR'] = well['Water Flow Rate m3/d'] / (well['Oil Flow Sm3/d']+well['Water Flow Rate m3/d'])

well.dropna(subset=['GOR', 'WGR', 'WLR'], axis=0, inplace=True)
well.isnull().sum()

well = well[well['GOR']!=0]
well = well[well['GOR']<=10000000]

well[well['GOR'] == 0 ].count()

well.columns


G2 = ['LCA-3083','LCA-3084','LCA-3085']
G7 = ['LCA-3005', 'LCA-3006', 'LCA-3007']
G8 = ['LCA-3008', 'LCA-3009', 'LCA-3010']
K3 = ['LCA-3011', 'LCA-3012', 'LCA-3013']
lc3001 = ['LCA-3001']

well = well[well['Test'] != 'sep-movil-r5-fsf']

well['Sep. Static Pressure psig'] = well['Sep. Static Pressure psig'].astype(float)
well['Sep. Gas Temp deg C'] = well['Sep. Gas Temp deg C'].astype(float)

wellname = K3

well.sort_values(by=['Test'],inplace=True)

for w in wellname:
    well_print(well[well['WELL Name']==w])
    fig1, ax = plt.subplots(1,3,figsize=(24,6))
    ax[0].set_title('Gas Flow Avg')
    ax[1].set_title('Oil Flow Avg')
    ax[2].set_title('Water Flow Avg')
    #ax[1].set_title('Pressure line Psig')
    #ax[2].set_title('Temperature C')
    
    sns.boxplot(y='Gas Rate Sm3/d', x='CHOKE', data=well[well['WELL Name']==w], hue='Test', orient='v' ,showfliers = False, ax=ax[0])
    sns.boxplot(y='Oil Flow Sm3/d', x='CHOKE', data=well[well['WELL Name']==w], hue='Test', orient='v' , showfliers = False,ax=ax[1])
    sns.boxplot(y='Water Flow Rate m3/d', x='CHOKE', data=well[well['WELL Name']==w], hue='Test',orient='v' , showfliers = False,ax=ax[2])

    #sns.boxplot(y='Sep. Static Pressure psig', x='CHOKE', data=well[well['WELL Name']==w], hue='Test',orient='v' , showfliers = False,ax=ax[1])
    #sns.boxplot(y='Sep. Gas Temp deg C', x='CHOKE', data=well[well['WELL Name']==w], hue='Test',orient='v' , showfliers = False,ax=ax[2])
    
    plt.show()
    #print(well[well['WELL Name']==w].describe())


![image](https://user-images.githubusercontent.com/31476977/114443352-f8bc5a00-9ba3-11eb-94a8-eb272e145b06.png)
![image](https://user-images.githubusercontent.com/31476977/114443391-02de5880-9ba4-11eb-8858-5af2dd2687c9.png)

    

