---
layout: post
title: "Exploring IoT with Edge Devices"
date: 2021-02-01
categories:
---

**Technologies:**

- Programming languages: C++, Python, HTML/CSS/JavaScript
- Cloud services: AWS IoT Core, AWS Gateway API, AWS Lambda, AWS DynamoDB

**Overview:**

Two edge devices (Espressif ESP32 MCUs), configured with external temperature sensors, send temperature data via wifi and internet to a NoSQL database (Amazon DynamoDB). Device firmware is coded in C++ and employs the deep sleep functionality of the MCU, thus requiring as little as 10 micro amps of power consumption per device. A web page, which is hosted in an AWS S3 bucket, retrieves the most recent data from the database and displays it in a plot on the web page for the user. The data flow is illustrated below:

{% include image.html src="/assets/posts/exploring-iot-with-edge-devices/device-to-dynamodb.png" alt="Device Data to DynamoDB" caption="Device Data to DynamoDB" %}

{% include image.html src="/assets/posts/exploring-iot-with-edge-devices/aws-s3-lambda-dynamodb.png" alt="Webpage and Data Retrieval from DynamoDB (source: Amazon)" caption="Webpage and Data Retrieval from DynamoDB (source: Amazon)" %}

**Motivation:**

This project was born out of my desire to learn about technologies used for the Internet of Things and cloud computing in general.

**Screenshots:**

{% include image.html src="/assets/posts/exploring-iot-with-edge-devices/iot-proj-desktop-webpage.png" alt="Desktop Webpage" caption="Desktop Webpage" %}

{% include image.html src="/assets/posts/exploring-iot-with-edge-devices/iot-proj-smartphone-webpage.png" alt="Smartphone Webpage (Portrait Orientation)" caption="Smartphone Webpage (Portrait Orientation)" width="50%" %}

{% include image.html src="/assets/posts/exploring-iot-with-edge-devices/esp32s.jpg" alt="Espressif ESP32 MCUs with Temperature Sensors and Supporting Electronics" caption="Espressif ESP32 MCUs with Temperature Sensors and Supporting Electronics" %}

**Challenges:**

- Learning the nuances of the Chart.js JavaScript library
- Learning how to perform queries on a NoSQL database
- Programming the serverless Lambda function to ensure a lean front-end

**Future Considerations:**

- Connect battery packs to the devices instead of using grid power and transformer
- Explore ability to update firmware in real time using the IoT Core console
