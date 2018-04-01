
Your objective is to build a series of scatter plots to showcase the following relationships:

* Temperature (F) vs. Latitude
* Humidity (%) vs. Latitude
* Cloudiness (%) vs. Latitude
* Wind Speed (mph) vs. Latitude

* Randomly select **at least** 500 unique (non-repeat) cities based on latitude and longitude.
* Perform a weather check on each of the cities using a series of successive API calls. 
* Include a print log of each city as it's being processed with the city number, city name, and requested URL.
* Save both a CSV of all data retrieved and png images for each scatter plot.

3 Observations from the data:

1. Cities within lower latitude range(i.e. regions closer to the equator) have higher temperature ranges

2. Cities within higher latitude range (i.e. regions farther from the equator) have a wide range of humidity (range from low humidity % to high humidity %) 

3. Cities within higher latitude range are more likely to experience higher wind speed (up to 30 mph) compared to other cities which have wind speeds from 1 to 20 mph


```python
# Dependencies
import json
import requests
import random
import os
import csv
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt


from config import api_key
from citipy import citipy
from pprint import pprint
```


```python
#Create an empty list to store 500 random cities
city_list = []

#write the city list to csv
with open('city_data.csv', 'w', newline='') as newfile:  
        
    #initialize csv writer
    csvwriter = csv.writer(newfile, delimiter=',')  

    #write the city list to csv
    csvwriter.writerow(["City"])

    #Write a while loop to keep track of our list of cities. We want to make sure we have 500 unique cities.
    while len(city_list) < 500:  

        #generate random lat coordinates (bound between -90 and 90) and lng coordinates (bound between -180 and 180)
        lat = random.uniform(-90,90)
        lng = random.uniform(-180,180)
        
        #use the citypy library to generate the nearest city from the coordinates
        city = citipy.nearest_city(lat, lng).city_name
        
        #set the parameters to add to our base_url
        params = {
            "appid": api_key,
            "units": "imperial",
            "q": city
        }
        
        # Build the endpoint URL 
        base_url = "http://api.openweathermap.org/data/2.5/weather?"
        
        try:
            # Run a request to endpoint and get url
            weather_data = requests.get(base_url, params=params)
            
            #Raise the status to check for exception 
            weather_data.raise_for_status()
            
        except requests.exceptions.RequestException as e:
            
            #If there is an exception, print city does not exist
            print(f'{city} does not exist!')
            
            #continue with the try statement until it suceeds. Once it succeeds, move on to next statement
            continue
            
        #Since it suceeds, it means city is in openweathermap api, so check to see if city has been added to our list already
        if city not in city_list:
            
            #If city does not exist in our list, then add it
            city_list.append(city)
            
            #write the city to csv
            csvwriter.writerow([city])

```

    illoqqortoormiut does not exist!
    taolanaro does not exist!
    vaitupu does not exist!
    belushya guba does not exist!
    umzimvubu does not exist!
    samusu does not exist!
    belushya guba does not exist!
    rawannawi does not exist!
    acarau does not exist!
    barentsburg does not exist!
    jiddah does not exist!
    mys shmidta does not exist!
    mys shmidta does not exist!
    taolanaro does not exist!
    tabiauea does not exist!
    alotau does not exist!
    taolanaro does not exist!
    bengkulu does not exist!
    barentsburg does not exist!
    tumannyy does not exist!
    belushya guba does not exist!
    taolanaro does not exist!
    illoqqortoormiut does not exist!
    linshu does not exist!
    korla does not exist!
    barentsburg does not exist!
    marcona does not exist!
    barentsburg does not exist!
    taolanaro does not exist!
    taolanaro does not exist!
    tsihombe does not exist!
    ruatoria does not exist!
    attawapiskat does not exist!
    bentiu does not exist!
    kilakarai does not exist!
    kashi does not exist!
    illoqqortoormiut does not exist!
    severnyy does not exist!
    mys shmidta does not exist!
    sentyabrskiy does not exist!
    taolanaro does not exist!
    tsihombe does not exist!
    ust-bolsheretsk does not exist!
    taolanaro does not exist!
    taolanaro does not exist!
    illoqqortoormiut does not exist!
    attawapiskat does not exist!
    svetlyy does not exist!
    sorvag does not exist!
    palabuhanratu does not exist!
    grand river south east does not exist!
    belushya guba does not exist!
    amderma does not exist!
    bossembele does not exist!
    haibowan does not exist!
    belushya guba does not exist!
    illoqqortoormiut does not exist!
    yuzhno-yeniseyskiy does not exist!
    taolanaro does not exist!
    miranorte does not exist!
    tsihombe does not exist!
    sembe does not exist!
    louisbourg does not exist!
    olafsvik does not exist!
    saryshagan does not exist!
    stoyba does not exist!
    sentyabrskiy does not exist!
    barentsburg does not exist!
    solovetskiy does not exist!
    illoqqortoormiut does not exist!
    umzimvubu does not exist!
    tahta does not exist!
    bargal does not exist!
    amderma does not exist!
    kpagouda does not exist!
    toliary does not exist!
    karakendzha does not exist!
    illoqqortoormiut does not exist!
    attawapiskat does not exist!
    karkaralinsk does not exist!
    barentsburg does not exist!
    saleaula does not exist!
    sorvag does not exist!
    belushya guba does not exist!
    kerteh does not exist!
    belushya guba does not exist!
    akyab does not exist!
    karakendzha does not exist!
    sentyabrskiy does not exist!
    illoqqortoormiut does not exist!
    azimur does not exist!
    illoqqortoormiut does not exist!
    grand river south east does not exist!
    illoqqortoormiut does not exist!
    taolanaro does not exist!
    berikulskiy does not exist!
    tidore does not exist!
    barentsburg does not exist!
    aktas does not exist!
    barentsburg does not exist!
    belushya guba does not exist!
    tabiauea does not exist!
    barentsburg does not exist!
    grand river south east does not exist!
    paradwip does not exist!
    taolanaro does not exist!
    taolanaro does not exist!
    belushya guba does not exist!
    taolanaro does not exist!
    taolanaro does not exist!
    umzimvubu does not exist!
    bengkulu does not exist!
    taolanaro does not exist!
    cheuskiny does not exist!
    taolanaro does not exist!
    tsihombe does not exist!
    yanan does not exist!
    barawe does not exist!
    amderma does not exist!



