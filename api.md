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
