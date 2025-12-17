---
layout: post
title: "Temperature Trend Web App"
date: 2020-10-26
categories: [software]
---

[Github](https://github.com/jasonepaul/django_weather_app/)

**Overview:**

A web app for displaying recent temperature trends. It shows the most recent eight weeks of daily minimum and maximum temperatures, along with the corresponding historical daily averages and records for the minimum and maximum temperatures.

**Motivation:**

The Software MEng program I recently completed was comprehensive but did not cover web development. I wanted to at least become a little acquainted with web development, so I took on a small project to cover topics including HTML, CSS, JavaScript, backend development, and deployment. I also enjoy working with data and ML, although ML is not used in this app (yet).

**Development:**

The Python based Django framework was used for backend development. There is a single app, the weather app, containing the business logic. The Bokeh visualization library was used for the plot. It includes a hover tool that displays the selected day’s min and max temperatures when viewed in a browser.

The raw data is accessed from a historical climate data API. Initially, the API is accessed to populate the statistics database table. This process takes over a minute as the data was obtained in yearly chunks (there are ~ 138 years of data) in csv format. The database tables are updated on a daily basis to stay current. Both the initial database population and daily updates are done as background processes using apscheduler. Pandas is used for data computation and structuring. Initially, some of the algorithms were designed using Jupyter Notebooks and then transferred to code modules using OOP.

**Deployment:**

Heroku cloud PaaS was used to host the app. The free tier was a good compromise for this MVP. The benefit is that it’s free, but one downside is that the dyno the app is installed on goes into an idle state when the app is not accessed for a period of 30 minutes. It can take ~ 20 seconds for the dyno to spin out of idle mode.

**Screenshots for Mobile and Desktop:**

{% include image.html src="/assets/posts/temp-trend-web-app/Temp Trend Web App iPhone.png" alt="Temp Trend Web App iPhone" caption="Image from iPhone" width="40%" %}

{% include image.html src="/assets/posts/temp-trend-web-app/Temp Trend Web App Chrome.png" alt="Temp Trend Web App Chrome" caption="Image from Chrome" %}

**Challenges:**

- Django: Obviously, there was the initial learning curve. By abstracting away a lot of the backend complexity of web development, it forces you to learn the details of the framework rather than the nuts and bolts of web development fundamentals.
- Background tasks: Initially I tried to avoid using background tasks. My rational was that I could implement the initial population of the statistics table simply by invoking functionality on first browser access of the site. This was not feasible since the Heroku dyno times out after working for more than 30 seconds on a request. I attempted to use Redis and RQ libraries to create a background task, only to find out that Heroku’s Redis To Go add-on is not free. After also trying the django-background-tasks library unsuccessfully, I was able to use apscheduler successfully.

**Future Considerations:**

- Use ML in the backend to do temperature forecasting for a period of 24 hours or 7 days, then compare this with Environment Canada’s forecast.
- Show tabular data below the plot.
- Allow users to choose one of several cities to display.
