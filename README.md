<h1>Equator Weather Vacation</h1>

<p>In this project I wanted to explore the relationship of distance from the equator to the weather in order to find our ideal vacation spot using python, OpenWeatherAPI and Google Maps API. I use NumPy to generate random coordinates and CityPy to find the nearest city. I then used the OpenWeather API to pull the weather report for that day 1-18-21. I graphed and calculated the correlation of the different weather conditions and the latitude. In order to find the ideal vacation spot, I filtered by the optimal weather conditions and used Google Maps API to find the nearest hotel. 
  
 Equator Weather Vacation also functions as an example as to how one might go about finding their next international rental property investment or find the ideal location for a solar/wind energy farm. For a vacation property one could use this method and cross reference the CAP rate to match the best financial investment. One could find cities with the best solar/energy farm climate for optimized energy generation. They could then cross reference the cost of land to find an initial list of potential investment areas. Obviously, there are many more nuances in finanial investments but this coulsd provide an intial list of possibilities. My study is only the weather report for one day but OpenWeather API has historical weather data as well. 
 
  The project had two parts: 
 1) Equator and Weather: Generated a random sample of cities and a study of the relationship between their weather vs their latitude.
 2) Vacation: We overlay a heatmap for visual representation of humidity using google maps API. Generate a list of cities that fit the input of ideal conditions and find the nearest hotel. 
  I used four main metrics: Temperature(max), Humidity (%), Cloudiness(%), and Wind Speed(mph)</p>

<h2>Equator and Weather</h2>

<h3>Dataset</h3>
<p>I used numpy to assign random latitude and longitude points. I then used citipy to find the nearest city to the randomly generated coordinates. I then quieried the OpenWeather API to give us the current weather metrics for 1-18-21 and added them to the dataframe. Since I was finding the nearest "city" to the random coordinates I had state that there are less cities in and around the South Pole and Southern waters. This does skew my dataset to not account for much south of -60 latitude.</p>

<h3>Exploring the Relationships</h3>
<p>First, I plotted Temperature, whose max temperatures were around or a little below the equator. This is what we would expect considering the analysis was ran in the middle of december when the sun shines the most directly on this part of the earth. 

Second was humidity. between -40 to 40 latitude there seems to be a spread from 20 to 100 percent humidity, with most of the spread being above 50%. Above 40 latitude the humidity stays above 50. This is surprising.

Third is cloudiness. There was a very even spread across the latitudes.

Fourth was the Wind Speed. This was also a pretty even distribution.

After our initial analysis we decided there might be different relationships for our weather metrics depending on which hemisphere they were. 

North Temperature v Latitude: As we increase the latitude the temperature went down. The have a negative correlation of -0.84.

South Temperature v Latitude: As we get increase in latitude the temperature goes up. However there is less correlation here: 0.53. The difference in correlation most likely has to do with the way the Earth faces the sun. The south receives more direct light and is at less of an angle to the sun. WHere the north is angled and asunlight is less and less direct as you go further north.

North and South Humidity v Latitude: North has a weaker correlation at 0.42 while the south is 0.53. Both seemto increase in humidity as they increase in latitude.

North and South Cloudiness v Latitude: There is very little correlation bewtween these metrics and the latitude. North is 0.15 and South is 0.23.

North and South Wind Speed v Latitude: There is no correlation in the North with wind speed and latitude. The south has very little correlation at -0.20>


<h2>VACATIONPY</h2>
<p>We wanted to use our dataset to create a visual representation of humidity using google's Places API. We created a heat_layer and added it to google maps figure.

We then thought we could find ideal vacation spots for ourselves by narrowing down the weather data to our preferred weather. We created an ideal dataframe with temperature less than 100 and more than 75, wind speed at less than 10 mph, cloudiness less than 5%. We left humidity open because we enjoy all humidities. Then we wanted tot find a hotel close to our narrowed locations. We quieried Google's nearby searches to find a list of the nearest hotels. We took the first one and add the hotel name and coordinates to the df. Then, we used citipy to grab the city name and country of the hotel to put it into the dataframe. We then placed them along with our heatmap on the google map.</p>
