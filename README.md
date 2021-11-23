# tagvenue-ML-pricing-prediction
![alt text](images/tag_venue_home_page.png)
# Tagvenue Venue Web Scrape
### Introduction 

The [Tagvenue](https://www.tagvenue.com/) website is basically an Air BnB for finding and booking venues for an event. The website hosts thousands of venues in the UK that can be booked for events such as weddings, work drinks, birthdays etc. Each venue has one or more **spaces** available to be booked. A **space** is basically a room or area within the venue. Some venues have a single space, often the whole venue, whilst others offer a selection of rooms, each offered as a separate space. Each Space has its own webpage on Tagvenue. This webpage contains all the data needed to choose which space to book for your event. Example data includes price, location, size, capacity, features, licensing etc. This notebook will scrape the data from all spaces on the [Tagvenue](https://www.tagvenue.com/) website that are located in **London**. At the time of writing this amounts to **~4400** spaces. 

The data will be saved in 2 csv files detailed below: 
- **tag_venue_space_data.csv**: Stores general information on each space, e.g. location, area, capacity, catering details, features etc. One row per event space. 
- **tag_venue_space_prices.csv**: Stores price data for each space. The price data is a bit complex, with prices shown for different days of the week and for different time periods e.g. per hour or per day. Each row is one price offering for a single space on a single day of the week. Each space will have many price offerings and thus each space will have many rows in the csv.    
