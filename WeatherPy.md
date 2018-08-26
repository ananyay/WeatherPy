

```python
# Dependencies and Setup
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import requests
import time

# Import API key
import api_keys

# Incorporated citipy to determine city based on latitude and longitude
from citipy import citipy

# Output File (CSV)
output_data_file = "../output_data/cities.csv"

# Range of latitudes and longitudes
lat_range = (-90, 90)
lng_range = (-180, 180)
```

## Generate Cities List


```python
# List for holding lat_lngs and cities
lat_lngs = []
cities = []

# Create a set of random lat and lng combinations
lats = np.random.uniform(low=-90.000, high=90.000, size=1500)
lngs = np.random.uniform(low=-180.000, high=180.000, size=1500)
lat_lngs = zip(lats, lngs)

# Identify nearest city for each lat, lng combination
for lat_lng in lat_lngs:
    city = citipy.nearest_city(lat_lng[0], lat_lng[1]).city_name
    
    # If the city is unique, then add it to a our cities list
    if city not in cities:
        cities.append(city)

# Print the city count to confirm sufficient count
len(cities)
```




    638



## Perform API Calls


```python
# OpenWeatherMap API Key
api_key = api_keys.api_key

# Starting URL for Weather Map API Call
url = "http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=" + api_key 
city_data = []

# Print to logger
print("Beginning Data Retrieval     ")
print("-----------------------------")

for city in cities:
    city_url = url + "&q=" + city
    print(city_url)
    try:
        city_weather = requests.get(city_url).json()
        city_lat = city_weather['coord']['lat']
        city_mtemp = city_weather['main']['temp_max']
        city_humidity = city_weather['main']['humidity']
        city_cloudiness = city_weather['clouds']['all']
        city_wspeed = city_weather['wind']['speed']
        city_data.append({"city":city,
                      "Latitude":city_lat,
                      "Max Temp":city_mtemp,
                      "Humidity":city_humidity,
                      "Cloudiness":city_cloudiness,
                      "Wind Speed":city_wspeed,
                      })
    except:
        print("city not found")
        pass

# Indicate that Data Loading is complete 
print("Data Retrieval Complete  ")

    
    
    




```

    Beginning Data Retrieval     
    -----------------------------
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=alofi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=belushya guba
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ushuaia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=akyab
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=hobart
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=saint-philippe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=carnarvon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=izhma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bubaque
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=lebu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=souillac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=atuona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=rikitea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=barcelos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=busselton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=chuy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=poshekhonye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ripiceni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=albany
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=talnakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=vaini
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bonavista
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bundaberg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=nikolskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bonito
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kontagora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=san patricio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=vostok
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tiznit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=chokurdakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=dhidhdhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=puerto gaitan
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=praia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=provideniya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=cherskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=cape town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=barrow
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=cidreira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yantzaza
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=saint george
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=umm kaddadah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=flin flon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mys shmidta
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=klaksvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mataura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=petropavlovsk-kamchatskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=banjar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=neiafu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=punta arenas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=illoqqortoormiut
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=qaanaaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=westport
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=berlevag
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=aklavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bluff
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=walvis bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=komsomolskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sioux lookout
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=prado
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=amderma
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=hithadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=georgetown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=upernavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mar del plata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=urumqi
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=olafsvik
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=vanimo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sheremetyevskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yar-sale
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=daru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=terney
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=jamestown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tsihombe
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=faanui
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=hamilton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=nara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=atambua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=hermanus
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=eenhana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yellowknife
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=new norfolk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=lorengau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=castro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=novosergiyevka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kaka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ye
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=nador
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=copacabana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=asau
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=batangafo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=guiratinga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=korla
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=gazli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=butaritari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=celestun
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tasiilaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mastic beach
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ayorou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=hervey bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=dikson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=hirado
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=leninsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=honiara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=east london
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=troy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=geraldton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=poum
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ajdabiya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=luderitz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=white rock
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bredasdorp
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=college
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=attawapiskat
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=barentsburg
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=udachnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=posse
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=dawson creek
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kimbe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=avarua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=lagoa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=saldanha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=cabo san lucas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=zaraza
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kirksville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tautira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=rapid valley
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=svetlyy
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=belmonte
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sirjan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=santa maria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=okha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=beringovskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=luganville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=monte azul
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sao joao da barra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=taolanaro
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=itanhem
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=coahuayana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=la ronge
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sumbe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=husavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kavieng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=moundsville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=umm lajj
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=port alfred
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=rafraf
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=dingle
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kargasok
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=pevek
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=erenhot
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kodiak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=longyearbyen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=xining
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=puerto ayora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=alugan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=shimoda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=samusu
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=brazzaville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=khandagayty
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=havoysund
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=verkhnevilyuysk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=zhigansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ilulissat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ancud
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tongchuan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=qui nhon
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=krasnoselkup
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=falam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=fevralsk
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yerbogachen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=puerto colombia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tiksi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sakakah
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=natchitoches
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=saleaula
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=marawi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=pueblo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=vardo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=esperance
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=paamiut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ribeira grande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=grand river south east
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=verkhoyansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=alotau
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=alice springs
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=victoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=hasaki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=lusambo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=abu samrah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tuatapere
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=vaitape
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kavaratti
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=iskateley
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=benemerito de las americas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=angoche
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=te anau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=emerald
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=pinawa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kahului
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=airai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=darnah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=codrington
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=meulaboh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mahebourg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=basco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=hilo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=khatanga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=jacareacanga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=palmer
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=lompoc
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=agirish
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=myrtle beach
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=necochea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=phan rang
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kaitangata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=thompson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=vagos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=igrim
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sibu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=omsukchan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=hami
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=atherton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ponta do sol
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=pucallpa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=chapleau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=neunkirchen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=qeshm
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=thinadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=serebryansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tezu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=orange
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mullaitivu
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=port elizabeth
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=burlatskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=espanola
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=portland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tubruq
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kapaa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=iqaluit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=riyadh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=omaruru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=troitsko-pechorsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=lebyazhye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=marihatag
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mogadishu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=quelimane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bethel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=isugod
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=katsuura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=fortuna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=camacupa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kildinstroy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sao borja
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bulgan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=hays
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=roald
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=chirongui
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tucurui
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=porto belo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sola
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=lobva
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sorkjosen
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=flinders
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=king city
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kamsack
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=isangel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=saint-pierre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=buala
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kawalu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=constitucion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=hambantota
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=itaperucu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=broome
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=miedzyrzec podlaski
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=aksarka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=wasilla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=nizhneyansk
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=severo-kurilsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sentyabrskiy
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=egvekinot
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=camapua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=waingapu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mezen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=rocha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tual
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=skelleftea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=la rioja
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=nome
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=quatre cocos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=matagami
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=malakal
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=beira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=camacari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=la plata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mahabaleshwar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=chapais
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=palabuhanratu
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tarudant
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=maiduguri
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mananara
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yagodnoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ossora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=chumikan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=cockburn town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=hualmay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=okhotsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=trinidad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=nemuro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=farah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=cheuskiny
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=iquitos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bengkulu
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=port hedland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=acajutla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=pisco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=firminy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yelizovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=brekstad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bacolod
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=serafimovich
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yanam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=teya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yuli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=antofagasta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sorland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=srednekolymsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=inirida
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ucluelet
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=porto santo
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mareeba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=port blair
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sabang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ostrovnoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=atlantic beach
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ziniare
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=quincy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=cao bang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=rongcheng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=paita
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=enshi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=xuddur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=uwayl
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=buraydah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bialystok
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=taytayan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=port hardy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tilichiki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bandarbeyla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=aniche
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=vilhena
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=banda aceh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bose
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=great bend
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=jiwani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=moron
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=quesnel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yeppoon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mackay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=edwardsville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ust-maya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bang saphan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=rudnichnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=wadsworth
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ternate
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=poso
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=aginskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=general pico
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=vung tau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=presidencia roque saenz pena
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=nguruka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=aitape
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=aktau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mount gambier
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=stara synyava
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=atasu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=amursk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=pathein
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=norman wells
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tumannyy
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=oranjestad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=maragogi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=vagur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=westpunt
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=zdvinsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=cayenne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=purpe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=strezhevoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=thunder bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=atar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mamallapuram
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kupang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=dole
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=puerto carreno
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kathmandu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=saskylakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yenagoa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=puerto leguizamo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=morgan city
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=chongqing
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=namibe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=saint pete beach
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=west wendover
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kamenskoye
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bur gabo
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=haines junction
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=lyubytino
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=pishin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=marcona
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=amahai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tabialan
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=hihifo
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ekibastuz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kirakira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ipaussu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ixtapa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=beloha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tawau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=pipri
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=san cristobal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kachikau
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=colwyn bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=camopi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=dongkan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bagdarin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sembakung
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bambanglipuro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=puerto escondido
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=taltal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=launceston
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=svetlogorsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=teeli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=guerrero negro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=nazilli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sidvokodvo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=vaitupu
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kazalinsk
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=brahmapuri
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=proletarskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=azul
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=lima
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=senneterre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ughelli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bolobo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=blairmore
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=novita
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sovetskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=atchison
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=biak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yambio
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kunming
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=port antonio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=coquimbo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=matay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=batemans bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=shingu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=port-gentil
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=san quintin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=oussouye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=golden
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=knoxville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=rawson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=waldshut-tiengen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=curaca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=wulanhaote
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yarada
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mizur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=pangoa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=garowe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=cheremukhovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tir pol
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bandar penggaram
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=acapulco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mbanza-ngungu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=lakatoro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sulangan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=fort nelson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=lavrentiya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=shatsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=narsaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=cabedelo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=aswan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sakaiminato
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=karratha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ulladulla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=road town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=vila velha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=asosa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=gwanda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=laguna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=toliary
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=morro bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=plettenberg bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mgachi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kalas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sataua
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=auki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tabiauea
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=clyde river
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=galle
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=linqiong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=camacha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=uvalde
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=padang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=oksfjord
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=fernley
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=saint-francois
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=vestmanna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=salym
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=zhizdra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yomitan
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=adrar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ouallam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=goderich
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yaan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=vao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sechura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=gotsu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=agadir
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ahipara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=temaraia
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=stokmarknes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tepalcatepec
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yertsevo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=avera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=nokaneng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bilibino
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mehamn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=zalantun
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=leshukonskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=dutse
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=pemangkat
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mattawa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=san carlos de bariloche
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=windsor
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tieling
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=manyana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=dubbo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=klyuchi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kemin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kokorevka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sehithwa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yamada
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=stolin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kouroussa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=estevan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=turan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=phangnga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=quepos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=pithiviers
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=san andres
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=torbay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=sao filipe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=cagayan de tawi-tawi
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=cervo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kamphaeng phet
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=qasigiannguit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tiruttani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=zamora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=langham
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=shagonar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=burica
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=henties bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=axim
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=chimoio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=samarai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=aban
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=manokwari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=pangody
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kodinsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=loandjili
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=praia da vitoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=pangnirtung
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=jinchang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=huarmey
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=jardim
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=jabiru
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=amapa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=saint-louis
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=wonthaggi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=cavalcante
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=novodolinskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=resistencia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=dunedin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=falealupo
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=talcahuano
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=zavyalovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=birjand
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=zhitikara
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=longlac
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=acarau
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bay roberts
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=haikou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=pundaguitan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bartica
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=liverpool
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yelets
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=koutsouras
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tigil
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=itarema
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=moindou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yefimovskiy
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=springdale
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=barra patuca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=oskarshamn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=dori
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=belen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=santa fe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=prince rupert
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=ketchikan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=fare
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tooele
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=virginia beach
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=popondetta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=waipawa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tipacoque
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=dandong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=freeport
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=utkivka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=utiroa
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=tazmalt
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=selikhino
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=nadym
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=chakia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bathsheba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=aracati
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=jining
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=koshurnikovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=caxito
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=yumen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=wanlaweyn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=bambous virieux
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=naolinco
    city not found
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=praya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=mitu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=cyangugu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=8e7985f09aa3bf830ab2d84bfc3dd5dc&q=kisangani
    Data Retrieval Complete  
    


