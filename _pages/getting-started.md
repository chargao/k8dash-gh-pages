---
layout: single
title: Getting Started With k8dash
permalink: /getting-started/
sidebar:
  nav: "docs"
---

Once you have k8dash running, familiarize yourself with the k8dash user interface.

| Nodes            | Shows the list of servers and CPU / RAM used by each server. This information can provide insights on server resource allocations.<br><br>For more details, click on a server. This shows which pods are running on that server. |
| Workloads        | Shows the deployments, daemon sets, jobs, etc. This information can be useful to monitor deployments.<br><br>For more details, click on the listed pods. In this view, you can:{::nomarkdown}<ul><li>Edit the pod configuration YAML</li><li>View the documentation</li><li>Delete a pod</li><li>View logs or even SSH directly into a pod directly from your browser</li></ul>{:/} |
| Namespace        | Lets you filter your cluster details by namespace. |
| Config Maps      | A config map is a Kubernetes concept that allows you to set up configurations and tie them to deployments. |
| Service Accounts | Lets you manage users, roles, and permissions for your cluster. |
| Apply            | Lets you enter YAML to make configuration changes to your cluster. |
| Ingress          | Lets you manage configurations. |
| Storage          | Lets you manage persistent volumes and claims. |

k8dash also includes sections for Services, Replicas, and more. 

{::comment}Turns out having a list in a table is not very syntactically pleasant in kramdown. FYI{:/comment}