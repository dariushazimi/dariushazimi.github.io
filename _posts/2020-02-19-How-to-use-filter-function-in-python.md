---
layout: post
title: How to use filter and Lambda function in python
subtitle: How to filter elements from a list using
bigimg: /img/path.jpg
tags: [filter, lambda]
---

Here is an exmaple to filter the list for the product with prices larger than $10.

    items = [
        ("product1", 10),
        ("product2", 3),
        ("product3", 210),
    ]

    filtered = list(filter(lambda item: item[1] >= 10, items))


    print(filtered)

and the output is:

    [('product1', 10), ('product3', 210)]