# PROJECT bungalow_challenge
This challenge is provided by [Bungalow](https://bungalow.com/). The purpose of this challenge is to test the development skill of the candidates. The requirements of this project is:
## Summary
1) Create a Vue project
2) Write one or more methods to ingest the endpoint provided below
3) Create an interface to display individual properties from the endpoint data into a client-side representation of tiles/cards similar to what you would find on our website (but ideally better).
## Requirements

For development, you will only need Node.js installed on your environment.

### Node

[Node](http://nodejs.org/) is really easy to install & now include [NPM](https://npmjs.org/).
You should be able to run the following command after the installation procedure
below.

    $ node --version
    v8.11.2

    $ npm --version
    5.6.0

## Install

    $ git clone https://github.com/namedyangfan/bungalow_challenge.git
    $ cd bungalow_challenge
    $ npm install

## Start & watch
```
npm run serve
```
the server listen to [port 8080](http://localhost:8080`) by default

## Example
#### overview
<a href="http://tinypic.com?ref=2qstksx" target="_blank"><img src="http://i64.tinypic.com/2qstksx.png" border="0" alt="Image and video hosting by TinyPic"></a>

#### searchable city filter
<img src="https://i.ibb.co/pKYFPY8/Screen-Shot-2019-02-27-at-11-25-14-AM.png" width="200"/>

#### room filter
<img src="https://i.ibb.co/MpWT9r5/Screen-Shot-2019-02-27-at-11-25-25-AM.png" width="200"/>

#### Move-in-Date filter
<a href="http://tinypic.com?ref=2uy61py" target="_blank"><img src="http://i66.tinypic.com/2uy61py.png" border="0" alt="Image and video hosting by TinyPic" width="200"></a>

## API
Two API routes were provided by [Bungalow](https://bungalow.com/)

 - get request for available cities:
```
https://fieldstone.bungalow.com/api/v1/markets/?format=json
```
 - get request for available listings in a given city(seattle):

```
https://fieldstone.bungalow.com/api/v1/listings/properties/?market__slug=seattle
```
## Features
 - responsive web components: multi-device experience
 - responsive images: the right resolution for any screen size
 - lazy loading Images: reduce the website loading time
 - searchable city selector: easy to search for your city
 - available rooms filter: filter the bungalows by its avliable rooms
 - move-in-date filter: filter the bungalows by its ealist move-in-date
 - router: save filter parameters 

## Assumptions
  1. User not using IE Browser for opening the site 
  2.  all cities have the same style and requirements for rendering
  3.  `slug` returned from the markets API can be used as the query parameter in the listings API
  4.  `display_name` returned from the markets API is the proper name for that market
  5.  all posting can be categorized into **available today**,**available in 5 days**, and **available in 1 month**
  6.  assume the maximum rooms per house is **10** and the minimum is **1**
  7.  listings API only returns a portion of the data that is small enough to be handled by the frontend
  8.  available room filter need to be saved on city selections
  9.  primary color is `#ef6c00`
  10.  the developer of this project has the right to use and modify the Bungalow Icon 

## Questions
        What is the preferred way to pass a function from parent component to child? (pass as a prop or an event?)

        The `Homepage` component has children components of `AvaliableRoom` and `MoveInDate`, should the 
        data of the filters handeled in the child components or the parent component. Does the parent component 
        need to know the filter setting? Should we do the filtering in the backend instead?

        Will any data or prop change trigger its correspondent components to be re-rendered?

        Is there any way that we could set the maximum number of rooms dynamicly? Is this required?
        
## Future Work
1.  The height of the card is set as static, it would be nice to set it as a dynamic number
2.  Add more filters
3.  Display help text for reset filter (reset filter is rendered when no rooms matches the filter setting)
4.  Add maps for displaying locations
5   Navigation bar is not working for small screens
