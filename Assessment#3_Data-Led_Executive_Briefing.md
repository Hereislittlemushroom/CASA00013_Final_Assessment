# The Analysis of the Trend of Airbnb Business, Policies and Impact of Covid-19 Pandemic in London, UK

- CASA0013 Introduction to Programming for Spatial Analysts
- Student id: 20044050
- Word count: 2,398

## Executive Summary

This report provides a trend and comparison analysis of Airbnb listings change in London, UK in the last five years (from 2015 to 2020). The recommendations and their data evidence are given below:

- The fundamentals of Airbnb business show fast growth since 2015. The statistics of Airbnb listings increased from 20,000 in 2015 to 90,000 by 2020 in London (around 35% growth per year)

- The remarkably climbing demand for Airbnb listings can be witnessed in London since 2016. The average price of listings increased from 95 GBP (2016) to 125 GBP(2020), which means that there are nearly 7% growth for each year) Simultaneously, there was a downward trend can be seen in the average annual availability of listings counted in days from more than 240 in 2015 to nearly 120 in 2020, which means an upward trend in demand.

- The price change is later than that in supply (approximately two months).  The decreasing can be found in the data of Airbnb listings from March whilst the similar downward trend was observed in the price from early April. Besides, the number of Airbnb listings from recovered from late July while price rebound from October.

- It is highly recommended to invest and support Airbnb business in London. Although the covid-19 caused national wide lockdown did affect the Airbnb business a lot in London,  the demand and supply of Airbnb listings will recover quickly once the lockdown policy is relaxing

# Reproducible Analysis

```python
import pandas as pd
import matplotlib.pyplot as plt
import time
pd.options.display.max_rows = 999
```

## 1. Pre-Covid Analysis

Store the links of Airbnb listings datasets from 2015 to 2020 in dictionary "urls". These links can be found in the http://insideairbnb.com/get-the-data.html ("London, England, United Kingdom" > "show archived data"). The reason why the range of pre-covid data was chosen as shown below is that covid-19 outbreak in London started from 12 February 2020.

```python
urls = {}
urls[2015] = 'http://data.insideairbnb.com/united-kingdom/england/london/2015-04-06/visualisations/listings.csv'
urls[2016] = 'http://data.insideairbnb.com/united-kingdom/england/london/2016-02-02/visualisations/listings.csv'
urls[2017] = 'http://data.insideairbnb.com/united-kingdom/england/london/2017-03-04/visualisations/listings.csv'
urls[2018] = 'http://data.insideairbnb.com/united-kingdom/england/london/2018-04-08/visualisations/listings.csv'
urls[2019] = 'http://data.insideairbnb.com/united-kingdom/england/london/2019-02-05/visualisations/listings.csv'
urls[2020] = 'http://data.insideairbnb.com/united-kingdom/england/london/2020-02-16/visualisations/listings.csv'
```

The `urls` dictionary is shown below:

```python
urls
```

    {2015: 'http://data.insideairbnb.com/united-kingdom/england/london/2015-04-06/visualisations/listings.csv',
     2016: 'http://data.insideairbnb.com/united-kingdom/england/london/2016-02-02/visualisations/listings.csv',
     2017: 'http://data.insideairbnb.com/united-kingdom/england/london/2017-03-04/visualisations/listings.csv',
     2018: 'http://data.insideairbnb.com/united-kingdom/england/london/2018-04-08/visualisations/listings.csv',
     2019: 'http://data.insideairbnb.com/united-kingdom/england/london/2019-02-05/visualisations/listings.csv',
     2020: 'http://data.insideairbnb.com/united-kingdom/england/london/2020-02-16/visualisations/listings.csv'}

First, create a new dictionary `df_summ_listing_per_year`. Then you can use `read_csv` to read all the urls in pandas dataframe format and create a new variable called `year` for each row in the dataframe.

