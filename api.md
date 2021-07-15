---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: API Documentation
description: Here you will find information about the BitBadges API and the various get/post methods

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
```javascript
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
```javascript
{
    general: error message string
}
```

`Get` **Get Badge**  
`https://us-central1-bitbadges.cloudfunctions.net/api/badgePages/:id`  
***Request:*** `id` string `Badge Page ID`  
***Response:***
> 200 (OK):
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
> 400 (Bad Request)
```javascript
{
    general: error message string
}
```

**Get All Badges**  
All badge hashes are posted on the [@BitBadgesHash](https://bitclout.com/u/BitBadgesHash) account, so you will interact w/ the BitClout backend API to get the full list of hashes.

*Note:* All badges are permanent and won't change, so consider storing them locally instead of adding stress to our API and database.

`Get` **Get All Badge Pages**  
`https://us-central1-bitbadges.cloudfunctions.net/api/badgePages`  
***Response***
> 200 (OK):
```javascript
[
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
]
```

`Get` **Get Username**  
`https://us-central1-bitbadges.cloudfunctions.net/api/username/:publickey`  
Gets a user's profile data from the BitClout chain by specifying the public key. Done to bypass CORS policy.  
***Request:*** `publicKey` string `BitClout public key`  
***Response***  
> 200 (OK):
```javascript
{
    Profile: {
        Username: string,
        PublicKeyBase58Check: string
    }
}
```

`Get` **Get Public Key**  
`https://us-central1-bitbadges.cloudfunctions.net/api/publicKey/:username`  
Gets a user's profile data from the BitClout chain by specifying the public key. Done to bypass CORS policy.  
***Request:*** `username` string `username for the user`  
***Response***  
> 200 (OK):
```javascript
{
    Profile: {
        Username: string,
        PublicKeyBase58Check: string
    }
}
```
`Post` **Create Badge**  
`https://us-central1-bitbadges.cloudfunctions.net/api/badges`  
Creates a badge by uploading to IPFS, adding the hash id to respective user's badgesIssues and badgesReceived array in our database, and posts hash to [@BitBadgesHash](https://bitclout.com/u/BitBadgesHash). User must own 0.05 BitBadges coin to issue a badge.

**Note that recipients array must be valid public keys (not usernames). Also, there is no check for validity within this method. If an element in recipient array is invalid, it will be stored in our database and on IPFS with that invalid key and will not show up on intended user's profile.**  

***Request:***  
`title` string `Badge title. Required.`  
`validDateEnd` number `Required if validDates is true, number of seconds since UNIX epoch`  
`validDateStart` number `Required if validDates is true, number of seconds since UNIX epoch`  
`validDates` boolean `true if badge is to have start/end dates; false if badge is valid forever`  
`description` string `Required but can be an empty string.`  
`backgroundColor` string `Required but can be an empty string. Must be a valid HTML color name or hex value.`  
`externalUrl` string `Required but can be an empty string`  
`imageUrl` string `Required but can be an empty string`  
`recipients` array `Public keys of recipients.`  
`issuer` string `Required`  
`jwt` string `jwt token obtained from BitClout identity that corresponds with publickey`  
`publickey` string `Public key of issuer; note the lowercase k`  
***Response***  
> 200 (OK):
```javascript
{
    backgroundColor: string, //Valid HTML color name or hex string
    dateCreated: Number, //number of seconds since UNIX epoch
    description: string,
    externalUrl: string,
    id: string, //IPFS hash
    imageUrl: string,
    issuer: string, //BitClout public key
    recipient: string, //BitClout public key
    title: string,
    validDateEnd: Number, //number of seconds since UNIX epoch
    validDateStart: Number, //number of seconds since UNIX epoch
    validDates: boolean //true if start/end dates, false if not
}
```
`Delete` **Delete Badge Page (Ad)**  
`https://us-central1-bitbadges.cloudfunctions.net/api/badgePages/:id`  
Deletes badge page (ad) and removes value from user badgesCreated array  
***Request:***  
`id` string `ID of badge page to be deleted`  
`publickey` string `Public key of issuer; note the lowercase k`  
`jwt` string `jwt token obtained from BitClout identity that corresponds with publickey`   
***Response***  
> 200 (OK):
```javascript
{
    general: "Success message"
}
```
> 400 (Bad Request)
```javascript
{
    general: "Error message"
}
```

