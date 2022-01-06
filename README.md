# World_Weather_Analysis
These project has 3 parts:

	 - Retrieve Weather Data 
	 - Create a Customer Travel Destinations Map
	 - Create a Travel Itinerary Map

	 
### Retrieve Weather Data
In this part, we find 2,000 random latitudes and longitudes with the below code;

	 lats = np.random.uniform(low=-90.000, high=90.000, size=2000) 
	 lngs =  np.random.uniform(low=-180.000, high=180.000, size=2000)

Then we use citipy module and nearest_city function to find nearest city of each Lat & Lng;

         city = citipy.nearest_city(coordinate[0], coordinate[1]).city_name

After that API was used  to retrieve the  weather description for each city and then  one  DataFrame and one CSV file are created from weather data of cities. They include the below information:

	 city, Country, Lat, Lng, Max Temp, Humidity, Cloudiness, Wind Speed & Current Description.

### Customer Travel Destinations Map 
The final CSV file of previous part is input data 
First step, we ask customer to chose minimum and maximum temperature criteria

	 - min_temp = float(input("What is the minimum temperature you would like for your trip? ")) 
	 - max_temp = float(input("What is the maximum temperature you would like for your trip? "))

Based on the above data; new DataFrame is created, .loc module is used. 

	 - preferred_cities_df = city_data_df.loc[(city_data_df["Max Temp"] <= max_temp) & (city_data_df["Max Temp"] >= min_temp)]
	 
Then we retrieve hotels for each city with 5000 meters, below parameters is set;

	 - radius: 5000, (for each city with 5000 meters)
	 - type: "lodging
	 - key": g_key (google API)}

The above parameters and Google Directions API is used to find the hotels.

	 - hotels = requests.get(base_URL, params=params).json()

A template box information is created to includes hotel name, city, country, current weather & maximum temperature. Finally, the map is prepared with marker layers.

###  Travel Itinerary Map
The final CSV file of previous part is input data.
Four cities are chosen as from the map and create a vacation itinerary route to travel between them. Then we use to_numpy function to create tuple of  latitude-longitude of each city. The route includes start, stop1, stop2, stop3, end. Note that the start city and the end city are the same.

	 - start = vacation_start["Lat"].to_numpy( [0],vacation_start["Lng"].to_numpy()[0]
	 - end = vacation_end["Lat"].to_numpy()[0],vacation_end["Lng"].to_numpy()[0]
	 - stop1 = vacation_stop1["Lat"].to_numpy()[0],vacation_stop1["Lng"].to_numpy()[0]
	 - stop2 = vacation_stop2["Lat"].to_numpy()[0],vacation_stop2["Lng"].to_numpy()[0]
	 - stop3 = vacation_stop3["Lat"].to_numpy()[0],vacation_stop3["Lng"].to_numpy()[0]
 
 thus, the direction layer is added to the map with the below code;
 
	 city_itinerary = gmaps.directions_layer(start, end, waypoints=[stop1,stop2,stop3], travel_mode="DRIVING")

One DataFrame is created from he four city DataFrames with .concat( ) function.

	 - itinerary_df = pd.concat([vacation_start, vacation_stop1, vacation_stop2, vacation_stop3],ignore_index=True)
	 
A template box information is created to includes hotel name, city, country, current weather & maximum temperature. Finally, the map is prepared with marker layers.
 
