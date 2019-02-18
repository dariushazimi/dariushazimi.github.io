---
layout: post
title: How to use Map and Lambda function in python
subtitle: How to get the elements from a list using Map
bigimg: /img/path.jpg
tags: [map, lambda]
---

Here is an exmaple to get the prices from the list.
Lat say we have the following list:

    items = [
        ("product1", 10),
        ("product2", 3),
        ("product3", 210),
    ]


We can use the map function as you can see below to get a list of prices.
    prices = list(map(lambda item: item[1], items))
    print(prices)

and the output is:

    [10, 3, 210]