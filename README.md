# PyBer Analysis

## Overview

In this analysis we review customer and driver datasets provided by the ride-sharing app PyBer. Our goal is to provide a summary of the data that informs management how much money their drivers are earning in different city types (Urban, Suburban and Rural). We will import multiple datasets representing drivers and the rides they provide to customers, merge them together, then provide an initial summary. While emphasizing the types of cities, we'll extract date that shows total rides, total drivers, total fares, average fare per ride and per driver, as well as the total fare by city type. We will provide a series of charts that illustrate which city types tend to be the most profitable over time.


## Results


### Total Rides

From the merged dataframe `pyber_data_df`, we count all unique ride IDs and group them by city type. The data shows 1625 urban rides, 625 suburban rides, and 125 rural rides.

    rides_per_city_type = pyber_data_df.groupby('type').count().ride_id
    rides_per_city_type
    
    >>> type
    >>> Rural        125
    >>> Suburban     625
    >>> Urban       1625
    >>> Name: ride_id, dtype: int64


### Total Drivers

To find the total number of drivers per city type, we add together the `driver_count` of the `city_data_df` dataframe, then group them by city type. Note: We don't want to use the merged `pyber_data_df` dataframe for this, because the sums would include highly redundant data and would return inaccurate results. Here we see that there are 2405 urban drivers, 490 suburban drivers, and 78 rural drivers.

	total_drivers_per_city_type = city_data_df.groupby('type').sum().driver_count
	total_drivers_per_city_type

    >>> type
    >>> Rural         78
    >>> Suburban     490
    >>> Urban       2405
    >>> Name: driver_count, dtype: int64


### Total Fares

By summing the `fare` column of the `pyber_data_df` and grouping by city type, we can see that urban areas earned $39,854.38, suburban areas earned $19,356.33, and rural areas earned $4,327.93.

	total_fares = pyber_data_df.groupby('type').sum().fare
	total_fares

    >>> type
    >>> Rural        4327.93
    >>> Suburban    19356.33
    >>> Urban       39854.38
    >>> Name: fare, dtype: float64

### Average Fare per Ride

Here we determine the average fare per ride by using the `.mean()` function. We see that the average urban fare is $24.52, while the average suburban fare is 30.97 and the average rural fare is $34.62.

	average_fare = pyber_data_df.groupby('type').mean().fare
	average_fare

	>>> type
	>>> Rural       34.623440
	>>> Suburban    30.970128
	>>> Urban       24.525772
	>>> Name: fare, dtype: float64

![PyBer Ride-Sharing Data (2019)](https://github.com/bristlab/PyBer_Analysis/blob/main/analysis/Fig1.png?raw=true)

### Average Fare per Driver

Finding the average fare per driver is done by first summing the fairs of all rides in `pyber_data_df`, then dividing by the total drivers. The result states that the average fare per driver in urban areas is $16.57, while suburban and rural areas are $39.50 and $55.48 respectively.

	fare_per_driver = pyber_data_df.groupby('type').sum().fare / total_drivers_per_city_type
	fare_per_driver

	>>> type
	>>> Rural       55.486282
	>>> Suburban    39.502714
	>>> Urban       16.571468
	>>> dtype: float64


### Total Fare by City Type

Here we will extract the total amount of all fares per city type. Urban areas take in $39.854.38, suburban areas take in $19,356.33 and rural areas take in $4327.93.

	total_fares = pyber_data_df.groupby('type').sum().fare
	total_fares

	>>> type
	>>> Rural        4327.93
	>>> Suburban    19356.33
	>>> Urban       39854.38


## Summary


|  | Total Rides | Total Drivers | Total Fares | Average Fare per Rider | Average Fare per Driver
| ---|---|----|----|----|----
| Rural | 125 | 78 | $4,327.93 | $34.62 | $55.49
| Suburban | 625 | 490 | $19,356.33 | $30.97 | $39.50
| Urban | 1625 | 2405 | $39,854.38 | $24.53 | $16.57

![PyBer Ride-Sharing Data (2019)](https://github.com/bristlab/PyBer_Analysis/blob/main/analysis/PyBer_fare_summary.png?raw=true)

We know that urban areas offer the most rides when compared to suburban and rural areas. Urban areas also have the most drivers, which means more competition among drivers, which corresponds with the average fair per driver in urban areas being the lowest. Despite lower fares per ride, urban areas have the highest revenue than suburban and rural areas due to high ride volume.

Conversly, rural areas have the fewest rides, the fewest drivers, the highest fares per ride, and the lowest revenue of all three city types.

We recommend implementing measures that will reduce the price per fare in rural and suburban areas in order to incentivies ridership and increased ride volume. This could be done by utilizing revenue earned in urban areas to subsidize rides in suburban areas. This could be combined with promotions or frequent rider programs in those areas. Increasing the number of drivers will likely be necessary to facilitate the increase in demand. If these measures work, they could be expanded to rural areas as well.

Alternatively, dropping services in rural areas in order to focus on maximizing revenue in urban and suburban areas would be possible, although it's possible that urban markets are already oversaturated.