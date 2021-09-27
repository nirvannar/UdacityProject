# UdacityProject
My first Udacity Project based on CRISP-DM
# Table of Contents

* [Installation](#Installation)
* [Project Motivation](#Project-Motivation)
* [File Descriptions](#File-Descriptions)
* [Results](#Results)
* [Licensing, Authors, and Acknowledgements](#Licensing,-Authors,-and-Acknowledgements)


## Installation <a name="Installation"></a>
The code should run with no issues using Python versions 3.8.8 using Jupyter Notebook server version 6.3.0.  Numpy, Pandas, matplotlib.pyplot, math, seaborn, wordcount, Datapane and Folium libraries were used.  A datapane account must be created and then the API token created and viewed at https://datapane.com/settings/  

Datapane must then be installed as below

```python
pip install -U datapane
```

## Project Motivation <a name="Project-Motivation"></a>
For this project, I was interestested in using the characteristcs of Holocene volcanoes for the purpose of Volcano tourism.  A combination of these characteristics and the tourists location and base and appetite for distance travel will allow the traveller to use a combination of analyses to pick the locations for leisure travel purposes.  

**_The following questions were required to be answered from the data._**
 
*Which is the highest Volcano in the world?  
Which country has the most volcanoes?  
Which region has the most volcanoes? 
What is the most common volcano type?  
Which year had the most eruptions  2021 July YTD, and which were they?  
Which is the closest volcano to OR Tambo Airport in Johannesburg, South Africa?  
Which are the active volcanoes within 3000km radius of OR Tambo Airport in Johannesburg, South Africa?  
How can we see the spread of volcanoes globally?*



## File Descriptions and Analyses <a name="File-Descriptions-and-Analyses"></a>
The notebook is exploratory in searching through the data pertaining to the questions showcased by the notebook title. Markdown cells were used to assist in walking through the thought process for individual steps.
I was interestested in using Smithsonian Institution data from the Global Volcanism Program entitled Volcanoes of the World 4.10.1, downloaded on 24 Jul 2021 at 11:16 AM	as a .csv file to use characteristcs of Holocene volcanoes for the purpose of Volcano tourism. 

The .csv file was analysed using a Jupyter Notebook.  It had 1398 rows of data and 4 columns of quantitative variables.  The total columns were 14 namely Volcano Number,	Volcano Name,	Country,	Primary Volcano Type,	Activity Evidence,	Last Known Eruption,	Region,	Subregion,	Latitude,	Longitude, 	Elevation (m),	Dominant Rock Type and	Tectonic Setting.   The columns of data "Dominant Rock Type" and "Tectonic Setting" contained blanks.  However these 2 columns were not used to obtain results and are excluded from any analysis.  

Pandas DataFrame.hist was used to see the distribution / shape of the data for the quantitative variables.  The only variables were volcano number, latitude, longitude and Elevation (m) that were analysed.  Elevation (m) was normally distributed while latitude had 2 peaks and the longitude and volcano numbers were spread out.

Seaborn pairplot and heatmap were used to check for any correlations between variables.  No strong correlations existed.  Thus no machine mearning models were considered in the analyses.  

There is one notebook available here to showcase work related to the above questions. 

*Which is the highest Volcano in the world?  Ojos del Salado, Nevados in Chile, South America using df['Elevation (m)'].max()  
Which country has the most volcanoes? USA using df['Country'].value_counts(normalise=True) to find percentages in descending order    
Which region has the most volcanoes? South America using df['Country'].value_counts(normalise=True) to find percentages in descending order    
What is the most common volcano type? Stratovolcano using df['Primary Volcano Type'].value_counts(normalise=True) to find percentages in descending order  
Which year had the most eruptions until 2021 July YTD, and which were they?  2021 with 57 July YTD  
Which is the closest volcano to OR Tambo Airport in Johannesburg, South Africa?  Kyejo  Tanzania  using Haversine Formula to calculate distance, appending a column called "distance" and using df['distance'].min()*

```python
# Closest Volcano to Johannesburg

from math import radians, cos, sin, asin, sqrt
def dist(Longitude1,Latitude1,Longitude2,Latitude2 ):
   
    # convert decimal degrees to radians 
    Longitude1,Latitude1, Longitude2,Latitude2  = map(radians, [Longitude1, Latitude1,Longitude2,Latitude2])
    # haversine formula 
    dlon = Longitude2 - Longitude1  
    dlat = Latitude2 - Latitude1 
    a = sin(dlat/2)**2 + cos(Latitude1) * cos(Latitude2) * sin(dlon/2)**2
    c = 2 * asin(sqrt(a)) 
    # Radius of earth in kilometers is 6371
    km = 6371* c
    return km

df['distance'] = [dist(df.Longitude[i],df.Latitude[i], 28.2411459,-26.1366728) 
                  for i in range(len(df))]
df['distance'] = df['distance'].round(decimals=3)

df.head(296)

print(df[df['distance']==df['distance'].min()])
```  

*Which are the active volcanoes within 3000km radius of OR Tambo Airport in Johannesburg, South Africa? A combination of characteristics were used to find Piton de la Fournaise,Lengai, Ol Doinyo, 	Nyamulagira and Nyiragongo from furtherest to closest.*
```python
df.loc[(df['Last Known Eruption'] == "2021 CE") & (df['distance'] <3000)] #Active volcanoes within 3000km radius of Jhb
```

*How can we see the spread of volcanoes globally? - answered via using Folium and datapane to add markers to the world map as below*
```python
# add marker one by one on the map
import pandas as pd
import folium

import datapane as dp

dp.login(token='627d7678b242daf7ecba23b579eab5e6754290b8')

df = pd.read_csv("C:/Users/nrampersad/Downloads/Downloads AAHP/2021/Udacity/GVP_Volcano_List_Holocene1.csv")
m = folium.Map(location=[-26.1366728, 28.2411459], tiles="OpenStreetMap", zoom_start=3)


#for i in range(0,len(data)):
for index, row in df.iterrows():
    icon_path = r"C:/Users/nrampersad/Downloads/noun_Volcano_1708.png"
    icon = folium.features.CustomIcon(icon_image=icon_path ,icon_size=(20,20))
    folium.Marker(
              #location=[data.iloc[i]['lat'], data.iloc[i]['lon']],
              #popup=data.iloc[i]['name'],
              [row['Latitude'], row['Longitude']], 
                  popup=row['Volcano Name'],
              icon=icon
              ).add_to(m)

# Show the map again
dp.Report(dp.Plot(m)).upload(name='folium_map')
m
```
## Results <a name="Results"></a>

[A Medium blog](https://medium.com/@nirvannsramp/intrepid-explosive-voyages-77f23e47e24e?source=friends_link&sk=b97c94187c9f435b0b955aa12acc408d) was created using the results. 

## Licensing, Authors, and Acknowledgements<a name="Licensing,-Authors,-and-Acknowledgements"></a>
The data was downloaded from the Smithsonian Institution Global Volcanism Program. Stack Overflow, Kaggle, Medium and Github were consulted for syntax references.  
The Volcano marker used in the Folium map was created by Joris Hoogendoorn from the Noun Project