```python
#read in the cities csv
city_data = pd.read_csv("city_data.csv")

#Add in columns needed to create our scatter plot
city_data["Cloudiness"] = ""
city_data["Country"] = ""
city_data["Date"] = ""
city_data["Humidity"] = ""
city_data["Lat"] = ""
city_data["Lng"] = ""
city_data["Max Temp"] = ""
city_data["Wind Speed"] = ""

city_data
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
      <th>City</th>
      <th>Cloudiness</th>
      <th>Country</th>
      <th>Date</th>
      <th>Humidity</th>
      <th>Lat</th>
      <th>Lng</th>
      <th>Max Temp</th>
      <th>Wind Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>lasa</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>1</th>
      <td>faanui</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>2</th>
      <td>ancud</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>3</th>
      <td>lakeside</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>4</th>
      <td>cabedelo</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>5</th>
      <td>cidreira</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>6</th>
      <td>gat</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>7</th>
      <td>mopipi</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>8</th>
      <td>san cristobal</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>9</th>
      <td>nikolskoye</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>10</th>
      <td>norman wells</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>11</th>
      <td>hermanus</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>12</th>
      <td>naze</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>13</th>
      <td>dikson</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>14</th>
      <td>butaritari</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>15</th>
      <td>mar del plata</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>16</th>
      <td>arman</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>17</th>
      <td>carnarvon</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>18</th>
      <td>mahebourg</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>19</th>
      <td>victoria</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>20</th>
      <td>vaini</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>21</th>
      <td>tual</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>22</th>
      <td>punta arenas</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>23</th>
      <td>comodoro rivadavia</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>24</th>
      <td>upernavik</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>25</th>
      <td>arraial do cabo</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>26</th>
      <td>busselton</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>27</th>
      <td>rikitea</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>28</th>
      <td>port hedland</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>29</th>
      <td>ushuaia</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>470</th>
      <td>chumikan</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>471</th>
      <td>tucumcari</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>472</th>
      <td>college</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>473</th>
      <td>griffith</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>474</th>
      <td>gigmoto</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>475</th>
      <td>port hardy</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>476</th>
      <td>peniche</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>477</th>
      <td>pochutla</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>478</th>
      <td>fort-shevchenko</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>479</th>
      <td>quang ngai</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>480</th>
      <td>laela</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>481</th>
      <td>tabou</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>482</th>
      <td>manyana</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>483</th>
      <td>hobyo</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>484</th>
      <td>high level</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>485</th>
      <td>am timan</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>486</th>
      <td>kladno</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>487</th>
      <td>margate</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>488</th>
      <td>abu kamal</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>489</th>
      <td>panzhihua</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>490</th>
      <td>saeby</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>491</th>
      <td>oussouye</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>492</th>
      <td>mattawa</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>493</th>
      <td>grand gaube</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>494</th>
      <td>police</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>495</th>
      <td>praya</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>496</th>
      <td>husum</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>497</th>
      <td>porto velho</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>498</th>
      <td>khilok</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>499</th>
      <td>nishihara</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>
<p>500 rows × 9 columns</p>
</div>




```python
#Create new csv file to log in the list of cities with their urls
with open('cities_url_log.csv', 'w', newline='') as newfile:
        
    #initialize csv writer
    csvwriter = csv.writer(newfile, delimiter=',')
    
    #Write the first line of the csv file
    csvwriter.writerow(["Beginning Data Retrieval"])
    csvwriter.writerow(["----------------------------"])

    #Loop through the 500 random cities, log their urls and store the data in dataframe
    for index, row in city_data.iterrows():
        
        #set params for query URL 
        params = {
            "appid": api_key,
            "units": "imperial",
            "q": row["City"]
        }

        # Build the endpoint URL 
        base_url = "http://api.openweathermap.org/data/2.5/weather?"

        # Run a request to endpoint and get url
        weather_data = requests.get(base_url, params=params)
        
        #Log the city and its url to a csv
        csvwriter.writerow([f"Processing City {index+1} | {row['City']}"])
        csvwriter.writerow([weather_data.url])
        
        #convert weather data to json
        weather_data_json = weather_data.json()
        
        #set the column values for each city in the dataframe 
        city_data.set_value(index, "Cloudiness", weather_data_json['clouds']['all'])
        city_data.set_value(index, "Country", weather_data_json['sys']['country'])
        city_data.set_value(index, "Date", weather_data_json['dt'])
        city_data.set_value(index, "Humidity", weather_data_json['main']['humidity'])
        city_data.set_value(index, "Lat", weather_data_json['coord']['lat'])
        city_data.set_value(index, "Lng", weather_data_json['coord']['lon'])
        city_data.set_value(index, "Max Temp", weather_data_json['main']['temp_max'])
        city_data.set_value(index, "Wind Speed", weather_data_json['wind']['speed'])


