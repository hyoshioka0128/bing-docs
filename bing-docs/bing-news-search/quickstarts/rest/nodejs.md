---
title: "Quickstart: Perform a news search with Node.js - Bing News Search REST API"
titleSuffix: Bing Search Services
description: Use this quickstart to send a request to Bing News Search REST API using Node.js.
services: bing-search-services
author: swhite-msft
manager: ehansen
ms.service: bing-search-services
ms.subservice: bing-news-search
ms.topic: quickstart
ms.date: 07/15/2020
ms.author: scottwhi
---

# Quickstart: Perform a news search using Node.js and Bing News Search REST API

Use this quickstart to make your first call to Bing News Search API. This simple JavaScript application sends a search query to the API and displays the JSON response.

Although this application is written in JavaScript and runs in Node.js, the API is a RESTful Web service compatible with most programming languages.

The source code for this sample is available on [GitHub](https://github.com/Azure-Samples/cognitive-services-REST-api-samples/blob/master/nodejs/Search/BingNewsSearchv7.js).

## Prerequisites

* The latest version of [Node.js](https://nodejs.org/en/download/).
* The [JavaScript Request Library](https://github.com/request/request).

<!--
[!INCLUDE [bing-news-search-signup-requirements](../../../../includes/bing-news-search-signup-requirements.md)]
-->

## Create and initialize the application

1. Create a new JavaScript file in your favorite IDE or editor, and set the strictness and HTTPS requirements.

    ```javascript
    'use strict';
    let https = require('https');
    ```

2. Create variables for the API endpoint, news API search path, your subscription key, and search term. 

    ```javascript
    let subscriptionKey = 'enter key here';
    let host = 'api.bing.microsoft.com';
    let path = '/v7.0/news/search';
    let term = 'Microsoft';
    ```

## Handle and parse the response

1. Define a function named `response_handler` that takes an HTTP call, `response`, as a parameter. 

   Add code to this function in the steps that follow.

2. Define a variable to contain the body of the JSON response.  

    ```javascript
    let response_handler = function (response) {
        let body = '';
    };
    ```

3. Store the body of the response when the `data` flag is called.

    ```javascript
    response.on('data', function (d) {
        body += d;
    });
    ```

3. When an `end` flag is signaled, the JSON and headers can be viewed.

    ```javascript
    response.on('end', function () {
        console.log('\nRelevant Headers:\n');
        for (var header in response.headers)
            // header keys are lower-cased by Node.js
            if (header.startsWith("bingapis-") || header.startsWith("x-msedge-"))
                 console.log(header + ": " + response.headers[header]);
        body = JSON.stringify(JSON.parse(body), null, '  ');
        console.log('\nJSON Response:\n');
        console.log(body);
     });
    ```

## Example JSON response

A successful response is returned in JSON, as shown in the following example: 

```json
{
   "_type": "News",
   "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/news\/search?q=Microsoft",
   "totalEstimatedMatches": 36,
   "sort": [
      {
         "name": "Best match",
         "id": "relevance",
         "isSelected": true,
         "url": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/news\/search?q=Microsoft"
      },
      {
         "name": "Most recent",
         "id": "date",
         "isSelected": false,
         "url": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/news\/search?q=Microsoft&sortby=date"
      }
   ],
   "value": [
      {
         "name": "Microsoft to open flagship London brick-and-mortar retail store",
         "url": "http:\/\/www.contoso.com\/article\/microsoft-to-open-flagshi...",
         "image": {
            "thumbnail": {
               "contentUrl": "https:\/\/www.bing.com\/th?id=ON.F9E4A49EC010417...",
               "width": 220,
               "height": 146
            }
         },
         "description": "After years of rumors about Microsoft opening a brick-and-mortar...", 
         "about": [
           {
             "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entiti...", 
             "name": "Microsoft"
           }, 
           {
             "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entit...", 
             "name": "London"
           }
         ], 
         "provider": [
           {
             "_type": "Organization", 
             "name": "Contoso"
           }
         ], 
          "datePublished": "2017-09-21T21:16:00.0000000Z", 
          "category": "ScienceAndTechnology"
      }, 

      . . .
      
      {
         "name": "Microsoft adds Availability Zones to its Azure cloud platform",
         "url": "https:\/\/contoso.com\/2017\/09\/21\/microsoft-adds-availability...",
         "image": {
            "thumbnail": {
               "contentUrl": "https:\/\/www.bing.com\/th?id=ON.0AE7595B9720...",
               "width": 700,
               "height": 466
            }
         },
         "description": "Microsoft has begun adding Availability Zones to its...",
         "about": [
            {
               "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entities\/a093e9b...",
               "name": "Microsoft"
            },
            {
               "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entities\/cf3abf7d-e379-...",
               "name": "Windows Azure"
            },
            {
               "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entities\/9cdd061c-1fae-d0...",
               "name": "Cloud"
            }
         ],
         "provider": [
            {
               "_type": "Organization",
               "name": "Contoso"
            }
         ],
         "datePublished": "2017-09-21T09:01:00.0000000Z",
         "category": "ScienceAndTechnology"
      }
   ]
}
```

## Next steps

> [!div class="nextstepaction"]
> [Create a single-page web app](../../tutorial/bing-news-search-single-page-app.md)