```python
#creating a dataframe
city_df = pd.DataFrame(city_data)

# re arranging the columns in data frame 
city_df = city_df [["city","Cloudiness","Humidity","Latitude","Max Temp","Wind Speed"]]
city_df.head()


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
      <th>city</th>
      <th>Cloudiness</th>
      <th>Humidity</th>
      <th>Latitude</th>
      <th>Max Temp</th>
      <th>Wind Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>alofi</td>
      <td>76</td>
      <td>94</td>
      <td>-19.06</td>
      <td>73.40</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ushuaia</td>
      <td>75</td>
      <td>80</td>
      <td>-54.81</td>
      <td>39.20</td>
      <td>4.70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>hobart</td>
      <td>75</td>
      <td>61</td>
      <td>-42.88</td>
      <td>48.20</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>3</th>
      <td>saint-philippe</td>
      <td>90</td>
      <td>47</td>
      <td>45.36</td>
      <td>82.40</td>
      <td>5.82</td>
    </tr>
    <tr>
      <th>4</th>
      <td>carnarvon</td>
      <td>0</td>
      <td>79</td>
      <td>-30.97</td>
      <td>36.92</td>
      <td>13.69</td>
    </tr>
  </tbody>
</table>
</div>




```python
## Latitude Vs Max Temperature plot
#plt.scatter(city_df['Latitude'],city_df['Max Temp'],)
city_df.plot(x = 'Latitude',y = 'Max Temp',kind ='scatter',title="Latitude Vs Max Temperature",grid = True)

