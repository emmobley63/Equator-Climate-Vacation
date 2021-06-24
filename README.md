<h1>Equator Weather Vacation</h1>

<p>In this project I wanted to explore the relationship of distance from the equator to the weather in order to find our ideal vacation spot using python, OpenWeatherAPI and Google Maps API. I use NumPy to generate random coordinates and CityPy to find the nearest city. I then used the OpenWeather API to pull the weather report for that day 1-18-21. I graphed and calculated the correlation of the different weather conditions and the latitude. In order to find the ideal vacation spot, I filtered by the optimal weather conditions and used Google Maps API to find the nearest hotel. 
  
 Equator Weather Vacation also functions as an example as to how one might go about finding their next international rental property investment or find the ideal location for a solar/wind energy farm. For a vacation property one could use this method and cross reference the CAP rate to match the best financial investment. One could find cities with the best solar/energy farm climate for optimized energy generation. They could then cross reference the cost of land to find an initial list of potential investment areas. Obviously, there are many more nuances in financial investments but this could provide an intial list of possibilities. My study is only the weather report for a single day but OpenWeather API has historical weather data that could be used to find the recent weather trends.
 
  The project had two parts: 
 1) Equator and Weather: Generated a random sample of cities and a study of the relationship between their weather vs their latitude.
 2) Vacation: We overlay a heatmap for visual representation of humidity using google maps API. Generate a list of cities that fit the input of ideal conditions and find the nearest hotel. 
  I used four main metrics: Temperature(max), Humidity (%), Cloudiness(%), and Wind Speed(mph)</p>
<br>

<h2>Equator and Weather</h2>

<h3>Dataset</h3>
<p>I used numpy to assign random latitude and longitude points. I then used citipy to find the nearest city to the randomly generated coordinates. I then quieried the OpenWeather API to give us the current weather metrics for 1-18-21 and added them to the dataframe. Since I was finding the nearest "city" to the random coordinates I had state that there are less cities in and around the South Pole and Southern waters. This does skew my dataset to not account for much south of -60 latitude.</p>
<br>

<h3>Exploring the Relationships</h3>
<table>
  <tr>
    <td>
      <p>First, I plotted Temperature, whose max temperatures were around or a little below the equator. This is what we would expect considering the analysis was ran in the middle of december when the sun shines the most directly on this part of the earth.
      <p>
    </td>
    <td colspan="2">
      <img src="https://github.com/emmobley63/Equator-Weather-Vacation/blob/main/Images/Temperature_Latitude_1-18-21.png">
    </td>
  </tr>

  <tr>
    <td>Second was humidity. between -40 to 40 latitude there seemed to be a spread from 20 to 100 percent humidity, with most of the spread being above 50%. Above 40 latitude the humidity stayed above 50. This was surprising.
    </td>
    <td colspan="2">
      <img src="https://github.com/emmobley63/Equator-Weather-Vacation/blob/main/Images/Humidity_Latitude_1-18-21.png">
    </td>

   <tr>
     <td>Third was cloudiness. There was a very even spread across the latitudes.
     </td>
     <td colspan="2">
       <img src="https://github.com/emmobley63/Equator-Weather-Vacation/blob/main/Images/Cloudiness_Latitude_1-18-21.png">
     </td>
  </tr>

  <tr>
    <td>Fourth was Wind Speed. This was also a pretty even distribution.
    </td>
    <td colspan="2">
      <img src="https://github.com/emmobley63/Equator-Weather-Vacation/blob/main/Images/WindSpeed_Latitude_1-18-21.png">
    </td>
  </tr>

  <tr>
    <td colspan="3">After my initial analysis I decided there might be different relationships for our weather metrics depending on which hemisphere they were. Northern hemisphere graphs are pictured in red and the southern in green.</td>
  </tr>

  <tr>
    <td>North Temperature v Latitude: As I increased the latitude, the temperature went down. They had a negative correlation of -0.84. South Temperature v Latitude: Increases in the latitude caused the temperature to go up. However there was less correlation here: 0.53. The difference in correlation most likely had to do with the tilt and rotation of the Earth during this time of year. At 23.5 degrees off its orbital plane, the Earth receives the Sun's rays differently depending on the time of the year and the hemisphere. During the time of the weather sample, the south receives more direct light and was at less of an angle to the sun. Where the north was angled and sunlight was less and less direct as you go further north.
    </td>
    <td>
      <img src="https://github.com/emmobley63/Equator-Weather-Vacation/blob/main/Images/Nothern_Hemisphere_Temperature_Latitude_1-18-21.png">
    </td>
    <td>
      <img src="https://github.com/emmobley63/Equator-Weather-Vacation/blob/main/Images/Southern_Hemisphere_Temperature_Latitude_1-18-21.png">
    </td>
  </tr>

  <tr>
    <td>North and South Humidity v Latitude: North has a weaker correlation at 0.42 while the south is 0.53. Both seem to increase in humidity as they increase in latitude.
    </td>
    <td>
      <img src="https://github.com/emmobley63/Equator-Weather-Vacation/blob/main/Images/Nothern_Hemisphere_Humidity_Latitude_1-18-21.png">
    </td>
    <td>
      <img src="https://github.com/emmobley63/Equator-Weather-Vacation/blob/main/Images/Southern_Hemisphere_Humidity_Latitude_1-18-21.png">
    </td>
  </tr>

  <tr>
    <td>North and South Cloudiness v Latitude: There is very little correlation bewtween these metrics and the latitude. North is 0.15 and South is 0.23.
    </td>
    <td>
      <img src="https://github.com/emmobley63/Equator-Weather-Vacation/blob/main/Images/Nothern_Hemisphere_Cloudiness_Latitude_1-18-21.png">
    </td>
    <td>
      <img src="https://github.com/emmobley63/Equator-Weather-Vacation/blob/main/Images/Southern_Hemisphere_Cloudiness_Latitude_1-18-21.png">
    </td>
  </tr>

  <tr>
    <td>North and South Wind Speed v Latitude: There is no correlation in the North with wind speed and latitude. The south has very little correlation at -0.20
    </td>
    <td>
      <img src="https://github.com/emmobley63/Equator-Weather-Vacation/blob/main/Images/Nothern_Hemisphere_WindSpeed_Latitude_1-18-21.png">
    </td>
    <td>
      <img src="https://github.com/emmobley63/Equator-Weather-Vacation/blob/main/Images/Southern_Hemisphere_WindSpeed_Latitude_1-18-21.png">
    </td>
  </tr>
</table>
<br>

 
<h2>Vacation</h2>
<p>I wanted to use our dataset to create a visual representation of humidity using Google's Places API. I created a heat_layer and added it to Google maps figure.

I then thought I could find ideal vacation spots by narrowing down the weather data to my preferred weather. I created an ideal dataframe with temperature less than 100 and more than 75, wind speed at less than 10 mph, cloudiness less than 5%. I left humidity open because we enjoy all humidities. Then I wanted to find a hotel close to our narrowed locations. I quieried Google's nearby searches to find a list of the nearest hotels. I took the first one and added the hotel name and coordinates to the df. Then, I used citipy to grab the city name and country of the hotel to put it into the dataframe. I then placed them along with our heatmap on the google map.</p>

<p>Evan Mobley | <a href="https://www.linkedin.com/in/evanmmobley/">LinkedIn</a> | emmobley63@gmail.com