```

    /Users/danieltang/anaconda3/envs/PythonData/lib/python3.6/site-packages/ipykernel/__main__.py:35: FutureWarning: set_value is deprecated and will be removed in a future release. Please use .at[] or .iat[] accessors instead
    /Users/danieltang/anaconda3/envs/PythonData/lib/python3.6/site-packages/ipykernel/__main__.py:36: FutureWarning: set_value is deprecated and will be removed in a future release. Please use .at[] or .iat[] accessors instead
    /Users/danieltang/anaconda3/envs/PythonData/lib/python3.6/site-packages/ipykernel/__main__.py:37: FutureWarning: set_value is deprecated and will be removed in a future release. Please use .at[] or .iat[] accessors instead
    /Users/danieltang/anaconda3/envs/PythonData/lib/python3.6/site-packages/ipykernel/__main__.py:38: FutureWarning: set_value is deprecated and will be removed in a future release. Please use .at[] or .iat[] accessors instead
    /Users/danieltang/anaconda3/envs/PythonData/lib/python3.6/site-packages/ipykernel/__main__.py:39: FutureWarning: set_value is deprecated and will be removed in a future release. Please use .at[] or .iat[] accessors instead
    /Users/danieltang/anaconda3/envs/PythonData/lib/python3.6/site-packages/ipykernel/__main__.py:40: FutureWarning: set_value is deprecated and will be removed in a future release. Please use .at[] or .iat[] accessors instead
    /Users/danieltang/anaconda3/envs/PythonData/lib/python3.6/site-packages/ipykernel/__main__.py:41: FutureWarning: set_value is deprecated and will be removed in a future release. Please use .at[] or .iat[] accessors instead
    /Users/danieltang/anaconda3/envs/PythonData/lib/python3.6/site-packages/ipykernel/__main__.py:42: FutureWarning: set_value is deprecated and will be removed in a future release. Please use .at[] or .iat[] accessors instead



```python
city_data
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
      <th>City</th>
      <th>Cloudiness</th>
      <th>Country</th>
      <th>Date</th>
      <th>Humidity</th>
      <th>Lat</th>
      <th>Lng</th>
      <th>Max Temp</th>
      <th>Wind Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>lasa</td>
      <td>0</td>
      <td>CY</td>
      <td>1522539000</td>
      <td>82</td>
      <td>34.92</td>
      <td>32.53</td>
      <td>57.2</td>
      <td>5.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>faanui</td>
      <td>80</td>
      <td>PF</td>
      <td>1522539918</td>
      <td>99</td>
      <td>-16.48</td>
      <td>-151.75</td>
      <td>82.52</td>
      <td>13.04</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ancud</td>
      <td>0</td>
      <td>CL</td>
      <td>1522539926</td>
      <td>76</td>
      <td>-41.87</td>
      <td>-73.83</td>
      <td>53.54</td>
      <td>6.89</td>
    </tr>
    <tr>
      <th>3</th>
      <td>lakeside</td>
      <td>75</td>
      <td>US</td>
      <td>1522539180</td>
      <td>82</td>
      <td>32.86</td>
      <td>-116.92</td>
      <td>78.8</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>4</th>
      <td>cabedelo</td>
      <td>75</td>
      <td>BR</td>
      <td>1522537200</td>
      <td>88</td>
      <td>-6.97</td>
      <td>-34.84</td>
      <td>77</td>
      <td>5.82</td>
    </tr>
    <tr>
      <th>5</th>
      <td>cidreira</td>
      <td>92</td>
      <td>BR</td>
      <td>1522539928</td>
      <td>100</td>
      <td>-30.17</td>
      <td>-50.22</td>
      <td>67.54</td>
      <td>4.83</td>
    </tr>
    <tr>
      <th>6</th>
      <td>gat</td>
      <td>0</td>
      <td>SN</td>
      <td>1522537200</td>
      <td>53</td>
      <td>14.69</td>
      <td>-16.54</td>
      <td>75.2</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>7</th>
      <td>mopipi</td>
      <td>8</td>
      <td>BW</td>
      <td>1522539930</td>
      <td>88</td>
      <td>-21.2</td>
      <td>24.86</td>
      <td>68.12</td>
      <td>7.85</td>
    </tr>
    <tr>
      <th>8</th>
      <td>san cristobal</td>
      <td>75</td>
      <td>EC</td>
      <td>1522537200</td>
      <td>81</td>
      <td>-0.39</td>
      <td>-78.55</td>
      <td>53.6</td>
      <td>6.93</td>
    </tr>
    <tr>
      <th>9</th>
      <td>nikolskoye</td>
      <td>0</td>
      <td>RU</td>
      <td>1522537200</td>
      <td>85</td>
      <td>59.7</td>
      <td>30.79</td>
      <td>21.2</td>
      <td>2.71</td>
    </tr>
    <tr>
      <th>10</th>
      <td>norman wells</td>
      <td>75</td>
      <td>CA</td>
      <td>1522537200</td>
      <td>39</td>
      <td>65.28</td>
      <td>-126.83</td>
      <td>30.2</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>11</th>
      <td>hermanus</td>
      <td>24</td>
      <td>ZA</td>
      <td>1522539924</td>
      <td>92</td>
      <td>-34.42</td>
      <td>19.24</td>
      <td>54.44</td>
      <td>5.61</td>
    </tr>
    <tr>
      <th>12</th>
      <td>naze</td>
      <td>88</td>
      <td>NG</td>
      <td>1522539925</td>
      <td>93</td>
      <td>5.43</td>
      <td>7.07</td>
      <td>76.63</td>
      <td>7.78</td>
    </tr>
    <tr>
      <th>13</th>
      <td>dikson</td>
      <td>68</td>
      <td>RU</td>
      <td>1522539933</td>
      <td>82</td>
      <td>73.51</td>
      <td>80.55</td>
      <td>-1.81</td>
      <td>18.63</td>
    </tr>
    <tr>
      <th>14</th>
      <td>butaritari</td>
      <td>24</td>
      <td>KI</td>
      <td>1522539934</td>
      <td>99</td>
      <td>3.07</td>
      <td>172.79</td>
      <td>82.93</td>
      <td>15.28</td>
    </tr>
    <tr>
      <th>15</th>
      <td>mar del plata</td>
      <td>0</td>
      <td>AR</td>
      <td>1522539801</td>
      <td>80</td>
      <td>-46.43</td>
      <td>-67.52</td>
      <td>52.42</td>
      <td>4.21</td>
    </tr>
    <tr>
      <th>16</th>
      <td>arman</td>
      <td>40</td>
      <td>RU</td>
      <td>1522537200</td>
      <td>48</td>
      <td>59.7</td>
      <td>150.17</td>
      <td>21.2</td>
      <td>6.71</td>
    </tr>
    <tr>
      <th>17</th>
      <td>carnarvon</td>
      <td>0</td>
      <td>ZA</td>
      <td>1522539927</td>
      <td>78</td>
      <td>-30.97</td>
      <td>22.13</td>
      <td>44.95</td>
      <td>2.98</td>
    </tr>
    <tr>
      <th>18</th>
      <td>mahebourg</td>
      <td>75</td>
      <td>MU</td>
      <td>1522537200</td>
      <td>88</td>
      <td>-20.41</td>
      <td>57.7</td>
      <td>80.6</td>
      <td>10.29</td>
    </tr>
    <tr>
      <th>19</th>
      <td>victoria</td>
      <td>90</td>
      <td>BN</td>
      <td>1522537200</td>
      <td>94</td>
      <td>5.28</td>
      <td>115.24</td>
      <td>78.8</td>
      <td>1.74</td>
    </tr>
    <tr>
      <th>20</th>
      <td>vaini</td>
      <td>20</td>
      <td>IN</td>
      <td>1522539928</td>
      <td>88</td>
      <td>15.34</td>
      <td>74.49</td>
      <td>62.54</td>
      <td>1.07</td>
    </tr>
    <tr>
      <th>21</th>
      <td>tual</td>
      <td>68</td>
      <td>ID</td>
      <td>1522539929</td>
      <td>100</td>
      <td>-5.67</td>
      <td>132.75</td>
      <td>79.69</td>
      <td>9.57</td>
    </tr>
    <tr>
      <th>22</th>
      <td>punta arenas</td>
      <td>75</td>
      <td>CL</td>
      <td>1522537200</td>
      <td>66</td>
      <td>-53.16</td>
      <td>-70.91</td>
      <td>51.8</td>
      <td>19.46</td>
    </tr>
    <tr>
      <th>23</th>
      <td>comodoro rivadavia</td>
      <td>0</td>
      <td>AR</td>
      <td>1522537200</td>
      <td>81</td>
      <td>-45.87</td>
      <td>-67.48</td>
      <td>53.6</td>
      <td>2.24</td>
    </tr>
    <tr>
      <th>24</th>
      <td>upernavik</td>
      <td>8</td>
      <td>GL</td>
      <td>1522539686</td>
      <td>76</td>
      <td>72.79</td>
      <td>-56.15</td>
      <td>18.49</td>
      <td>3.2</td>
    </tr>
    <tr>
      <th>25</th>
      <td>arraial do cabo</td>
      <td>12</td>
      <td>BR</td>
      <td>1522539660</td>
      <td>87</td>
      <td>-22.97</td>
      <td>-42.02</td>
      <td>77.89</td>
      <td>20.04</td>
    </tr>
    <tr>
      <th>26</th>
      <td>busselton</td>
      <td>0</td>
      <td>AU</td>
      <td>1522539938</td>
      <td>100</td>
      <td>-33.64</td>
      <td>115.35</td>
      <td>58.94</td>
      <td>14.34</td>
    </tr>
    <tr>
      <th>27</th>
      <td>rikitea</td>
      <td>0</td>
      <td>PF</td>
      <td>1522539931</td>
      <td>100</td>
      <td>-23.12</td>
      <td>-134.97</td>
      <td>78.88</td>
      <td>9.64</td>
    </tr>
    <tr>
      <th>28</th>
      <td>port hedland</td>
      <td>40</td>
      <td>AU</td>
      <td>1522539000</td>
      <td>62</td>
      <td>-20.31</td>
      <td>118.58</td>
      <td>84.2</td>
      <td>8.05</td>
    </tr>
    <tr>
      <th>29</th>
      <td>ushuaia</td>
      <td>40</td>
      <td>AR</td>
      <td>1522537200</td>
      <td>70</td>
      <td>-54.81</td>
      <td>-68.31</td>
      <td>48.2</td>
      <td>8.05</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>470</th>
      <td>chumikan</td>
      <td>68</td>
      <td>RU</td>
      <td>1522540146</td>
      <td>66</td>
      <td>54.72</td>
      <td>135.31</td>
      <td>16.46</td>
      <td>3.71</td>
    </tr>
    <tr>
      <th>471</th>
      <td>tucumcari</td>
      <td>1</td>
      <td>US</td>
      <td>1522536780</td>
      <td>17</td>
      <td>35.17</td>
      <td>-103.73</td>
      <td>73.4</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>472</th>
      <td>college</td>
      <td>90</td>
      <td>US</td>
      <td>1522537080</td>
      <td>62</td>
      <td>64.86</td>
      <td>-147.8</td>
      <td>28.4</td>
      <td>5.77</td>
    </tr>
    <tr>
      <th>473</th>
      <td>griffith</td>
      <td>0</td>
      <td>AU</td>
      <td>1522540147</td>
      <td>52</td>
      <td>-34.29</td>
      <td>146.06</td>
      <td>73.84</td>
      <td>4.54</td>
    </tr>
    <tr>
      <th>474</th>
      <td>gigmoto</td>
      <td>80</td>
      <td>PH</td>
      <td>1522540148</td>
      <td>100</td>
      <td>13.78</td>
      <td>124.39</td>
      <td>77.57</td>
      <td>11.54</td>
    </tr>
    <tr>
      <th>475</th>
      <td>port hardy</td>
      <td>90</td>
      <td>CA</td>
      <td>1522537200</td>
      <td>66</td>
      <td>50.7</td>
      <td>-127.42</td>
      <td>48.2</td>
      <td>8.05</td>
    </tr>
    <tr>
      <th>476</th>
      <td>peniche</td>
      <td>0</td>
      <td>PT</td>
      <td>1522539000</td>
      <td>81</td>
      <td>39.36</td>
      <td>-9.38</td>
      <td>51.8</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>477</th>
      <td>pochutla</td>
      <td>75</td>
      <td>MX</td>
      <td>1522536600</td>
      <td>98</td>
      <td>15.74</td>
      <td>-96.47</td>
      <td>87.8</td>
      <td>11.41</td>
    </tr>
    <tr>
      <th>478</th>
      <td>fort-shevchenko</td>
      <td>0</td>
      <td>KZ</td>
      <td>1522540142</td>
      <td>100</td>
      <td>44.51</td>
      <td>50.26</td>
      <td>33.92</td>
      <td>13.33</td>
    </tr>
    <tr>
      <th>479</th>
      <td>quang ngai</td>
      <td>56</td>
      <td>VN</td>
      <td>1522540142</td>
      <td>96</td>
      <td>15.12</td>
      <td>108.8</td>
      <td>67.94</td>
      <td>2.48</td>
    </tr>
    <tr>
      <th>480</th>
      <td>laela</td>
      <td>48</td>
      <td>TZ</td>
      <td>1522540118</td>
      <td>92</td>
      <td>-8.57</td>
      <td>32.05</td>
      <td>56.42</td>
      <td>1.86</td>
    </tr>
    <tr>
      <th>481</th>
      <td>tabou</td>
      <td>80</td>
      <td>CI</td>
      <td>1522540143</td>
      <td>100</td>
      <td>4.42</td>
      <td>-7.36</td>
      <td>79.82</td>
      <td>6.85</td>
    </tr>
    <tr>
      <th>482</th>
      <td>manyana</td>
      <td>0</td>
      <td>AU</td>
      <td>1522537200</td>
      <td>53</td>
      <td>-35.26</td>
      <td>150.51</td>
      <td>77</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>483</th>
      <td>hobyo</td>
      <td>32</td>
      <td>SO</td>
      <td>1522540151</td>
      <td>92</td>
      <td>5.35</td>
      <td>48.53</td>
      <td>79.06</td>
      <td>6.33</td>
    </tr>
    <tr>
      <th>484</th>
      <td>high level</td>
      <td>20</td>
      <td>CA</td>
      <td>1522537200</td>
      <td>30</td>
      <td>58.52</td>
      <td>-117.13</td>
      <td>28.4</td>
      <td>6.93</td>
    </tr>
    <tr>
      <th>485</th>
      <td>am timan</td>
      <td>0</td>
      <td>TD</td>
      <td>1522540147</td>
      <td>34</td>
      <td>11.04</td>
      <td>20.28</td>
      <td>69.74</td>
      <td>6.78</td>
    </tr>
    <tr>
      <th>486</th>
      <td>kladno</td>
      <td>75</td>
      <td>CZ</td>
      <td>1522539000</td>
      <td>80</td>
      <td>50.15</td>
      <td>14.1</td>
      <td>42.8</td>
      <td>5.82</td>
    </tr>
    <tr>
      <th>487</th>
      <td>margate</td>
      <td>75</td>
      <td>AU</td>
      <td>1522539000</td>
      <td>51</td>
      <td>-43.03</td>
      <td>147.26</td>
      <td>62.6</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>488</th>
      <td>abu kamal</td>
      <td>0</td>
      <td>SY</td>
      <td>1522540156</td>
      <td>60</td>
      <td>34.45</td>
      <td>40.92</td>
      <td>46.48</td>
      <td>2.98</td>
    </tr>
    <tr>
      <th>489</th>
      <td>panzhihua</td>
      <td>0</td>
      <td>CN</td>
      <td>1522540148</td>
      <td>59</td>
      <td>26.59</td>
      <td>101.72</td>
      <td>46.61</td>
      <td>1.86</td>
    </tr>
    <tr>
      <th>490</th>
      <td>saeby</td>
      <td>56</td>
      <td>DK</td>
      <td>1522540157</td>
      <td>98</td>
      <td>57.33</td>
      <td>10.52</td>
      <td>35.41</td>
      <td>14.56</td>
    </tr>
    <tr>
      <th>491</th>
      <td>oussouye</td>
      <td>0</td>
      <td>SN</td>
      <td>1522537200</td>
      <td>57</td>
      <td>12.49</td>
      <td>-16.54</td>
      <td>78.8</td>
      <td>2.24</td>
    </tr>
    <tr>
      <th>492</th>
      <td>mattawa</td>
      <td>90</td>
      <td>CA</td>
      <td>1522537200</td>
      <td>98</td>
      <td>46.32</td>
      <td>-78.7</td>
      <td>32</td>
      <td>12.75</td>
    </tr>
    <tr>
      <th>493</th>
      <td>grand gaube</td>
      <td>75</td>
      <td>MU</td>
      <td>1522537200</td>
      <td>88</td>
      <td>-20.01</td>
      <td>57.66</td>
      <td>80.6</td>
      <td>10.29</td>
    </tr>
    <tr>
      <th>494</th>
      <td>police</td>
      <td>90</td>
      <td>PL</td>
      <td>1522539000</td>
      <td>93</td>
      <td>53.55</td>
      <td>14.57</td>
      <td>37.4</td>
      <td>5.82</td>
    </tr>
    <tr>
      <th>495</th>
      <td>praya</td>
      <td>20</td>
      <td>ID</td>
      <td>1522539000</td>
      <td>88</td>
      <td>-8.71</td>
      <td>116.27</td>
      <td>78.8</td>
      <td>1.12</td>
    </tr>
    <tr>
      <th>496</th>
      <td>husum</td>
      <td>80</td>
      <td>DE</td>
      <td>1522538400</td>
      <td>98</td>
      <td>54.49</td>
      <td>9.05</td>
      <td>33.8</td>
      <td>11.41</td>
    </tr>
    <tr>
      <th>497</th>
      <td>porto velho</td>
      <td>24</td>
      <td>BR</td>
      <td>1522539975</td>
      <td>84</td>
      <td>-8.75</td>
      <td>-63.87</td>
      <td>79.64</td>
      <td>2.59</td>
    </tr>
    <tr>
      <th>498</th>
      <td>khilok</td>
      <td>36</td>
      <td>RU</td>
      <td>1522540160</td>
      <td>58</td>
      <td>51.36</td>
      <td>110.46</td>
      <td>27.04</td>
      <td>12.77</td>
    </tr>
    <tr>
      <th>499</th>
      <td>nishihara</td>
      <td>1</td>
      <td>JP</td>
      <td>1522537200</td>
      <td>62</td>
      <td>35.74</td>
      <td>139.53</td>
      <td>57.2</td>
      <td>3.98</td>
    </tr>
  </tbody>
