# Comparing-GDP-Population-of-the-World-s-Most-Populous-Countries-in-2007-
Bar chart comparing populations in millions, with GDP in millions, formatted for Jupyter Notebook.

![Comparing GDP   Population of the World's Most Populous Countries in 2007](https://user-images.githubusercontent.com/48648985/55398086-943f7c80-553f-11e9-95a9-65ef25a1851a.png)


import pandas as pd
from matplotlib import pyplot as plt

data = pd.read_csv('countries.csv')
data.head()

### Finding the 10 most populous countries:

data_2007 = data[data.year == 2007]
top10 = data_2007.sort_values('population', ascending=False).head(10)

print(top10)

import numpy as np
#### Importing np for np.arange().
#### np.arange(10) is similar to range(10), and it allows us to shift
####  each value in it by the bar width as you can see below.
x = np.arange(10)

### Creating subplots in order to overlay two bar plots
### with proper axes on the left hand side and the right hand side.
fig, ax1 = plt.subplots()

width = 0.3 # This is the width of each bar in the bar plot.
plt.xticks(x, top10.country, rotation=45)
population = ax1.bar(x, top10.population / 10**6, width, color='lightgreen')
plt.ylabel('Population', fontsize='14')

##### ax1.twinx() gives us the same x-axis with the y-axis on the right.
ax2 = ax1.twinx()
gdp = ax2.bar(x + width, top10.gdpPerCapita * top10.population / 10**9,
              width, color='hotpink')
plt.ylabel('GDP', fontsize='14')
plt.legend([population, gdp],
           ['Population in Millions', 'GDP in Billions'])
figure = plt.gcf() # get current figure

plt.title('Comparing GDP & Population of the World\'s Most Populous Countries in 2007',
         color='mediumseagreen', fontweight='bold', fontsize=15)
plt.show()
