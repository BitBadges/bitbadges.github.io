---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: Database Schema
description: Information about ...

# Author box
author:
    title: About Author
    title_url: 'https://www.bitclout.com/u/BitBadges'
    external_url: true
    description: What is BitBadges? Our project allows any BitClout user to associate with any other user(s) through a NFT that is linked to the recipient's public key (no selling it). So once you earn a badge, no one can take it way from you!
    
# Micro navigation
micro_nav: true

# Page navigation
page_nav:
    prev:
        content: Previous page
        url: 'https://bitbadges.github.io/usecases'
    next:
        content: Next page
        url: 'https://bitbadges.github.io/codebase'
---

# Database Schema
There are three things stored in the BitBadges database: badges, badgePages, and users

## Database Schema
**Badges**
```javascript
{
    backgroundColor: string, //Valid HTML color name or hex string
    dateCreated: Number, //number of seconds since UNIX epoch
    description: string,
    externalUrl: string,
    id: string, //IPFS hash
    imageUrl: string,
    issuer: string, //BitClout public key
    recipients: string array, //BitClout public key
    title: string,
    validDateEnd: Number, //number of seconds since UNIX epoch
    validDateStart: Number, //number of seconds since UNIX epoch
    validDates: boolean //true if start/end dates, false if not
}
```
**Badge Pages (Ads)**
```javascript
{
    backgroundColor: string, //Valid HTML color name or hex string
    description: string,
    externalUrl: string,
    id: string, //IPFS hash
    imageUrl: string,
    issuer: string, //BitClout public key
    title: string,
    preReqs: string, //what it takes to earn the badge
    validity: string //explain how long the badge lasts
}
```
**Users**
```javascript
{
    badgesCreated: string array, //ids of badge pages or ads created
    badgesIssued: string array, //ids of badges given out
    badgesReceived: string array, //ids of badges received
    portfolioPages: object array //page details for a user profile
}
```
*Portfolio page object:*
```javascript
{
    badges: string array, //ids of badges on the given page
    pageTitle: string,
    pageNum: Number, //display index of page (starts at location 0),
    description: string
}
```