</table>
<p>500 rows × 9 columns</p>
</div>




```python
#Plot City Latitude vs. Max Temperature 
plt.scatter(city_data["Lat"], city_data["Max Temp"], marker="o", facecolors="blue", edgecolors="black", alpha=0.75)
plt.title("City Latitude vs. Max Temperature (03/31/17)")
plt.xlabel("Latitude")
plt.ylabel("Max Temperature (F)")
plt.savefig("City Lat vs Max Temp.png")
plt.show()
```


![png](output_7_0.png)



```python
#Plot City Latitude vs. Humidity 
plt.scatter(city_data["Lat"], city_data["Humidity"], marker="o", facecolors="blue", edgecolors="black", alpha=0.75)
plt.title("City Latitude vs. Humidity (03/31/17)")
plt.xlabel("Latitude")
plt.ylabel("Humitidy (%)")
plt.savefig("City Lat vs Humidity.png")
plt.show()
```


![png](output_8_0.png)



```python
#Plot City Latitude vs. Cloudiness 
plt.scatter(city_data["Lat"], city_data["Cloudiness"], marker="o", facecolors="blue", edgecolors="black", alpha=0.75)
plt.title("City Latitude vs. Cloudiness (03/31/17)")
plt.xlabel("Latitude")
plt.ylabel("Cloudiness (%)")
plt.savefig("City Lat vs Humidity.png")
plt.show()
```


![png](output_9_0.png)



```python
#Plot City Latitude vs. Wind Speed
plt.scatter(city_data["Lat"], city_data["Wind Speed"], marker="o", facecolors="blue", edgecolors="black", alpha=0.75)
plt.title("City Latitude vs. Wind Speed (03/31/17)")
plt.xlabel("Latitude")
plt.ylabel("Wind Speed (mph)")
plt.savefig("City Lat vs Humidity.png")
plt.show()
```


![png](output_10_0.png)

