---
layout: post
title:  "Polination predictions for Luxembourg"
date:   2018-05-04
categories: ml
---

# Why?

No decent predictions for hay fever sufferers in Luxembourg.

# Data sources

Let's use data from polination data from [data.public.lu](https://data.public.lu/en/datasets/pollen/) which is convenient as it is a single download. Getting reliable weather data for Luxembourg is slightly more difficult - I had to revert to scraping [wunderground](https://www.wunderground.com/) - see [a small script](https://github.com/misza222/LuPollen/blob/master/getLuxWeather.ipynb)

# EDA

WiP

# Models

For a start there I've used simple linear model as a baseline. Features for linear model included day and week of the year, min and max temperature on the day.


# code on [github](https://github.com/misza222/LuPollen/)