```python
df_summ_listing_per_year = {}
# *** This might take for a while to read csv file (maybe less than 5 minutes) ***
for year in urls.keys():
    t0 = time.time()
    url = urls[year]
    print('Reading data from ', url)
    df_summ_listing = pd.read_csv(url)
    print('time taken', time.time()-t0, 'sec') # count the data loading time
    # create a new columns called "year" for each row in the dataframe
    df_summ_listing['year'] = year
    # add dataframes in these six years to the dictionary "df_summ_listing_per_year"
    df_summ_listing_per_year[year] = df_summ_listing
```

    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2015-04-06/visualisations/listings.csv
    time taken 4.388001441955566 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2016-02-02/visualisations/listings.csv
    time taken 5.754214763641357 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2017-03-04/visualisations/listings.csv
    time taken 7.79807710647583 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2018-04-08/visualisations/listings.csv
    time taken 9.582064151763916 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2019-02-05/visualisations/listings.csv
    time taken 10.551798105239868 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2020-02-16/visualisations/listings.csv
    time taken 10.302597522735596 sec

Merge these dataframes from dictionary `df_summ_listing_per_year` into a new dataframe called `df_combined`. Then, you can check all the variables by `head()` function (here I set the first 5 rows to output)

```python
df_combined = pd.concat(df_summ_listing_per_year.values())
# Overview of df_combined dataframe
df_combined.head(n=5)
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>name</th>
      <th>host_id</th>
      <th>host_name</th>
      <th>neighbourhood_group</th>
      <th>neighbourhood</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>room_type</th>
      <th>price</th>
      <th>minimum_nights</th>
      <th>number_of_reviews</th>
      <th>last_review</th>
      <th>reviews_per_month</th>
      <th>calculated_host_listings_count</th>
      <th>availability_365</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>600795</td>
      <td>London Zone1 LOFT 1Bed/1Lounge flat</td>
      <td>485861</td>
      <td>Lara</td>
      <td>NaN</td>
      <td>Tower Hamlets</td>
      <td>51.512390</td>
      <td>-0.063669</td>
      <td>Entire home/apt</td>
      <td>89</td>
      <td>2</td>
      <td>62</td>
      <td>2015-02-25</td>
      <td>2.1</td>
      <td>8</td>
      <td>355.0</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4530027</td>
      <td>Double room 20mins to Oxford Street</td>
      <td>23486604</td>
      <td>Jasmine</td>
      <td>NaN</td>
      <td>Barnet</td>
      <td>51.615380</td>
      <td>-0.144852</td>
      <td>Shared room</td>
      <td>100</td>
      <td>1</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1</td>
      <td>365.0</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>2</th>
      <td>896177</td>
      <td>Cosy room for 1 or 2 in Kennington</td>
      <td>4777568</td>
      <td>Cameron</td>
      <td>NaN</td>
      <td>Southwark</td>
      <td>51.491397</td>
      <td>-0.102909</td>
      <td>Private room</td>
      <td>65</td>
      <td>2</td>
      <td>9</td>
      <td>2013-10-12</td>
      <td>0.4</td>
      <td>1</td>
      <td>352.0</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3770567</td>
      <td>Double Room with large garden</td>
      <td>11255553</td>
      <td>Mike</td>
      <td>NaN</td>
      <td>Islington</td>
      <td>51.547610</td>
      <td>-0.098068</td>
      <td>Private room</td>
      <td>45</td>
      <td>1</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1</td>
      <td>221.0</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4292560</td>
      <td>Superb 3BR House Notting Hill VP</td>
      <td>1432477</td>
      <td>Maxime And Fanny</td>
      <td>NaN</td>
      <td>Kensington and Chelsea</td>
      <td>51.518255</td>
      <td>-0.206391</td>
      <td>Entire home/apt</td>
      <td>399</td>
      <td>2</td>
      <td>10</td>
      <td>2015-03-01</td>
      <td>1.8</td>
      <td>100</td>
      <td>290.0</td>
      <td>2015</td>
    </tr>
  </tbody>
</table>
</div>

Now, you can count the frequency of samples grouped by `year` then make a visualisation.

```python
# plot number of listings in the past six years
fig_precovid_listings = df_combined.groupby('year')['id'].count().plot(color = 'darkgreen',linewidth=3).get_figure()
plt.title('Airbnb number of listings in London since 2015',fontsize=20)
plt.xlabel('Year',fontsize=18)
plt.ylabel('Frequency',fontsize=18)
```

    Text(0, 0.5, 'Frequency')

![png](/Img/output_14_1.png)

```python
# plot average listing price in the past six years
fig_precovid_price = df_combined.groupby('year')['price'].mean().plot(color = "royalblue",linewidth=3).get_figure()
plt.title('Airbnb average listing price in London since 2015',fontsize = 20)
plt.xlabel('Year',fontsize = 18)
plt.ylabel('Average price (GBP)',fontsize = 18)
```

    Text(0, 0.5, 'Average price (GBP)')

![png](/Img/output_15_1.png)

```python
# plot average availability days
fig_precovid_availability = df_combined.groupby('year')['availability_365'].mean().plot(color = "darkcyan",linewidth=3).get_figure()
plt.title('Airbnb average availability in 365 days in London since 2015',fontsize = 20)
plt.xlabel('Year',fontsize = 18)
plt.ylabel('Availability (days)',fontsize = 18)
```

    Text(0, 0.5, 'Availability (days)')

![png](/Img/output_16_1.png)

## 2 Impact of Covid-19 Analysis

Simultaneouly, according to the above process, create the dictionary `urls_covid` to store links.

```python
# load and read monthly data in the past two years
urls_covid = {}
urls_covid[202012] = 'http://data.insideairbnb.com/united-kingdom/england/london/2020-12-16/visualisations/listings.csv'
urls_covid[202011] = 'http://data.insideairbnb.com/united-kingdom/england/london/2020-11-06/visualisations/listings.csv'
urls_covid[202010] = 'http://data.insideairbnb.com/united-kingdom/england/london/2020-10-13/visualisations/listings.csv'
urls_covid[202009] = 'http://data.insideairbnb.com/united-kingdom/england/london/2020-09-11/visualisations/listings.csv'
urls_covid[202008] = 'http://data.insideairbnb.com/united-kingdom/england/london/2020-08-24/visualisations/listings.csv'
urls_covid[202007] = 'http://data.insideairbnb.com/united-kingdom/england/london/2020-07-14/visualisations/listings.csv'
urls_covid[202006] = 'http://data.insideairbnb.com/united-kingdom/england/london/2020-06-11/visualisations/listings.csv'
urls_covid[202005] = 'http://data.insideairbnb.com/united-kingdom/england/london/2020-05-10/visualisations/listings.csv'
urls_covid[202004] = 'http://data.insideairbnb.com/united-kingdom/england/london/2020-04-14/visualisations/listings.csv'
urls_covid[202003] = 'http://data.insideairbnb.com/united-kingdom/england/london/2020-03-15/visualisations/listings.csv'
urls_covid[202002] = 'http://data.insideairbnb.com/united-kingdom/england/london/2020-02-16/visualisations/listings.csv'
urls_covid[202001] = 'http://data.insideairbnb.com/united-kingdom/england/london/2020-01-09/visualisations/listings.csv'
# -------------------********-------------------
urls_covid[201912] = 'http://data.insideairbnb.com/united-kingdom/england/london/2019-12-09/visualisations/listings.csv'
urls_covid[201911] = 'http://data.insideairbnb.com/united-kingdom/england/london/2019-11-05/visualisations/listings.csv'
urls_covid[201910] = 'http://data.insideairbnb.com/united-kingdom/england/london/2019-10-15/visualisations/listings.csv'
urls_covid[201909] = 'http://data.insideairbnb.com/united-kingdom/england/london/2019-09-14/visualisations/listings.csv'
urls_covid[201908] = 'http://data.insideairbnb.com/united-kingdom/england/london/2019-08-09/visualisations/listings.csv'
urls_covid[201907] = 'http://data.insideairbnb.com/united-kingdom/england/london/2019-07-10/visualisations/listings.csv'
urls_covid[201906] = 'http://data.insideairbnb.com/united-kingdom/england/london/2019-06-05/visualisations/listings.csv'
urls_covid[201905] = 'http://data.insideairbnb.com/united-kingdom/england/london/2019-05-05/visualisations/listings.csv'
urls_covid[201904] = 'http://data.insideairbnb.com/united-kingdom/england/london/2019-04-09/visualisations/listings.csv'
urls_covid[201903] = 'http://data.insideairbnb.com/united-kingdom/england/london/2019-03-07/visualisations/listings.csv'
urls_covid[201902] = 'http://data.insideairbnb.com/united-kingdom/england/london/2019-02-05/visualisations/listings.csv'
urls_covid[201901] = 'http://data.insideairbnb.com/united-kingdom/england/london/2019-01-13/visualisations/listings.csv'
```

```python
# *** This might take for a while to read csv file (maybe less than 5 minutes) ***
# read csv into DataFrames and save into a dictionary 
df_summ_cov_listing_per_year = {}
for year in urls_covid.keys():
    t0 = time.time()
    url=urls_covid[year]
    print('Reading data from ', url)
    df_summ_cov_listing = pd.read_csv(url)
    print('time taken', time.time()-t0, 'sec')
    df_summ_cov_listing['year'] = year
    df_summ_cov_listing_per_year[year] = df_summ_cov_listing
