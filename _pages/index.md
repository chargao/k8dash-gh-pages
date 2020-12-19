---
layout: splash
title: k8dash
permalink: /
header:
  overlay_image: /assets/images/website_header_k8dash.png
whyk8dash:
  - image_path: /assets/images/cluster-health_k8dash_website_bucket.png
    alt: "Monitor Cluster Health"
    title: "Monitor Cluster Health"
    excerpt: "Quickly view your cluster’s health via real-time charts that help you track poorly performing resources."
  - image_path: /assets/images/fast-and-live_k8dash_website_bucket.png
    alt: "Fast and Live Metrics"
    title: "Fast and Live Metrics"
    excerpt: "Benefit from a Kubernetes dashboard that automatically refreshes and updates in real time."
  - image_path: /assets/images/responsive_k8dash_website_bucket.png
    alt: "Responsive UI"
    title: "Responsive UI"
    excerpt: "Monitor your cluster while on-the-go via the 100% responsive UI that runs on your phone or tablet."
---
## What is k8dash?

A Kubernetes dashboard that helps you understand and manage your cluster at a glance.
Get started  Join the Community

## Why k8dash?
{% include feature_row  id="whyk8dash" %}

## Set up k8dash in as little as a minute 

(todo add bootstrap columns for the below)
<div class="row">
  <div class="col-md-6" markdown="1">
  Install k8dash via the available yaml file

  * Download kubernetes-k8dash.yaml

  Deploy k8dash by running the following command:
  `kubectl apply -f https://raw.githubusercontent.com/herbrandson/k8dash/master/kubernetes-k8dash.yaml`

   To learn more, go to the install page.
  </div>
  <div class="col-md-6" markdown="1">
#### Start in as little as a minute
You can configure k8dash in multiple ways, making it totally customizable. A few features you can install include: 
* k8dash makes using OpenId Connect for authentication easy 
* If you do not have an ingress server set up, you can utilize a NodePort service
  </div>
</div>


Join the community on GitHub Discussions.