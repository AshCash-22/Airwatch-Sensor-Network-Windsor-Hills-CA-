# AirWatch-A-Low-Cost-Sensor-Network-for-Community-Air-Quality-Monitoring
Who I am

Hi, my name is Ashley and this is my Airwatch Senor Network for my city, Windsor Hills, CA! I am a 17 year old female African American who strives to learn more about hardware and softwre components, and how they help our world. 

Why I built this

Los Angeles County covers more than 4,000 square miles, but its official air quality monitoring network is limited. Many neighborhoods, including mine, do not have a monitor nearby. This means residents have no reliable way to know what they are breathing each day. People in my community had concerns about local air quality, but there was no local data to support those concerns or track changes over time.

I wanted to fill that gap by building a low-cost sensor that could give my neighborhood real, local air quality data and make it available for anyone to check. This project combines what I want to study—Electrical and Computer Engineering—with a problem I care about, which is why I chose it as my passion project.

What it does

AirWatch is an ESP32-based sensor station that measures particulate matter (PM1.0, PM2.5, PM10), general air quality and gas indicators, as well as temperature and humidity. It streams the data live to a public dashboard. Anyone, whether a neighbor, a parent, or a curious kid, can open the dashboard and see current conditions without needing any technical background.

Design decisions, and why I made them

I made many choices while building this, and most involved tradeoffs. I am sharing my reasoning here because I believe the decisions are just as important as the final result.

Why did I choose an ESP32 instead of a basic Arduino Uno? The main requirement for this project was to send data from the device to the internet. An Arduino Uno does not have built-in WiFi, so I would have needed to add a WiFi shield, which would increase cost, complexity, and the chance of something going wrong. The ESP32 has built-in WiFi, costs less than an Uno with a WiFi shield, and can still be programmed using the Arduino IDE. Given my timeline and budget, this was the more efficient choice, not just a more advanced one.

Why did I choose the PMS5003 for particulate matter? I picked the PMS5003 instead of cheaper dust sensors because it uses laser scattering to measure PM1.0, PM2.5, and PM10 separately, instead of giving just one general "dust level" number. PM2.5 is the metric most health guidelines (EPA, WHO) use, so I needed a sensor accurate enough to report it directly instead of estimating.

Why did I use the BME680 along with the PMS5003? Measuring only particulate matter does not give the full picture of air quality. The BME680 adds a general gas resistance reading, which is a proxy for VOCs, as well as temperature, humidity, and pressure. These factors all affect how pollutants behave and spread. I was honest with myself that this sensor does not measure any single pollutant, like benzene, very precisely; it gives a general indicator, not a lab-grade reading. I decided it was better to be clear about its limits than to pretend it measured something more specific.

Why did I use Adafruit IO instead of building a custom website? At first, I thought about creating a full custom website with its own database and backend. I decided not to do that because my free Adafruit IO account gives me live-updating public dashboards, stores historical data, and provides a shareable link, all without needing to build or maintain server infrastructure. Since I needed to build, deploy, and start collecting real data within a few months, I thought it was better to focus my effort on the sensor hardware and data quality instead of creating a dashboard from scratch. If I have extra time later, I can build a custom front-end using my existing data, but it is not required.

Why did I limit my cloud dashboard to 5 data feeds? My Adafruit IO account only allows 5 feeds on the free tier. Instead of upgrading or finding a workaround, I used this limit to help me prioritize. I kept PM2.5, PM10, temperature, humidity, and gas resistance on the public dashboard because these values are most important to my air quality mission and most useful to a general audience. I left out PM1.0 and barometric pressure from the public feed, not because they are unimportant, but because they are less central to the story I want to tell. This was a real engineering tradeoff: deciding what is most important to share given a strict limit.

Why did I decide not to add local SD card backup logging? At first, I planned to add a microSD card module as a backup in case the device's WiFi connection failed outdoors. After several attempts at wiring and setup, I chose to leave it out. My reasoning was that Adafruit IO already keeps a timestamped history of every reading, which serves as a durable record of my data without adding another hardware point of failure. Given my timeline, I felt the SD card added risk and complexity without much extra value. If WiFi drops briefly during deployment, there will be a small, understandable gap in that day's data, but I would rather have a reliable, simpler device than a fragile one with unnecessary features.

Why am I running one sensor station instead of a full network? At first, I thought about setting up two or three stations in different locations for comparison. But with my application deadline, I decided to focus on building and testing one station thoroughly. One well-documented and reliable station is a stronger and more honest project than several stations built too quickly to trust. If I have more time later, expanding to a second location would be a natural next step.

How I validated it

Before setting up the sensor outdoors, I compared my readings with the nearest official monitors on PurpleAir and AirNow over several days. This helped me confirm that my sensor's readings were reasonable and followed real trends instead of just producing random data. My station is not lab-grade equipment, and I do not claim that it is. It is a low-cost tool meant to fill a coverage gap, not to replace regulatory-grade monitoring.

What I learned

This project taught me the real mechanics of embedded systems: connecting multiple sensors using different protocols (UART for the PMS5003, I2C for the BME680) on one microcontroller, managing wireless data transmission within a service's rate limits, and solving real hardware problems like driver issues, wiring mistakes, and a stubborn SD card module I eventually removed. Just as importantly, it taught me how to explain technical work to people without a technical background. The main goal of the public dashboard is for my neighbors, not just other engineers, to understand what it shows.

Hardware

* ESP32 (WROOM-32) microcontroller
* PMS5003 laser particulate matter sensor
* BME680 environmental sensor (temperature, humidity, pressure, gas/VOC)
* Weatherproof outdoor enclosure

Status

In progress. The sensor is currently deployed and collecting data. This README will be updated with final results, charts, and findings as the project wraps up.
