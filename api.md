---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: API Documentation
description: Here you will find information about the BitBadges API and the various get/post methods. Message us if you have any questions/concerns.

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

`GET` **Get User**  
`https://us-central1-bitbadges.cloudfunctions.net/api/users/:id`  
Gets all user's data

> **_Request Params:_**  
`id` string `User's BitClout public key (no usernames, please convert first using BitClout API)`  
**_Response:_**  

> 200 (OK):

```javascript
{
    badgesIssued: [string],
    badgesReceived: [string],
    badgesListed: [string],
    badgesAccepted: [string],
    badgesPending: [string],
    issuedCollections: [string],
    receivedCollections: [string]
}
```

`GET` **Get Badge**  
`https://us-central1-bitbadges.cloudfunctions.net/api/badge/:id`  
Gets badge data for a specific badge ID  
**_Request Params:_** `id` string `Badge ID`  
**_Response:_**  

> 200 (OK):

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

`POST` **Get Badges**  
`https://us-central1-bitbadges.cloudfunctions.net/api/badges`  
Gets all data for badges specified  
**_Request Body:_**  
`badgeIds` string[] `Array of badge ids to get`  
**_Response:_**  

> 200 (OK):

```javascript
{
    badges: [
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
    ]
}
```

`GET` **Get All Badges**  
All badge hashes are posted on the [@BitBadgesHash](https://bitclout.com/u/BitBadgesHash) account, so please interact w/ the BitClout backend API to see the full list of hashes.

_Note:_ All badges are permanent and won't change, so consider caching or storing them locally instead of adding stress to our API and database.

`POST` **Create Badge**  
`https://us-central1-bitbadges.cloudfunctions.net/api/badge`  
Creates a badge by uploading to IPFS, adding the hash id to respective user's badgesIssued and badgesPending array in our database, and posts hash to [@BitBadgesHash](https://bitclout.com/u/BitBadgesHash). First 25 recipients are free. After that it costs 0.005 $CLOUT per recipient (subject to change).  

**The recipients array must be valid public keys, no usernames should be entered here. This method does not a) check for if a public key exists or b) convert usernames to public key. Every element in the recipients array will be treated as a valid public key and badges will be issued to each one.**  

**_Request Body:_**  
`title` string `Badge title. Required.`  
`validDateEnd` number `Required if validDates is true, number of seconds since UNIX epoch`  
`validDateStart` number `Required if validDates is true, number of seconds since UNIX epoch`  
`validDates` boolean `true if badge is to have start/end dates; false if badge is valid forever`  
`description` string `Required but can be an empty string.`  
`backgroundColor` string `Required but can be an empty string. Must be a valid HTML color name or hex value ('#FFFFFF' or 'red'). Defaults to black`  
`externalUrl` string `Required but can be an empty string`  
`imageUrl` string `Required but can be an empty string. Defaults to sample badge image`  
`recipients` array `Public keys of recipients.`  
`issuer` string `Required`  
`jwt` string `jwt token obtained from BitClout identity that corresponds with publickey`  
`publickey` string `Public key of issuer; note the lowercase k`  
`signedTransactionHex` – string – `Required if twenty six or more recipients. Signed transaction hex of a send bitclout transaction from BitClout Identity that is sending at least 0.005 $CLOUT per recipient starting with the sixth one to the @BitBadges account on BitClout. See /getFeeTxn for more details on how to do this. Note: Hex must be already signed when inputted. For details on how to get it signed, visit the BitClout Identity API docs. We strongly recommend against using access level 4 for your app.`  
`amountNanos` – number – `Required if twenty six or more recipients. Number of nanos in the transaction specified by the signedTransactionHex; 10^9 nanos equals one $CLOUT`  

**_Response_**  

> 200 (OK):

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

`GET` **Get Fee Transaction**  
`https://us-central1-bitbadges.cloudfunctions.net/api/feeTxn/:senderKey/:numRecipients`  

Creates a “send-bitclout” transaction using the BitClout backend API with the minimum amount of $CLOUT transferred to @BitBadges in order to issue the badge with specified number of recipients. Current pricing is 0.005 $CLOUT starting with the sixth recipient. First five are free. If numRecipients is less than five, it will still create a transaction that sends 0 $CLOUT to @BitBadges. All pricing listed above does not include network fees.  

Once you obtain TransactionHex from this transaction, you must get it signed using BitClout Identity before you input it into the create badge method. For details on how to get it signed, visit the BitClout Identity API docs. We strongly recommend against using access level 4 for your app.  

**_Request Params:_**  
`senderKey`: string - `public key of account that is sending the $CLOUT to @BitBadges`  
`numRecipients`: string – `number of recipients of badge to be issued`  

**_Response:_**  

> 200 (OK):

```javascript
{
    TransactionHex: string, //hex of the txn sending $CLOUT to @BitBadges
    amountNanos: string, //number of nanos being spent in the transaction
}
```

