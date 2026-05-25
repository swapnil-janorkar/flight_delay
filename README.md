Flight Delay Time Statistics Dashboard
A Python-based interactive web dashboard built with Dash and Plotly that visualizes average flight delay times across US airlines, broken down by delay category and month for any selected year.

📌 Project Overview
This project aims to help analysts, aviation enthusiasts, and data scientists explore and understand patterns in US airline delay data. By selecting a year, users can instantly see how different airlines performed across five types of delays — giving a comprehensive view of operational reliability over time.
The dataset is sourced from IBM's Developer Skills Network and contains historical US domestic flight records including delay reasons, airline codes, and timing information.

🎯 What the Project Is Trying to Do
Flight delays are a major pain point in air travel. This dashboard addresses the question:

"Which airlines experience the most delays, of what type, and during which months?"

It breaks down the average delay time (in minutes) for each airline across five distinct delay categories and plots trends across all 12 months of a selected year. This allows users to:

Identify which airlines are most affected by specific delay types
Spot seasonal patterns (e.g., weather delays spiking in winter months)
Compare carrier reliability side by side across the year
Understand whether delays stem from external factors (weather, NAS) or internal factors (carrier, late aircraft)


📊 Output — What You See
When the dashboard runs, it opens a browser-based interactive web app with:
🔢 Input Field
A numeric input box labeled "Input Year" (default: 2010) at the top of the page. Changing this value instantly refreshes all five charts below.

📈 Five Line Charts (Plots)
Each chart shows Average Delay Time (minutes) on the Y-axis and Month (1–12) on the X-axis, with a separate colored line per airline (Reporting_Airline).
#Chart IDTitleWhat It Shows1carrier-plotAverage Carrier Delay Time by AirlineDelays caused by circumstances within the airline's control (e.g., maintenance, crew issues, aircraft cleaning)2weather-plotAverage Weather Delay Time by AirlineDelays directly attributable to weather conditions (storms, fog, ice)3nas-plotAverage NAS Delay Time by AirlineDelays caused by the National Airspace System — air traffic control, heavy traffic volume, airport operations4security-plotAverage Security Delay Time by AirlineDelays caused by security-related issues at the terminal or gate5late-plotAverage Late Aircraft Delay Time by AirlineDelays caused by a previous flight on the same aircraft arriving late, cascading into the next departure
Charts 1–4 are displayed in a 2×2 grid layout (two rows of two side-by-side charts). Chart 5 (Late Aircraft) is displayed below, spanning 65% of the page width.

🗂️ Dataset

Source: IBM Developer Skills Network (publicly hosted on IBM Cloud Object Storage)
URL: https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/...airline_data.csv
Encoding: ISO-8859-1
Key Columns Used:

ColumnDescriptionYearYear of the flightMonthMonth of the flight (1 = Jan, 12 = Dec)Reporting_AirlineAirline carrier code (e.g., AA, UA, DL)CarrierDelayMinutes of carrier-caused delayWeatherDelayMinutes of weather-caused delayNASDelayMinutes of NAS-caused delaySecurityDelayMinutes of security-caused delayLateAircraftDelayMinutes of late aircraft-caused delay

🧠 How It Works — Code Walkthrough
1. Data Loading
pythonairline_data = pd.read_csv('...airline_data.csv', encoding="ISO-8859-1", dtype={...})
The full dataset is loaded once into memory at startup.
2. App Layout
pythonapp.layout = html.Div([...])
Defines the page structure using Dash HTML components — a title, a year input field, and five dcc.Graph placeholders.
3. compute_info(airline_data, entered_year)
Filters the dataset to the selected year and computes monthly averages per airline for each of the five delay types using groupby + mean().
4. get_graph(entered_year) — Callback
Triggered every time the year input changes. Calls compute_info() and generates five Plotly Express line figures, returning them to update all five charts simultaneously.

🚀 How to Run
Prerequisites
bashpip install pandas plotly dash
Run the App
bashpython flight_delay.py
Then open your browser and navigate to:
http://127.0.0.1:8050/

🛠️ Tech Stack
ToolPurposePython 3.xCore languagePandasData loading, filtering, and aggregationPlotly ExpressGenerating interactive line chartsDashWeb application framework for the interactive UI

📁 File Structure
project/
│
├── flight_delay.py      # Main application file
└── README.md            # This file

💡 Possible Improvements

Add a dropdown for airline selection to filter specific carriers
Add a date range slider instead of a single year input
Include a map visualization showing delay hotspots by airport
Add bar chart comparisons for annual totals alongside monthly trends
Enable data export (CSV/PNG) from the dashboard


📄 License
This project uses publicly available data from IBM's Developer Skills Network, intended for educational purposes.
