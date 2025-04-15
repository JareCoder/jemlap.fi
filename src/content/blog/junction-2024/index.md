---
title: 'Junction 2024'
publishDate: 2025-15-04
description: 'Our journey and success at one of the Europs biggest hacakthons.'
tags:
  - Hackathon
  - Docker
  - 3D
language: 'English'
heroImage: { src: './thumbnail.jpg', color: '#D58388' }
---
A weekend of pure brainstorming, development, troubleshooting and some more troubleshooting. Free food, workshops and cool challenges all provided for you. What more could you ask for?!

## What is Junction?
Junction is one of the biggest Hackathons in Europe. It's hosted in Helsinki with over 1500 attending every year. From all over the world! You can read more about Junction here: https://www.hackjunction.com

## Familiar faces, new challenges
It was our groups 3rd consecutive year attending Junction. We were one person short this time around, so we had an opportunity to bring a new friend with us. Lauri had no prior hackathon experience, so he had a lot to learn, see and feel.

## AAAAA! What should we do?
Picking the challenge is arguably the most stressful part of the hackathon. And you have to do that right at the beginning! Choosing an interesting track that not only suits your skills, but offers you something new to learn can be challenging. And it was. 

We ended up doing KONE's challenge called "BIM for any building, by anyone". The challenge was to generate 3D models from given floorplan SVG's. And then be able to place a KONE elevator in that building.

The challenge allowed us to dive deeper into 3D rendering and handling in a web development environment. Which was all quite new to us.

## Gameplan
Me having the most experience in 3D modeling and rendering, I started researching ready made solutions or projects for our SVG -> 3D process. After a few hours of digging we ended up finding a functional and dockerized project that would could use as our base and backend. It utilized some smart math and Blender under the hood to draw found lines from the SVG. And an trained OpenCV model to recognize walls, windows and doors from the SVGs.

Now that the tool from SVG -> 3D model had been found I could focus on getting it running in Azure and make sure we could access it. And oh boy was that easier said than done. After hours and hours of rebuilding Docker images, changing configurations and touching up code where needed in the project itself we finally got it up and running. Now we could use a basic API to upload an image, build the 3D model and then save it to an Azure blob storage.

While I was struggling with Azure and Docker containers the rest of the team built the Web app for rendering the models, arranging floors and uploading images. Additionally we made a Flutter app that you could use to render the 3D models in AR.

![Diagram](./quickbim_diagram.png)

## Sauna break
On Sunday after getting the project to a "near ready" state, we decided to take a break with the rooftop sauna. And oh boy was the view nice. Sauna was great and we had the opportunity to discuss other challenges and solutions with fellow hackers.