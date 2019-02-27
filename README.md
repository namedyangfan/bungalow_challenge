# PROJECT bungalow_challenge

## Summary

## Requirements

For development, you will only need Node.js installed on your environement.

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

### Start & watch
```
npm run serve
```
Vue CLI use port 8080 as default. `http://localhost:8080/`

## Features
responsive web components: multi-device experience
responsice images: the right resolution for any screen size
lazy loading Images: reduce the website loading time
searchable city selector: easy to search for your city
avaliable rooms filter: the filter setting is saved for city selector

## Assumptions
User not using IE Browser for opening the site 
all cities have the same style and requirments for rendering
`slug` returned from the markets API can be used as the query parameter in the listings API
`display_name` returned from the markets API is the proper name for that market
all posting can be catagorized into *avaliable today*,*avaliable in 5 days*, and *avaliable in 1 month*
listings API only returns a portion of the data that is small enough to be handled by the frontend
avaliable room filter need to be saved on city selections
primary color is `#ef6c00`
the developer of this project has the right to use and modify the Bungalow Icon 

## Commit Style Guid
ref:
style:
core:
fix:
## Future Work and Questions
What is the preferred way to pass a function from parent component to child?
Will any data or prop change trigger its correspondent components to be rerendered?

