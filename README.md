# S-P-500-stock-prices-2014-2017
### INTRODUCTION ###

A Python project for Historical 500 stock market data for current S&P 500 companies from 2014-2017.  Each record represents a single day of trading and includes the ticker name, volume, high, low, open, and close prices.

**Table of Contents**
  - Project Overview
  - Project scope
  - Business objectives 
  - Document purpose 
  - Use case
  - Data source
  - Data overview
  - Data cleaning and processing
  - Data Visualization
  - Recommendation

### Project Overview:

This project involves an exploratory data analysis (EDA) of historical stock price data for S&P 500 companies between January 2, 2014, and December 29, 2017. The goal is to uncover patterns, answer specific business questions, and draw investment insights from the dataset using Python.

### Project Scope:

- Analyze trading volume trends across dates and weekdays
- Identify the most volatile day for Amazon (AMZN)
- Discover the most actively traded stocks on high-volume days
- Evaluate investment performance over time
- Deliver insights that could inform future trading or investment decisions.

### Business Objectives:

 - Determine peak trading activity periods
 - Understand which weekdays typically see more or less market activity
 - Identify potential investment opportunities based on historical growth
 - Analyze stock volatility for risk assessment

**Document Purpose**

This document outlines the steps taken to clean, analyze, and draw insights from the dataset. It serves as a reference for showcasing analytical thinking and Python programming skills for a data analyst portfolio.

**Use Case**

A potential investor or financial analyst could use this analysis to:

 - Time the market for better trading volume
 - Evaluate historical stock performance
 - Understand volatility in high-profile stocks like AMZN
 - Identify trends useful for portfolio strategy

**Data Source**

- Dataset: S&P 500 Stock Prices (2014–2017)
- Format: CSV
- Fields: symbol, date, open, high, low, close, volume
- Source: [Maven Analytics](https://mavenanalytics.io/data-playground?dataStructure=Single%20table&order=number_of_records%2Cdesc)

**Data Overview**
 - Date Range: 2014-01-02 to 2017-12-29
 - Number of Companies: 500+ unique symbols
 - Key Metrics: Daily price (open, high, low, and close), trading volume
 - Total Records: ~1.5 million rows (based on date & symbol combinations.

**Data Cleaning and Processing**

 - Converted date column to date-time format
 - Extracted days of the week from dates
 - Handled grouped aggregations to compute total volumes and volatility
 - Calculated percentage gain from start to end of dataset per stock
 - Filtered records for specific dates (e.g., 2015-08-24, 2014-01-02, 2017-12-29)

**Data Visualization**

This showcases visual insights derived from data analysis projects, using Python (Pandas, Matplotlib, Numpy, Seaborn) to transform the datasets into clear, actionable visuals. Each visualization highlights key trends, patterns, and outcomes that support data-driven decision making.

 - Top 10 Most Traded Stocks by Volume
 ```
  top_volume = df_clean.groupby('symbol')['volume'].sum().sort_values(ascending=False).head(10)

plt.figure(figsize=(10, 6))
top_volume.plot(kind='bar', color='skyblue')
plt.title('Top 10 Most Frequently Traded Stocks (2014–2017)', fontsize=14)
plt.ylabel('Total Volume Traded')
plt.xlabel('Stock Symbol')
plt.xticks(rotation=45)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.tight_layout()
plt.show()

```
![](https://github.com/Abdulquadri2025/same-thing/blob/main/Top%2010%20Most%20frequently%20traded%20stock.png)

- Daily Average Closing Price (All Stocks)
 ```
daily_avg_close = df_clean.groupby('date')['close'].mean()

plt.figure(figsize=(12, 5))
daily_avg_close.plot()
plt.title('Average Daily Closing Price of All S&P 500 Stocks (2014–2017)')
plt.xlabel('Date')
plt.ylabel('Average Close Price')
plt.grid(True)
plt.tight_layout()
plt.show()
```
![](https://github.com/Abdulquadri2025/same-thing/blob/main/Average%20daily%20closing%20price.png)

- Price Trend of Selected Stocks (e.g., AAPL, MSFT, GOOG)
```
selected_stocks = ['AAPL', 'MSFT', 'GOOG']
plt.figure(figsize=(12, 6))

For stock in selected_stocks:
    stock_data = df_clean[df_clean['symbol'] == stock]
    plt.plot(stock_data['date'], stock_data['close'], label=stock)

plt.title('Stock Price Trend (2014–2017)')
plt.xlabel('Date')
plt.ylabel('Close Price')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show(

```
![](https://github.com/Abdulquadri2025/same-thing/blob/main/Stock%20Price%20Trend.png)

- Monthly Heatmap of Average Close Price (e.g., for AAPL)
```
aapl = df_clean[df_clean['symbol'] == 'AAPL']
aapl['month'] = aapl['date'].dt.to_period('M')
monthly_avg = aapl.groupby('month')['close'].mean().unstack().reset_index()
monthly_avg_df = aapl.groupby([aapl['date'].dt.year, aapl['date'].dt.month])['close'].mean().unstack()

plt.figure(figsize=(10, 6))
sns.heatmap(monthly_avg_df, cmap="YlGnBu", annot=True, fmt=".1f")
plt.title('AAPL Monthly Average Close Price')
plt.xlabel('Month')
plt.ylabel('Year')
plt.tight_layout()
plt.show()

```
![](https://github.com/Abdulquadri2025/same-thing/blob/main/AAPL%20Monthly%20Average%20Close%20Price.png)

- Numpy Analysis: Percent Change and Moving Average
```
aapl_sorted = aapl.sort_values(by='date')
aapl_sorted['pct_change'] = aapl_sorted['close'].pct_change() * 100
aapl_sorted['moving_avg_30'] = aapl_sorted['close'].rolling(window=30).mean()

plt.figure(figsize=(12, 6))
plt.plot(aapl_sorted['date'], aapl_sorted['close'], label='AAPL Close')
plt.plot(aapl_sorted['date'], aapl_sorted['moving_avg_30'], label='30-Day Moving Avg', linestyle='--')
plt.title('AAPL Close Price & 30-Day Moving Average')
plt.xlabel('Date')
plt.ylabel('Price')
plt.legend()
plt.grid(True)

```
![](https://github.com/Abdulquadri2025/same-thing/blob/main/AAPL%20Close%20price%20and%2030%20days%20moving%20average.png)

**Recommendations**

 - Optimal Investment: Invest in the stock with the highest percentage gain over the period (identified during analysis)
 - High Volume Day Trading: Focus on Mondays if higher volume offers better liquidity
 - Risk Assessment: Use volatility insights (like Amazon’s most volatile day) for risk profiling
 - Market Monitoring: Watch for unusual spikes like the trading peak on August 24, 2015

**Conclusions**

This project demonstrates how Python can be used to analyze financial datasets, extract insights, and support investment decisions. The analysis uncovered key trends in trading volume, weekday patterns, and performance, providing valuable input for both novice and experienced investors.

Thank you

I am highly motivated to pursue a data analyst role within an organization where I can effectively apply my skills, take on new challenges, and continuously grow. I aim to contribute meaningfully to a team that values impact and innovation while advancing my professional development and the organization’s goals.
You can contact me at aregbeabdulquadri@gmail.com

**THANK YOU**













