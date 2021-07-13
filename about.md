---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: About
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
        url: 'https://bitbadges.github.io/'
    next:
        content: Next page
        url: 'https://bitbadges.github.io/vision/'
---
# What is BitBadges?
BitBadges is an open source, community driven platform where BitClout users can issue NFT badges to other users!

## Our Goal
BitBadges aims to help tie together social identity and NFT ownership on the internet through BitClout and the use of blockchain technology. We want to give a platform to creators and individuals that allows them to go peer to peer with any service they wish to offer. 

URL: bitbadges.web.app

## Laying the Foundation
We aim to provide the foundation upon which any developer can build any innovation they wish. Like BitClout laid the foundation by providing public access to data like posts, messages, transactions, etc, BitBadges lays the foundation by providing public access to badges. We offer a public API with access to all data for all badges so anyone can build whatever they wish on top of our ecosystem.
We are a completely open source and community driven project. BitBadges will not be run as a company, just code. Those who contribute and innovate within our ecosystem will be rewarded with the official BitBadges account creator coins.

Join the discord at: discord.gg/Hc9eU73S

## Badges
There are three main parts to BitBadges: issuing badges to others, advertising your badges, and showcasing the badges you have earned!
Issuing Badges: Badges can be issued by any user to any other user, but once a badge is issued, it is permanently on the blockchain and can't be changed. They are customizable, so you can issue a badge for anything from a gym membership to a college diploma to a store receipt. Customization options include background colors, start/end dates, image URLs, and much more. Badges are non-transferrable and will forever be linked to a public key once they are issued.  You must hold 0.05 BitBadges coin to be able to issue a badge.
Advertising Your Badges: If you want to offer your badge to others, create an advertisement for your badge on the BitBadge website! This advertisement should explain how the users can earn your badge and details about the badge. Some potential advertisers include professors trying to sell their course, content creators selling access to premium content, and much more!
Showcasing Your Badges: The last aspect of BitBadges is showing off your portfolio on your profile. Every user has a BitBadges profile that can be accessed simply by signing in on BitBadges using your BitClout account. Your profile can be customized however you would like it to be. You can show off all your work related badges and treat it like a LinkedIn resume, or you can show off all your athletic achievements. You can customize it however you would like and can even create different sections of your profile for different purposes!

## Behind the Scenes
Are these NFTs? Badges take inspiration from Ethereum's ERC-721 tokens, but the main difference between them is that badges are tied to a public key and non transferable.
How is a badge stored? When a badge is issued, its metadata (all its attributes as a JSON object) is stored as a text file on the Interplanetary FIle System (IPFS) and in the BitBadges database. The IPFS is a global shared file system, and the important attribute about IPFS is that once a file is uploaded, it can't be changed. This means that your badges are permanent and can't be changed by anyone ever! This is important because one can prove ownership of a badge. Each IPFS file has a unique hash identifier which is automatically posted to @BitBadgesHash every time a badge is issued. This means that the data is also permanently stored on the BitClout blockchain.
Note: You may see some inconsistencies between the IPFS/@BitBadgesHash and the Firestore database for the timeframe when the platform was being developed and tested. Some test badges were deleted from certain user's profiles. Anything after __/__ is guaranteed to be consistent between the database and blockchain.
How are ads and profiles stored? All profile data and badge advertisements are stored in the BitBadges database. They are not stored on any permanent file storage because they can be edited.
Why are badges stored in a database if it is on the IPFS? It is stored in the BitBadges database because we offer a public API for anyone who wishes to get access to any badge's data. This allows anyone to create any innovation on top of the BitBadges foundation similar to how anyone can build on top of the BitClout core foundation. 
