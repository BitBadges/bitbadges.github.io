---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: Database Schema
description: There are four things stored in the BitBadges database - badges, listed badges, collections, and users.

# Author box
author:
    title: About Author
    title_url: 'https://www.bitclout.com/u/BitBadges'
    external_url: true
    description: What is BitBadges? Our project utilizes a blockchain mechanism where users can associate with other user(s) through a NFT that is linked to the recipient's public key (no selling it). So once you earn a badge, no one can take it away from you!
    
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
There are four things stored in the BitBadges database: badges, badgePages, collections, and users.  

**Badges:** Badges are non transferable NFTs. Badges store all metadata about each NFT.  
**Listed Badges (badgePages):** Listed badges are advertisements to show off the badges you are offering.  
**Collections:** Users can group together badges they have either issued or received into a collection.  
**Users:** Users profiles store data about what badges they have issued, received, pending, and the collections they create.  

**Badges**
```javascript
{
    attributes: string, //valid JSON object string; not currently implemented
    backgroundColor: string, //Valid HTML color name or hex string
    category: string, //not currently implemented
    collectionId: string, //not currently implemented
    dateCreated: Number, //number of milliseconds since UNIX epoch
    description: string,
    externalUrl: string, //must be in valid URL format
    id: string, //IPFS hash
    imageUrl: string, //please use permanent image storage solutions; badges are permanent
    isVisible: boolean, //currently always set to true
    issuer: string, //BitClout public key
    issuerChain: string, //$CLOUT only for now
    recipients: string array, //BitClout public key
    recipientsChains: string array, //["$CLOUT", ...] only for now
    title: string, 
    validDateEnd: Number, //number of milliseconds since UNIX epoch
    validDateStart: Number, //number of milliseconds since UNIX epoch
    validDates: boolean //true if badge has start/end dates, false if valid forever
}
```
**Listed Badges (Ads)**
```javascript
{
    backgroundColor: string, //Valid HTML color name or hex string
    category: string, //is blank for now, not implemented yet
    dateCreated: number, //number of milliseconds since UNIX epoch
    description: string, 
    externalUrl: string,//must be in valid URL format
    id: string, //hash of id in our DB
    imageUrl: string, //must be in valid URL format
    issuer: string, //BitClout public key
    title: string,
    preReqs: string, //how to obtain the badge
    validity: string //explain how long the badge lasts
}
```
**Users**
```javascript
{
    badgesAccepted: string array, //ids of badges accepted to show on profile
    badgesListed: string array, //ids of badges listed for offer
    badgesIssued: string array, //ids of badges issued
    badgesPending: string array, //ids of pending badges (received but not accepted)
    badgesReceived: string array, //ids of any badges received (pending or not)
    issuedCollections: string array, //collection names made up of your issued badges
    receivedCollections: string array, //collection names made up of user's received badges
}

```
**Collections**
```javascript
{
    backgroundColor: string, //valid HTML color names
    badges: string array, //ids of badges on the given page, must be valid badges
    dateCreated: number, //number of milliseconds since UNIX epoch
    description: string,
    imageUrl: string, //must be in valid URL format
    isVisible: boolean, //always true for now
    issuers: string array, //public keys array of all issuers of badges in collection
    name: string, //title
    receivedColelction: boolean, //true if made up of received badges, false if issued badges
    recipients: string array //public keys array of all recipients of the badges in collection
}
```
