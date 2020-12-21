---
layout: single
title: Overview
permalink: /overview/
sidebar:
  nav: "docs"
---
k8dash (pronounced /kāt,daSH/ or Kate Dash) is an open source Kubernetes dashboard that helps you quickly understand the concepts of your cluster in a visual way. You can also manage your cluster components via the dashboard.

{% include video id="u-1jGAhAHAM" provider="youtube" %}

## k8dash at a glance:

* k8dash was first released in March 2019.
* It has received over 660 GitHub stars and over 1.1 million Docker Hub pulls.
* In May, 2020, Indeed Engineering adopted the k8dash project. k8dash is installed as a standard at Indeed.

Please star the project at [github.com/indeedeng/k8dash](https://github.com/indeedeng/k8dash).

(TODO add screenshots here)

With k8dash you can do the following:
* Fully manage your cluster, including namespaces, nodes, pods, replica sets, deployments, storage, RBAC, and more.
* Learn the status of components, which pods are deployed, and which pods or deployments use the most resources.
* Benefit from a Kubernetes dashboard that automatically refreshes and updates in real time.
* Quickly view your cluster’s health via real-time charts that help you track poorly performing resources.
* Monitor your cluster while on-the-go via the 100% responsive UI that runs on your phone or tablet.
* Get started in as little as a minute using the provided YAML. 
* Update and scale your cluster via the Resource YAML Editor, which includes inline API docs that describe each field.
* Employ a Simple Open ID integration with no special proxies required.
* If you’re already using OIDC to secure your cluster, k8dash makes extending this to your dashboards easy: configure 2-3 environment variables and you’re up and running. No special authenticating proxies or other complicated configurations are required.

## Why k8dash

| Feature                    | k8dash | Octant | Lens | k9s | Default Web UI | 
| -------------------------- |:------:|:------:|:----:|:---:|:--------------:|
|Web based (no download required) | x |        |      |     | x              |
|Cluster management               | x | x      | x    | x   | x              |
|Mobile optimized                 | x |        |      |     |                |
|Real-time dashboards             | x | x      | x    |     |                |
|Native OIDC integration          | x |        |      |     |                | 
|Multi cluster management         |   | x      | x    | x   |                | 
|RBAC Support                     | x | x      | x    | x   | x              | 
|Plugin Functionality             |   | x      | x    | x   |                | 
|Metrics                          | x | x      | x    |    |x (not real-time)| 

#### A deeper dive into the open source Kubernetes dashboards listed above:

###### [Default Web UI](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/) ([GitHub](https://github.com/kubernetes/dashboard))
The default Kubernetes web UI allows you to perform cluster management without needing to download additional software. Limitations include: no real-time updates; not optimized for mobile; more complicated installation that creates many more Kubernetes objects. Additionally, The Kubernetes built-in dashboard only supports bearer token logins out of the box. Support for OIDC requires additional configuration, generally by setting up an authenticating proxy (a separate piece of software).

###### [K9s](https://k9scli.io/) ([GitHub](https://github.com/derailed/k9s)) 
K9s is a command line interface with ASCII art. It provides a terminal UI to interact with your Kubernetes clusters. The aim of the K9s project is to make it easier to navigate, observe, and manage your applications in the wild. K9s continually watches Kubernetes for changes and offers subsequent commands to interact with your observed resources.

###### [Octant](https://octant.dev/) ([GitHub](https://github.com/vmware-tanzu/octant)) 
Octant is an [extensible platform](https://reference.octant.dev/?path=/docs/docs-about-1-why--page) that features real-time updates and works as an installed desktop application. Octant helps you understand the complexity of Kubernetes clusters through a combination of introspective tooling, cluster navigation, and object management. Octant’s plug-in system provides additional functionality through gRPC. Because Octant is an installed desktop application, you can’t share links with others.

###### [Lens](https://k8slens.dev/) ([GitHub](https://github.com/lensapp/lens))
Lens, created by VMWare, is an installed desktop application. Lens bills itself as a Kubernetes IDE and offers real-time cluster state visualization and multi cluster management for hundreds of clusters. With Lens, you can manage extra large clusters, up to 25K pods. Prometheus powers resource utilization charts and trends with history. Lens also supports terminal access to nodes and containers. However, because Lens is an installed desktop application, you can’t share links with others.
