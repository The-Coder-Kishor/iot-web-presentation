---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# some information about your slides, markdown enabled
background: https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.freepik.com%2Ffree-photos-vectors%2Fiot-background&psig=AOvVaw3Flz-zj8ncTlqqL79o1M-W&ust=1714068928520000&source=images&cd=vfe&opi=89978449&ved=0CBAQjRxqFwoTCKDGv76624UDFQAAAAAdAAAAABAJ
title: Personalized Climate Control Project
info: |
  ## Presentation for the IoT Project
# apply any unocss classes to the current slide
class: text-center
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# https://sli.dev/guide/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations#slide-transitions
transition: fade-out
# enable MDC Syntax: https://sli.dev/guide/syntax#mdc-syntax
mdc: true
---

# Personalized Climate Control Project

## By: [Team 31]
Online Presentation Available [Here](https://the-coder-kishor.github.io/iot-web-presentation/)
<br /> 

### Sidharth K (2023101113)
### Aditya Shankar (2023111030)
### Adithya Kishor (2023111019)
### Anirudh Sankar (2023111024)

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/The-Coder-Kishor/iot-web-presentation" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>
<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: two-cols
layoutClass: gap-16
---

# Table of contents


::right::

<Toc v-click minDepth="1" maxDepth="2"></Toc>


---
transition: slide-up

---

# Motivation Behind the Project
<v-click>
The motivation behind the project was to create a proper working HVAC modelwhich can be used to adjust the environmental conditions according to the needs of the individual. Data collected over time from such a physical model can be later used to create much better ai agents that can optimize the energy consumption of the HVAC system.

- 📝 **Data Collection** - <span v-mark.underline.orange="1"> focus on collecting data in the form of humidity, temperature, pressure, pm2.5 and pm10 values </span>
- 🛠 **Hackable** - <span v-mark.underline.orange="2"> to allow the user to modify thresholds and turn actuators on and off </span>
-  🧑‍💻 **Developer Friendly** - <span v-mark.underline.orange="3"> to create a user accessible dashboard to show all the values, threshold and buttons that the user can use to get data about the room </span> 
</v-click>
<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
transition: slide-up

---

# Our Implementation

In our implementation we have used the following sensors:
- two <span v-mark.underline.orange="1">DHT11 sensor to collect the temperature and humidity values</span>
- <span v-mark.underline.orange="2">BME280 sensor </span>to collect the pressure values
- <span v-mark.underline.orange="3">SDS sensor to collect the pm2.5 and pm10 values.</span> (It however stopped working after a few days)
- We have used <span v-mark.underline.orange="4"> PC fans </span> to control airflow, both the fans blow inside to increase the pressure. The fans given to us are unidirectional so we cannot decrease the pressure in the room by inverting the polarity.
- An <span v-mark.underline.orange="5"> ESP32 Dev Module </span> as the interface between the sensors, actuators and the MQTT server
- An <span v-mark.underline.orange="6"> L298N Motor Driver </span> to drive the fans
- <span v-mark.underline.orange="7"> 12V Power Module </span> which can supply 3.3V, 5V and 12V which we require for the sensors, the ESP and the fans respectively.
- A <span v-mark.underline.orange="8">Thingspeak MQTT </span>server to save and receive data.
- A <span v-mark.underline.orange="9"> dashboard that updates itself </span> with new data and allows the user tochange their preferences for the HVAC system.


<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

<!--
Here is another comment.
-->
---
transition: slide-up

---

# Our Dashboard (Data and Data Analysis)

You can open the publicly hosted dashboard [here](https://the-coder-kishor.github.io/iot_web_dashboard/)

<iframe src="https://the-coder-kishor.github.io/iot_web_dashboard/" title="dashboard" style="height:45vh; width:45vw;"></iframe>

---
transition: slide-up
---

# Failure analysis of the prototype

The air quality sensor (SDS) fried up likely due to electrical overload or other unknown reasons, rendering it useless for air quality sensing.

The different cases where our prototype would likely fail are:-

1) Communication errors: Loss of Wifi connectivity and the entire setup can only be run when one of use is present in the room which means we were not able to capture much data during the mornings (when there were classes)
2) Mechanical issues: The given fan is unidirectional so were not able to switch its direction per will extremely reducing the operational freedom of the project
3) Wear and Tear of the components: The 12V power supply being used to power the fan, the esp and the sensors had immense static build up which was causing a serious problem.
5) Sensor inaccuracies: The SDS sensor which was providing us pm2.5 and pm10 sensors used to work in the beginning but then stopped working with no specific cause
6) Power Failures, Short circuits etc..

---
transition: slide-up
---

# Next Steps

The next possible steps include:-

1) Develop an intuitive and user-friendly app for users to set preferences, view real-time data, and receive alerts or notifications.
2) Integrate the climate control system with existing smart home platforms for seamless operation and compatibility with other smart devices.
3) Get better sensors, coolers and other actuators which can "actually" cool the environment.
4) This time we were not able to make a closed model to try stuff on because components would break often, so that is one thing we need to implement in the future.
5) Use the data taken from the project to create AI models that can be used for optimizing energy usage (the most important use of such a project).
---
transition: slide-up
---

# Thank You

The pdf of the presentation is available [here](https://github.com/The-Coder-Kishor/iot-web-presentation/blob/main/pdf/slides-export.pdf)