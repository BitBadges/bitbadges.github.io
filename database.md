---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: Database Schema
description: There are three things currently stored in the BitBadges database - badges, badgePages, and users

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
    attributes: string, //not currently implemented
    backgroundColor: string, //Valid HTML color name or hex string
    category: string, //not currently implemented
    collectionId: string, //not currently implemented
    dateCreated: Number, //number of seconds since UNIX epoch
    description: string,
    externalUrl: string,
    id: string, //IPFS hash
    imageUrl: string,
    isVisible: true,
    issuer: string, //BitClout public key
    issuerChain: string, //$CLOUT only for now
    recipients: string array, //BitClout public key
    recipientsChains: string array, //["$CLOUT", ...] only for now
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
    category: string, //is blank for now, not implemented yet
    dateCreated: number, 
    description: string,
    externalUrl: string,
    id: string, //hash of id in our DB
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
    badgesAccepted: string array, //ids of badges accepted to show on profile
    badgesListed: string array, //ids of badges listed for offer
    badgesIssued: string array, //ids of badges given out
    badgesPending: string array, //ids of badges pending to show on profile
    badgesReceived: string array, //ids of badges received
    issuedCollections: string array, //collections made up of your issued badges
    receivedCollections: string array, //collections made up of user's received badges
}

```
*Collection object:*
```javascript
{
    backgroundColor: string,
    badges: string array, //ids of badges on the given page
    dateCreated: number,
    description: string,
    imageUrl: string,
    isVisible: boolean, //always true for now
    issuers: string array, //array of all public keys in DB
    name: string,
    receivedColelction: boolean, //true if made up of received badges, false if issued badges
    recipients: string array //array of all public keys in DB
}
```
