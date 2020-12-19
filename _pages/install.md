---
layout: single
title: Install
permalink: /install/
---
To install and run k8dash on your Kubernetes cluster, follow these steps:
1. Download [kubernetes-k8dash.yaml](https://raw.githubusercontent.com/herbrandson/k8dash/master/kubernetes-k8dash.yaml)
2. Deploy k8dash by running the following command:

    ```
    kubectl apply -f https://raw.githubusercontent.com/herbrandson/k8dash/master/kubernetes-k8dash.yaml
    ```
To access k8dash, you must make it publicly visible. If you have an ingress server setup, you can accomplish by adding a route like the following:

    ```
    kind: Ingress
    apiVersion: extensions/v1beta1
    metadata:
      name: k8dash
      namespace: kube-system
    spec:
      rules:
      -
        host: k8dash.example.com
        http:
          paths:
          -
            path: /
            backend:
              serviceName: k8dash
              servicePort: 80
    ```

3. Sign In

    1. Setting Up a Service Account Token

        The first (and easiest) option is to create a dedicated service account. This can be accomplished using the following script.

        ```
        # Create the service account in the current namespace (we assume default)
        kubectl create serviceaccount k8dash-sa

        # Give that service account root on the cluster
        kubectl create clusterrolebinding k8dash-sa --clusterrole=cluster-admin --serviceaccount=default:k8dash-sa

        # Find the secret that was created to hold the token for the SA
        kubectl get secrets

        # Show the contents of the secret to extract the token
        kubectl describe secret k8dash-sa-token-xxxxx
        ```

        Retrieve the token value from the secret and enter it into the login screen to access the dashboard.
    2. You can also log in to k8dash with OIDC

4. Optional: Use NodePort with k8dash

## Installing Metrics Server

k8dash relies heavily on [metrics-server](https://github.com/kubernetes-incubator/metrics-server) to display real-time cluster metrics. It is strongly recommended that you install metrics-server for the best experience from k8dash.
* [Installing metrics-server](https://github.com/kubernetes-incubator/metrics-server)
* [Running metrics-server with kubeadm](https://medium.com/@waleedkhan91/how-to-configure-metrics-server-on-kubeadm-provisioned-kubernetes-cluster-f755a2ac43a2)


## Running OIDC on k8dash

k8dash makes using OpenId Connect for authentication easy. Assuming your cluster is configured to use OIDC, all you need to do is create a secret containing your credentials and run the kubernetes-k8dash-oidc.yaml config.