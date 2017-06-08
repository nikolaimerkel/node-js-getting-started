# node-js-getting-started

A barebones Node.js app using [Express 4](http://expressjs.com/) forked from [heroku/node-js-getting-started](https://github.com/heroku/node-js-getting-started). 

## Running Locally

Make sure you have [Docker](https://www.docker.com/) installed.

```sh
$ git clone https://github.com/nikolaimerkel/node-js-getting-started.git
$ cd node-js-getting-started
$ docker build -t merkel/nodejs .
$ docker run -it -p 8080:8080 merkel/nodejs
```

Your app should now be running on [localhost:8080](http://localhost:8080/).
