# Cryptocurrency-Tracker-With-ESP8266-and-Arduino

### What?
The main goal is to have a dedicated, inexpensive, device that would help us avoid repeatedly checking websites, apps, email, writing scripts, etc., 
in order to monitor the ups and downs of coin prices.

In terms of what's required, I challenged myself to use the minimum number of parts, and require no special tools/skills such as soldering.

### How?
**THE HARDWARE**
- To build a price tracker for cryptocurrency we simply needed two pieces of hardware: 
   - an internet-capable microcontroller to gather the data, 
   - and a screen to display it, we tried to find the best solution considering ease of use and cost.

*OLED display*

Given our main goal of having a device with a small form factor that could sit on our desks, the first choice was to use a 0.96" OLED screen to display the price data.

Not only are these displays small (and bright!), but they're very easy to control over i2c merely having to connect 4 wires to our microcontroller or single-board computer: 
  - 2 for power and ground, 
  - and 2 for the data and clock lines.

*ESP8266 microcontroller (SoC)*

What can we say about the ESP8266 that hasn't been said about the wheel, sliced bread, or the iPhone... we love it! It's the most convenient, inexpensive way to have a microcontroller running code while connected to a Wi-Fi network.

The SoC comes in a variety of modules, breakouts, and development boards. 

For this project, we evaluated a few options and settled DevKit 1.0 Development Board for its compactness and our familiarity with using an OLED display with it in past projects OLED display with it in past projects!

**THE SOFTWARE**

Running on the microcontroller, we need 
  - software that's able to query the price data from dedicated servers, as well as 
  - to control the OLED screen to display the queried data.

*Price data API*

As of this writing, the best sites that provide a free API to query the current prices of different cryptocurrencies are:

* [coinmarketcap.com](coinmarketcap.com)<br>
* [coindesk.com](coindesk.com)<br>

Even better, at the moment they neither of them requires an API key, 
  - so we only need to write the firmware to perform queries and 
  - parse the result to obtain the necessary data.

*Firmware*

To perform the two tasks mentioned above, namely, query/parse data and control the OLED screen, we use a piece of code running on the ESP8266.

**The firmware performs 4 major tasks:**

*1. Connecting to the Internet*

Using the built-in Arduino library for the ESP8266 and entering our WiFi network credentials (ssid/password) we connect to the internet.

*2. Querying the data*

Using the built-in Arduino library for the ESP8266 , we create a WebClient object that allows us to send a GET request to the servers' APIs and retrieve the price data.

*3. Parsing the data*

Using Benoît Blanchon's fantastic Arduino JSON library (available in the Library Manager), we can easily get the parts of the JSON-formatted data that interest us.

*4. Displaying the data*

Using a couple of OLED Arduino libraries, it's straight forward to display the price data on the screen as well as our custom graphics. Most of the work, however, goes into making the UI both intuitive and aesthetically pleasing.