```

    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2020-12-16/visualisations/listings.csv
    time taken 11.198619842529297 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2020-11-06/visualisations/listings.csv
    time taken 10.856090545654297 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2020-10-13/visualisations/listings.csv
    time taken 9.107778549194336 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2020-09-11/visualisations/listings.csv
    time taken 9.061921119689941 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2020-08-24/visualisations/listings.csv
    time taken 8.608404159545898 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2020-07-14/visualisations/listings.csv
    time taken 14.440271139144897 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2020-06-11/visualisations/listings.csv
    time taken 13.531993627548218 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2020-05-10/visualisations/listings.csv
    time taken 10.052074670791626 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2020-04-14/visualisations/listings.csv
    time taken 11.525549173355103 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2020-03-15/visualisations/listings.csv
    time taken 10.471135139465332 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2020-02-16/visualisations/listings.csv
    time taken 11.876988172531128 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2020-01-09/visualisations/listings.csv
    time taken 10.30359697341919 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2019-12-09/visualisations/listings.csv
    time taken 11.94169020652771 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2019-11-05/visualisations/listings.csv
    time taken 11.411057710647583 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2019-10-15/visualisations/listings.csv
    time taken 11.71405577659607 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2019-09-14/visualisations/listings.csv
    time taken 10.459508657455444 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2019-08-09/visualisations/listings.csv
    time taken 10.361687660217285 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2019-07-10/visualisations/listings.csv
    time taken 10.08323884010315 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2019-06-05/visualisations/listings.csv
    time taken 10.836713075637817 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2019-05-05/visualisations/listings.csv
    time taken 9.601900339126587 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2019-04-09/visualisations/listings.csv
    time taken 9.15566372871399 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2019-03-07/visualisations/listings.csv
    time taken 10.37789273262024 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2019-02-05/visualisations/listings.csv
    time taken 14.611492156982422 sec
    Reading data from  http://data.insideairbnb.com/united-kingdom/england/london/2019-01-13/visualisations/listings.csv
    time taken 11.676574945449829 sec

```python
# combined all the individual DataFrames
df_covid_combined = pd.concat(df_summ_cov_listing_per_year.values())
```

Then, we need to drop the null value when transform the type of data before observing the trend in the scale of month.

```python
# convert time format
df_covid_combined['time'] = pd.to_datetime(df_covid_combined['year'], format='%Y%m', errors='coerce').dropna()
```

Now, you can count the frequency of samples grouped by year then make a visualisation. The distribution of samples before and after covid-19 outbreak can be observed in this figure.

```python
# plot number of listings since 2019 and highlight the covid-19 outbreak date
fig_covid_listings = df_covid_combined.groupby('time')['id'].count().plot(color = 'red',linewidth=3).get_figure()
plt.title('Airbnb number of listings since 2019',fontsize = 20)
plt.xlabel('Year',fontsize = 18)
plt.ylabel('Frequency',fontsize = 18)
plt.axvline(x=pd.to_datetime('2020-02-12'), ymin=0, ymax=1,label='covid-19',linestyle = '--')
```

    <matplotlib.lines.Line2D at 0x7f1150414790>

![png](/Img/output_25_1.png)

```python
# plot average listing price
fig_covid_price = df_covid_combined.groupby('time')['price'].mean().plot(color = 'indianred',linewidth=3).get_figure()
plt.title('Airbnb Average Listing Price in London since 2019',fontsize = 20)
plt.xlabel('Month',fontsize = 18)
plt.ylabel('Average price (GBP)',fontsize = 18)
plt.axvline(x=pd.to_datetime('2020-02-12'), ymin=0, ymax=1,label='covid-19',linestyle = '--')
```

    <matplotlib.lines.Line2D at 0x7f113f51d4d0>

![png](/Img/output_26_1.png)

```python
# plot average availability days
fig_covid_availability = df_covid_combined.groupby('time')['availability_365'].mean().plot(color = "darkorange",linewidth=3).get_figure()
plt.title('Airbnb average availability in 365 days since 2019',fontsize = 20)
plt.xlabel('Month',fontsize = 18)
plt.ylabel('Availability (days)',fontsize = 18)
plt.axvline(x=pd.to_datetime('2020-02-12'), ymin=0, ymax=1,label='covid-19',linestyle = '--')
```

    <matplotlib.lines.Line2D at 0x7f113f495250>

![png](/Img/output_27_1.png)

# Executive Briefing

## 1 Introduction

In this report, Airbnb listings data was analysed in the past five years to gain some insights mainly from the following three aspects

- Policies and regulations regarding running Airbnb in London. We try to understand if government regulations have a big impact on the Airbnb business that we can find from the data provided on the website.

- Historical trend and future perspectives. We investigated the listing data in the past six years. We choose the most import factors that reflect the market activities, supply and demand.

- The impact of Covid-19. We process monthly data in the past two years, from Jan 2019 to the end of 2020 to investigate the trend in more details. From the same aspects in the previous part, we can see the Covid-19 impact in prominent in both supply and demand side.

## 2 Existing Policies

The official policies of Airbnb hosting in the UK are claimed below:

_"If you host a property in England, Scotland, or Wales that’s available to let for 140 days or more per year, the government deems it a self-catering property that’s subject to business rates."_ [1]

As mentioned in reference [2], we have the following policies for running Airbnb in London.

- The 90-day rule in London - In 2017 a short-term rental regulation was introduced in London which applies to entire home listings on Airbnb. The London-specific measure is designed to promote responsible home sharing, to limit the number of nights each year hosts and landlords can rent out their property.

- Holiday let accommodation - If the property is exempt from the 90-day rule, then it may be classed as a self-catering property or holiday let accommodation. This means that if we have guests for more than 140 nights a year, we may be liable to pay business rates.

- Contracts and leases - In addition to local and national laws, the host may need to comply with building lease, contract or regulations too.

When it comes to covid-19, in July 2020, the previous Lockdown Regulations (SI 350) was replaced with the new regulations[3] which allowed business activities partly.

## 3 Data Source

- The data set is from inside Airbnb website, _"an independent, non-commercial set of tools and data"_[4], which are based on publicly available data from Airbnb.

- The data are available back to 2015 but not all monthly data are available. Under this circumstance, we sample a subset of data for our analysis.

## 4 Historical Trend on Listing Data

### 4.1 Number of listings since 2015

- The total number of listings went up from 20k in 2015 to 90k by 2020, which represent an annualized growth of around 35%.

- The fast growth of the number of listings suggests a fast growth of Airbnb's fundamentals since 2015.

```python
fig_precovid_listings
```

![png](/Img/output_31_0.png)

### 4.2 Average listing price since 2015

- The initial dip of the price might due to the increase of the supply while the demand did not go up fast enough accordingly.

- From 2016 the price is going up from 95 to more than 125, which is around 7% increase each year, this reflects the strongly increasing demand.

```python
fig_precovid_price
```

![png](/Img/output_33_0.png)

### 4.3 Average listings annual availability since 2015

- The average annual availability counted in days is going down from more than 240 to 120 in 2018.

- After 2018 the available days became stable above 120, which is a reflection that people usually make Airbnb appointment several months ahead.

- The downtrend is a reflection of the strong demand of the markets, and since 2018, the supply and demand are getting into an equilibrium.

```python
fig_precovid_availability
```

![png](/Img/output_35_0.png)

## 5 The impact of Covid-19

### 5.1 Number of listings since 2019

According to reference[5], the ninth case of coronavirus was found in the UK, which may mark that covid-19 outbreak started from 12 February 2020 (as shown in the figure below).

- The monthly number of listings data peaked in March 2020 when the government ordered national wide lockdown regulations [6]. 

- The number of listings went down quickly from 8,8000 to 7,4000 until late July when the lockdown was relaxing. 

```python
fig_covid_listings
```

![png](/Img/output_38_0.png)

### 5.2 Average listing price since 2019

- The average listing price peaked at April, which is a reflection of the decreasing of the demand which is at a faster rate than the decrease of the supply.

- Price rebound from October which is a reflection of the rebound of the demand.

- It shows that the price change is lagged one to two months than the supply change.

```python
fig_covid_price
```

![png](/Img/output_40_0.png)

### 5.3 Average listings availability since 2019

- The availability data is volatile but in the range of 120 over 2020.

- The level of available data suggest that both supply and demand decreased simultaneously, and the price adjustment contributed as well.

- The market is shrunk but remain robust in terms of the operation suggested by the availability date.

```python
fig_covid_availability
```

![png](/Img/output_42_0.png)

## Summary

- The Airbnb business is growing very fast in the past five years and the momentum should remain in the future after Covid recovery.

- The regulations introduced in 2017 does not affect the Airbnb business from the data above and we assume there is not a strong reason to change the regulations.

- The Covid caused national lockdown did affect the Airbnb business a lot, which caused both decreases in demand and supply. But as long as the lockdown is released, the demand and supply will recover quickly.

- Overall, we see Airbnb is a strong and robust business and worth long term investments.

### References

- [1]Responsible hosting in the United Kingdom. (2021). Retrieved 10 January 2021, from https://www.airbnb.co.uk/help/article/1379/responsible-hosting-in-the-united-kingdom#taxes    

- [2]Important Airbnb regulations and laws you should know about in London - Hostmaker Blog. (2018). Retrieved 10 January 2021, from https://hostmaker.com/blog/important-airbnb-regulations-country-laws-know-london/

- [3]The Health Protection (Coronavirus, Restrictions) (No. 2) (England) Regulations 2020. (2021). Retrieved 10 January 2021, from https://www.legislation.gov.uk/uksi/2020/684/contents/made/data.htm

- [4]Get the Data. (2021). Retrieved 10 January 2021, from http://insideairbnb.com/about.html

- [5]BBC News Services. (2020). Coronavirus: Ninth case found in UK. Retrieved from https://www.bbc.com/news/uk-51481469

- [6]The Health Protection (Coronavirus, Restrictions) (England) Regulations 2020. (2021). Retrieved 13 January 2021, from https://www.legislation.gov.uk/uksi/2020/350/regulation/6/2020-03-26
