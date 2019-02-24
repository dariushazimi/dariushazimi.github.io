---
layout: post
title: How to get Canonical ID for your IAM user 
subtitle: Get canonical id for your user id
bigimg: /img/path.jpg
tags: [s3, awscli]
---
You can also get your Canonical ID for your IAM user from the CLI command:

List all the buckets and your iam Canonical ID:

    aws s3api list-buckets  
    
And if you just want to get your Canonical ID:

    aws s3api list-buckets | grep ID