# save the figure 
plt.savefig("output_plots/Max_Temp_vs_Latitude.png")

# Display the plot 
plt.show()
```


![png](output_6_0.png)



```python
## latitude vs Humidity
city_df.plot(x='Latitude',y='Humidity',kind = 'scatter',title ="Latitude vs Humidity",grid = True)
# save the figure 
plt.savefig("output_plots/Humidity_vs_Latitude.png")
# Display the plot 
plt.show()
```


![png](output_7_0.png)



```python
# Cloudiness (%) vs. Latitude
city_df.plot(x='Latitude',y='Cloudiness',kind = 'scatter',title ="Cloudiness (%) vs. Latitude",grid = True)

# save the figure 
plt.savefig("output_plots/Cloudiness_vs_Latitude.png")

# Display the plot 
plt.show()
```


![png](output_8_0.png)



```python
# Wind Speed (mph) vs. Latitude
city_df.plot(x='Latitude',y='Wind Speed',kind = 'scatter',title ="Wind Speed (mph) vs. Latitude",grid = True) 

# Save the figure
plt.savefig("output_plots/Wind_Speed_vs_Latitude.png")

# Show plot
plt.show()
```


![png](output_9_0.png)



```python
# save the Dataframe to csv file 
city_df.to_csv(output_data_file,index_label ="city_id")
```
