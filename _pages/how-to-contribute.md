---
layout: single
title: How to contribute
permalink: /how-to-contribute/
toc: true
sidebar:
  nav: "docs"
---

We’re always looking for new contributions. If you would like to contribute, see the [list of issues in GitHub](https://github.com/indeedeng/k8dash/issues) or reach out to us on GitHub Discussions. You can also learn more by reading our [Contributing Guidelines](https://github.com/indeedeng/k8dash/blob/master/CONTRIBUTING.md). 

The k8dash team is also looking for additional maintainers. If you’re interested, you can learn more by reading [Path to Maintainership](https://github.com/indeedeng/k8dash/blob/master/PATH_TO_MAINTAINER.md).

## Development

### Prerequisites

* A running Kubernetes cluster. Installing and running [minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/) is an easy way to fulfill this prerequisite. After you install minikube, run it with the `minikube start --driver=docker` command.
* Once the cluster is up and running, create some login credentials as described in Logging In.

### High-level Architecture

k8dash has two main components:
* [Client-side](#client-side)
* [Server-side](#server-side)

#### Client-side

The k8dash client is a React application (using TypeScript) with minimal other dependencies. k8dash’s client-side architecture consists of:
* A React application built with create-react-app
* Sass
* Minimal third-party dependencies

The client-side code is in the client > src folder. Within this folder you can find:
* index.js
* The views and art in SVG format

To run the client:

1. Open a new terminal tab and navigate to the `/client` directory.
2. Run `npm i` and then `npm start`. 
    This will open up a browser window to your local k8dash dashboard. If everything compiles correctly, the site will load and you will see the following error message: `Unhandled Rejection (Error): Api request error: Forbidden....`
3. To close the message, click X (top right). After you close the message, you should see the UI where you can enter your token.

#### Server-side

The k8dash server-side code in index.js is a proxy to the Kubernetes API consisting of less than 200 lines of code. k8dash’s client-side architecture consists of:
* @kubernetes/client-node, the Kubernetes npm module
* Express webserver
* Node JS
* http-proxy-middleware for proxy requests to the Kubernetes API
openid-client npm module for Open ID Connect (OIDC)

To run the server:

1. From the `/server` directory, run `npm i` to install dependencies.
2. To run the server, run `npm start`. The server is a simple express.js server that is primarily responsible for proxying requests to the Kubernetes API server.

During development, the server will use whatever is configured in `~/.kube/config` to connect the desired cluster. If you are using minikube, for example, you can run `kubectl config set-context minikube` to set up `~/.kube/config` correctly.