`POST` **Accept Badge**  
`https://us-central1-bitbadges.cloudfunctions.net/api/acceptBadge`  
Accepts a badges by moving it from badgesPending to badgesAccepted  
**_Request Body:_**  
`badgeId` string `Badge Id to accept`  
`jwt` string `jwt token obtained from BitClout identity that corresponds with publickey`  
`publickey` string `Public key of issuer; note the lowercase k`  
**_Response:_**  

> 200 (OK):

```javascript
{
  general: string; //success message
}
```

`POST` **Decline Badge**  
`https://us-central1-bitbadges.cloudfunctions.net/api/declineBadge`  
Declines a badge by removing it from badgesPending  
**_Request Body:_**  
`badgeId` string `Badge Id to decline`  
`jwt` string `jwt token obtained from BitClout identity that corresponds with publickey`  
`publickey` string `Public key of issuer; note the lowercase k`  
**_Response:_**  

> 200 (OK):

```javascript
{
  general: string; //success message
}
```

`GET` **Get Badge Page**  
`https://us-central1-bitbadges.cloudfunctions.net/api/badgePages/:id`  
**_Request Params:_** `id` string `Badge Page ID`  
**_Response:_**  

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

`POST` **Create a Listed Badge**  
`https://us-central1-bitbadges.cloudfunctions.net/api/badgePages`  
**_Request Body:_**  
`backgroundColor`: string, //Valid HTML color name or hex string
`description`: string,
`externalUrl`: string,
`imageUrl`: string,
`issuer`: string, //BitClout public key
`title`: string,
`preReqs`: string, //what it takes to earn the badge
`validity`: string, //explain how long the badge lasts
`publickey` string `Public key of issuer; note the lowercase k`  
`jwt` string `jwt token obtained from BitClout identity that corresponds with publickey`  

**_Response_**  

> 200 (OK):

```javascript
{
  {
    backgroundColor: string, //Valid HTML color name or hex string
    description: string,
    externalUrl: string,
    id: string, //IPFS hash
    imageUrl: string,
    issuer: string, //BitClout public key
    title: string,
    preReqs: string, //what it takes to earn the badge
    validity: string, //explain how long the badge lasts
  },
}
```

`GET` **Get All User Badge Pages**  
`https://us-central1-bitbadges.cloudfunctions.net/api/userBadgePages/:userId`  
**_Request Params:_** `userId` string `User Public Key`  
**_Response_**  

> 200 (OK):

```javascript
{
  badgePages: [
    {
      backgroundColor: string, //Valid HTML color name or hex string
      description: string,
      externalUrl: string,
      id: string, //IPFS hash
      imageUrl: string,
      issuer: string, //BitClout public key
      title: string,
      preReqs: string, //what it takes to earn the badge
      validity: string, //explain how long the badge lasts
    },
  ];
}
```

`DELETE` **Delete Listed Badge for Offer**  
`https://us-central1-bitbadges.cloudfunctions.net/api/badgePages/:id`  
Deletes a listed badge and removes value from user badgesListed array  
**_Request Body:_**  
`id` string `ID of listed badge to be deleted`  
`publickey` string `Public key of issuer; note the lowercase k`  
`jwt` string `jwt token obtained from BitClout identity that corresponds with publickey`  
**_Response_**  

> 200 (OK):

```javascript
{
  general: 'Success message';
}
```

`GET` **Get Collection**  
`https://us-central1-bitbadges.cloudfunctions.net/api/collections/:userId/:name`  
**_Request Params:_** `userId` string `User Public Key`  
`name` string `Collection name you wish to get`
**_Response_**  

> 200 (OK):

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
};
```


`GET` **Get All Collections for a User**  
`https://us-central1-bitbadges.cloudfunctions.net/api/collections/:userId`  
**_Request Params:_** `userId` string `User Public Key`  
**_Response_**  

> 200 (OK):

```javascript
{
  collections: [
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
  ]
};
```


`POST` **Create Collection**  
`https://us-central1-bitbadges.cloudfunctions.net/api/users/createCollection`  
Creates a collection for a user. If receivedCollection is true, it is a collection of received badges. If not, a collection of issued badges instead. Name must be unique from other collections a user creates.  
**_Request Body:_**  
`description` string `description of current page; defaults to empty string if none provided`  
`badges` array `String array with all badges to showcase on the profile page; must be valid badges received by user`  
`name` string  
`receivedCollection` boolean  
`imageUrl` string  
`jwt` string `jwt token obtained from BitClout identity that corresponds with publickey`  
`publickey` string `Public key of issuer; note the lowercase k`  
**_Response_**  

> 200 (OK):

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

`DELETE` **Delete Collection**  
`https://us-central1-bitbadges.cloudfunctions.net/api/users/deleteCollection`  
Deletes a collection according to name specified
**_Request Body:_**  
`name` string `name of collection to be deleted`
`publickey` string `Public key of issuer; note the lowercase k`  
`jwt` string `jwt token obtained from BitClout identity that corresponds with publickey`  
**_Response_**  

> 200 (OK):

```javascript
{
  general: 'Success message';
}
```
