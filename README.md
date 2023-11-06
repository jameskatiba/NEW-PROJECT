
import pandas as PD
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline

# Reading the sales CSV file from the local machine
data = pd.read_csv('Superstore data.csv')
data.head()

# Getting generate information about the data in the file i.e columns and rows
data.info()
# The data show that there are 21 columns 15 of object type, 3 with float type, and 3 with integer values
# The file has 9994 rows all populated with data in all the columns i.e there are no null columns

# Use the describe function to get the statistical summary of the numerical data in the file
data.describe()
# The outcome shows for instance in sales count count = 9994 sales with a mean of 229.858, std = 623.2451, 
# minimum = 0.444, median = 54.49, lower quartile = 17.28, upper quartile=209.94 and maximum = 22638.48 

#Extreacting the columns 'Ship Mode', 'Segment', 'City', 'Sales', 'Quantity', 'Discount', and 'Profit' from the main file
data subset = data[['Ship Mode', 'Segment', 'City', 'Sales', 'Quantity', 'Discount', 'Profit']]
# The first 15 records from the data subset
data subset.head(10)

# Quantity_sales subset
Quant_sales = {}
Quantity_sales =dataSubset[['Quantity', 'Sales']]
for i in Quantity_sales.Quantity.unique():
    Quant_sales[i] = [dataSubset['Sales'][v] for v in dataSubset[dataSubset["Quantity"] == i].index]
Total_sales ={}
for key, value in Quant_sales.items():
    Total_sales[key] = sum(value)
sale_T = Total_sales.items()
Sorted_sales = sorted(sale_T, key=lambda x: x[0])
x = dict(Sorted_sales).keys()
y = dict(Sorted_sales).values()
#plotting a bar plot for quantity against sales
fig, ax = plt.subplots()
ax.bar(x,y)
ax.set_ylabel('Total sales')
ax.set_xlabel('Quantity levels')
ax.set_title('Sales distribution per quantity');
# The result shows that sales were high for quantity levels 3 and 4 beyond 400000 sales in total for each
# Low sales are recorded for quantities 1,10,11,12,13 and 14 have 50000 and below sales.


# City_sales distribution
City_sales = {}
city_sales =dataSubset[['City', 'Sales']]
for i in city_sales.City.unique():
    City_sales[i] = [dataSubset['Sales'][v] for v in dataSubset[dataSubset["City"] == i].index]
Total_sales ={}
for key, value in City_sales.items():
    Total_sales[key] = sum(value)
sale_C = Total_sales.items()
Sorted_sales = sorted(sale_C, key=lambda x: x[1], reverse = True)
#There exist 531 cities taking a set of top 30 cities in sales
top_30_cities = Sorted_sales[0:30]
x = dict(top_30_cities).keys()
x_labels = np.arange(0,30)+1
y = dict(top_30_cities).values()
#plotting a bar graph presentation for the top 30 cities
SaleCity = sns.barplot(x=x_labels,y=y, hue = x)
sns.set_style('dark')
plt.legend(ncol=3);
# The chart shows that New York City recorded the highest sales over 250000 sales
# Only 6 cities out of 531 made sales over 50,000 thus majority of the cities made sales below 50000

# Creating a data frame for the correlation of sales, quantity, discount, and profit columns
corr_df=dataSubset[['Sales', 'Quantity', 'Discount', 'Profit']].corr()
corr_df


sns.heatmap(corr_df,cmap='coolwarm',vmin=-1,vmax=1,annot=True,square=True,annot_kws={'fontsize':11,'fontweight':'bold'});

data['Cost'] = data['Sales']-data['Profit']
data. columns

# Plotting a scatter plot for the Cost of product and sales.

Price_sales = sns.scatterplot(x='Cost',y='Sales',data=data)
Price_sales.set(title="Impact of product Cost on Sales");
# From the scatter plot, the majority of the items orders were of low cost, the number reduces with an increase in costs
