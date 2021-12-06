# Tagvenue ML Pricing Prediction
![alt text](images/tag_venue_home_page.png)
The [Tagvenue](https://www.tagvenue.com/) website is basically an Air BnB for finding and booking venues for an event. The website hosts thousands of venues in the UK that can be booked for events such as weddings, work drinks, birthdays etc. Each venue has one or more **spaces** available to be booked.

In this project, we have scraped all **London** event spaces from the Tagvenue website. We plan to clean and model this data to predict the price of event spaces in London using predictors such as capacity, area, location, facilities, licences etc. This repository will be updated as we make progress. 

## Notebooks

- **Tag_Venue_Scrape.ipynb** - Performs web scrape of Tagvenue, extracting data from all event spaces in London and creates 2 datasets: *tag_venue_space_data.csv* and *tag_venue_space_prices.csv*

## Datasets

At present, we only have the raw scraped data. This data is split into 2 tables as outlined below: 

- **tag_venue_space_data.csv**: Stores general information on each space, e.g. location, area, capacity, catering details, features etc. One row per event space. 
- **tag_venue_space_prices.csv**: Stores price data for each space. The price data is a bit complex, with prices shown for different days of the week and for different time periods e.g. per hour or per day. Each row is one price offering for a single space on a single day of the week. Each space will have many price offerings and thus each space will have many rows in the csv.

## Metadata
### tag_venue_space_data.csv
Data |Data type|Description
:---|:---:|:---
space_url|string|url of event space's web page on Tagvenue.com
venue_url|string|url of the venue web page on Tagvenue.com. The venue owns the space i.e. the event space resides within the venue. 
venue_name|string|Name of venue. The venue owns the space, i.e. the space resides within the venue. 
space_name |string|Name of event space within venue
latitude|float|Latitude of venue
longitude|float|Longitude of venue
address|string|Address of venue
nearest_tube_station|string|Nearest tube station to venue, includes distance from nearest tube in feet when available 
max_seating|int|maximum seating capacity of event space
max_standing|int|maximum standing capacity of event space
area_in_msqrd|int|Area of event space in metres squared
catering_offered_by_venue|bool|Is catering offered by the venue for this event space (True / False)
external_catering_allowed|bool|Is external catering allowed for this event space (True/False)
supervenue|bool|Is this venue a supervenue (True / False) - 'Supervenue program is based on our customers' feedback and highlights venues that are most dedicated to providing outstanding hospitality, customer service and event experience' 
capacity section: columns 'Boardroom_max' to 'Classroom_max'|int|Each column header describes a different available layout e.g. 'Boardroom_max' is the boardroom layout. The value is the maximum capacity for the space when using that layout. The value will be missing if the space does not offer that layout. 
catering section part 1: columns 'Approved caterers only' to 'Venue provides alcohol'|int (1 or 0)|Each column header is a description of whether the venue does or does not provide a certain catering option. E.g. 'BYO alcohol not allowed' and 'BYO alcohol allowed'. These columns contain either a 1 or 0 to indicate which statement is correct for this venue. The pairs of contradicting statements are mutually exclusive such that if 'BYO alcohol not allowed' is 1 then 'BYO alcohol allowed' should be 0. The 'Approved Caterers Only' column has no contradicting column, i.e. there is no 'Unapproved Caterers Allowed' column. 
catering section part 2: columns 'Buyout fee for external catering' to 'Alcohol licence until 21:00'|bool|Each column header is a catering option (e.g. 'Halal menu') and the value will be True or False to indicate if the space offers that catering option.  If the value is missing, then the web page for the space did not indicate whether this catering option is available or not. 
features section: columns 'Wi-Fi' to 'Disabled access toilets'|bool|Each column header is a feature option (e.g. 'Wi-Fi') and the value will be True or False to indicate if the space offers that feature option.  If the value is missing, then the web page for the space did not indicate whether this feature option is available or not.

### tag_venue_space_prices.csv
Data |Data type|Description
:---|:---:|:---
space_url|string|url of the space web page on Tagvenue.com
venue_name|string|Name of venue
space_name |string|Name of event space within venue
latitude|float|Latitude of venue
longitude|float|Longitude of venue
day_of_week|string|Day of week the price is for e.g. 'Monday' means this is the Monday price. 
pricing_period|string|Description of time period that that you can reserve the space for at this price e.g. 'per morning' 
time_period|string|Hours the space will be booked for at this price
price|string|Price in UK £s to book the space for the given day_of_week and pricing_period / time_period. This can be a combined price e.g. '£50 + £100' which is why it is a string datatype. The price_type column will indicate what each of the two prices quoted refer to. 
price_type|string|Type of pricing e.g. 'min spend',  'hire' etc. or in the case of a combined price it could be 'min spend + hire' 
