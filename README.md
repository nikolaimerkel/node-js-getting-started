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

## Running on OpenShift
```sh
$ oc new-app https://github.com/nikolaimerkel/node-js-getting-started
```

- An image stream will be created as "node:boron" that will track the source image
- A Docker build using source code from https://github.com/nikolaimerkel/node-js-getting-started will be created
  - The resulting image will be pushed to image stream "node-js-getting-started:latest"
  Every time "node:boron" changes a new build will be triggered
  - This image will be deployed in deployment config "node-js-getting-started"
- Port 8080 will be load balanced by service "node-js-getting-started"
- Other containers can access this service through the hostname "node-js-getting-started"

The following resources should be created:
- imagestream "node" (The input image. Also called builder image)
- imagestream "node-js-getting-started" (The output image) 
- buildconfig "node-js-getting-started" (Specifies docker as the strategy for building, this location https://github.com/nikolaimerkel/node-js-getting-started.git containing the sources to use and that the build output will be the ImageStreamTag *node-js-getting-started:latest*)
- deploymentconfig "node-js-getting-started"
- service "node-js-getting-started"

A route has to be created manually in order to expose the service. With the following command a route with edge TLS termination will be created.

```sh
$ oc create route edge my-route --service=node-js-getting-started
```

