# Global iPhone Market Share Analysis using Python 

## Introduction 
"A market share is the percentage of total sales in an industry generated by a particular company" (Investopedia). It is calculated by dividing the company's total revenues by the total sales of the whole industry during a specific period of time. 

Market share is important because it provides invaluable information to the company to determine specific plans and actions that the company can take based on its market share outlook. Every company that is looking to grow must expand its market share. A company can easily determine its growth rate by measuring the yearly or quarterly assesment of its market share and comparing it to the historical performance of the company. 

iOS is the mobile operating system developed by Apple for its products such as the iPhone and iPad. It is the second largest market share for mobile operating systems behind Android. 

## Business Task 
Analyze the dataset for the market share of iPhone and iOS to identify patterns that can be used to determine production volumes for iPhones for the next fiscal year. 

## Ask
1. Is the market share analysis global or regional?
2. What are some patterns that can be identified between global market share of iOS & Andorid and the volume of iPhone sales? 
3. How can these patterns be used to determine production volumes for the next fiscal year? 

## Prepare 

### Data Information
The dataset used was pulled from Kaggle [here](https://www.kaggle.com/datasets/mohamedfahim003/global-iphone-and-smartphone-market-2011-2023).

The license is available [here](https://www.mit.edu/~amini/LICENSE.md).

This is a primary dataset that was gathered by using publicly available information provided directly from Apple. There is no bias as this information is raw data provided from Apple for their yearly iPhone sales and usage of the iOS platform. 

### ROCCC
#### Reliable
This data is reliable as it contains raw data from Apple 
#### Original
The data is original as it is a primary data pulled directly from Apple. 
#### Comprehensive
The data is comprehensive as it extends from 2011 to 2023. 
#### Current 
Data is current since it contains data as recent as 2023. 
#### Cited 
This data is cited as it contains raw data provided by Apple 

## Process
Begin by importing necessary Python libraries and the dataset. I am using Replit for this analysis. 

```
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
iphone_data = pd.read_csv('Iphone_Dataset.csv')
print(iphone_data.head())
```

![image](https://github.com/user-attachments/assets/92209410-188b-446b-8699-cdb35b528de3)

Check data for any errors

```
iphone_data.info()
```

![image](https://github.com/user-attachments/assets/3088996d-f86f-4afc-a996-3fe4e6f106ec)

Although there are some missing values in "Percentage_of_iPhone_Users", "No_of_iPhone_Sold_USA", "iOS_Market_Share", and "Android_Market_Share", I have decided to keep the data as is to avoid missing an entire year's worth of data for this analysis. 

Finally, I sorted the "Year" column by ascending order. 

```
iphone_data_sorted = iphone_data.sort_values(by=['Year'])

print(iphone_data_sorted.head())
```

![image](https://github.com/user-attachments/assets/328698f2-7c92-4752-916d-76ab1ea0fdb7)

## Analyze

### US iPhone Users vs. Global iPhone Users  
To begin, I have created a line graph to compare the amount of iPhone users in the US compared to the rest of the world. 

```
import matplotlib.pyplot as plt
import numpy as np

plt.plot(iphone_data_sorted['Year'], iphone_data['No_of_iPhone_Users'], label='No. of iPhone Users Globally', marker='.')
plt.plot(iphone_data_sorted['Year'], iphone_data['No_of_iPhone_Users_USA'], label ='No. of iPhone Users USA', marker='.')
plt.legend()
plt.title('No. of iPhone Users')
plt.xlabel('Year')
plt.ylabel('Number of Users')
plt.show()
```

![image](https://github.com/user-attachments/assets/5d6e0907-2afc-4fd1-bb14-4e38d594be56)

As expected, global iPhone users far outpace the amount of users in the US. However, what is surprising is the rate of growth in the global iPhone market compared to the rest of the world. 

The amount of iPhone users in the US has stagnated the last decade without any noticeable increase in users. On the other hand, the global iPhone market has been exploding rapidly with new users.  

This suggest that Apple should focus on meeting key production targets for the global market rather than the US market. The US market has been fully saturated and noticeable gains in users will be unlikely. 

I added two more columns to the database for the yearly percent increase for the amount of iPhones sold in the US and globally for better analysis.

```
iphone_data_sorted['Percent_Increase_iPhone_Users'] = iphone_data_sorted['No_of_iPhone_Users'].pct_change(periods=1) * 100

iphone_data_sorted['Percent_Increase_iPhone_Users_USA'] = iphone_data_sorted['No_of_iPhone_Users_USA'].pct_change(periods=1) * 100
```

```
plt.plot(iphone_data_sorted['Year'], iphone_data_sorted['Percent_Increase_iPhone_Users'], label='Percent Increases of iPhone Users Globally', marker='.')
plt.plot(iphone_data_sorted['Year'], iphone_data_sorted['Percent_Increase_iPhone_Users_USA'], label ='Percent Increase of iPhone Users USA', marker='.')
plt.legend()
plt.title('Percent Increase of iPhone Users')
plt.xlabel('Year')
plt.ylabel('Percent')
plt.show()
```

![image](https://github.com/user-attachments/assets/e6e98e47-ba57-4f07-8aa9-ab1c6aed6798)

The graph reveals that both the global and US market demand for iPhones have been steadily decreasing the last decade. Yet, it is important to note that the global market still has a higher year to year growth rate compared to the US market, further supporting the notion that Apple should be focused more on the global market than the domestic market for iPhones. 

Finally, I calculated the average growth rate for iPhone users in both the US and global market for the last 5 years. 

```
print('The average growth rate for the global market is ', statistics.mean(iphone_data_sorted['Percent_Increase_iPhone_Users'][8:]),'%')

print('The average growth rate for the US market is ', statistics.mean(iphone_data_sorted['Percent_Increase_iPhone_Users_USA'][8:]),'%')
```

![image](https://github.com/user-attachments/assets/ccb4b33a-7350-42e6-b678-6fbb6bf4f70e)

The average growth rate for iPhone users in the US market was 3.805%. The rate for the global market was 10.632%. Both these rates can be used to determine the production volume for iPhones in the US and global market. 

### Number of iPhone Users vs. iPhones Sold by Year 
I created a graph to compare the number of global iPhone users to global iPhone sales. 

```
plt.plot(iphone_data_sorted['Year'], iphone_data['No_of_iPhone_Users'], label='No of iPhone Users Globally', marker='.')
plt.plot(iphone_data_sorted['Year'], iphone_data['No_of_iPhone_Sold'], label ='No of iPhone Sold Globally', marker='.')
plt.legend()
plt.title('Number of Global iPhone Users vs iPhone Sales')
plt.xlabel('Year')
plt.ylabel('Count')
plt.show()
```

![image](https://github.com/user-attachments/assets/97de82a3-b6b6-4c23-9b94-a68ec85bd5da)

As shown by the graph, despite a stagnation in the amount of global iPhones sold, the number of global iPhone users have been steadily increasing. This suggests that users that have purchased iPhones in the past continue to use iPhones, resulting in the cumulative increase of global iPhone users. One can safely assume from this discovery that iPhone users are satisfied with their iPhones and will continue to use iPhones as long as the product does not become defective or of lower quality. Thus, Apple should avoid cost saving directives that directly affect the quality of the iPhone. Also, Apple can produce iPhones at a similar rate to previous years due to the lack of fluctuation in sales. 

### iOS Market Share vs. Android Market Share 
Finally, I created a bar graph to compare the global market share for iOS and Android. 

```
plt.bar(iphone_data_sorted['Year'], iphone_data_sorted['iOS_Market_Share'], label='iOS Market Share')
plt.bar(iphone_data_sorted['Year'], iphone_data_sorted['Android_Market_Share'], label='Android Market Share')
plt.xlabel("Year")
plt.ylabel("Market Share Percentage")
plt.title("Market Share iOS vs. Android")
plt.legend() 
plt.show()
```

![image](https://github.com/user-attachments/assets/650d4594-bcb5-4b67-8932-c56c943a4d2d)

The graph illustrates that although Android was gaining traction from 2013 to 2015, it has not been able to take any more market share from Apple. On the contrary, Android's market share began to slow down during 2016 and has been slowly losing its market share. There was a noticeable increase in market share for Android during 2021 and 2022 before falling back down. 

The data suggests that whatever Apple has been doing the last decade has been working. iOS still remains the industry leader while Android has been slowly losing its market share. Although there may be years that Android will gain traction due to new devices being released, iOS and Apple still remain as the consumers' favorite. As such, Apple should not be swayed by year to year changes in market-share, but should be focused on the overrall market share trends over several years. 

## Share 

## Act 

https://amankharwal.medium.com/data-analysis-projects-with-python-a262a6f9e68c
