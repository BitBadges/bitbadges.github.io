---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: API Documentation
description: Information about ...

# Author box
author:
    title: About Author
    title_url: 'https://www.bitclout.com/u/BitBadges'
    external_url: true
    description: Information about ...

# Micro navigation
micro_nav: true

# Page navigation
page_nav:
    prev:
        content: Previous page
        url: 'https://bitbadges.github.io/codebase'
    next:
        content: Next page
        url: 'https://bitbadges.github.io'
---

# API Documentation

`Get` **Get User**  
`https://us-central1-bitbadges.cloudfunctions.net/api/users/:id`  
Gets all the user's data  
***Request:*** `id` string `BitClout Username`  
***Response:***
> 200 (OK):
``` JavaScript
{
    badgesIssued: [string],
    badgesReceived: [string],
    badgesCreated: [string],
    portfolioPages: [
        {
            pageNum: Number,
            pageTitle: string,
            badges: [string]
        }
    ]
}
```
> 400 (Bad Request)
``` JavaScript
{
    general: error message string
}
```
