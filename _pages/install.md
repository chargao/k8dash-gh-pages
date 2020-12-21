---
layout: single
title: Install
permalink: /install/
toc: true
sidebar:
  nav: "docs"
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

k8dash makes using OpenId Connect for authentication easy. Assuming your cluster is configured to use OIDC, all you need to do is create a secret containing your credentials and run the [kubernetes-k8dash-oidc.yaml](https://raw.githubusercontent.com/herbrandson/k8dash/master/kubernetes-k8dash-oidc.yaml) config.

To learn more about configuring a cluster for OIDC, check out these great links:

* [Authenticating \| Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/)
* [Kubernetes Day 2 Operations: AuthN/AuthZ with OIDC and a Little Help From Keycloak \| by Bob Killen \| Medium](https://medium.com/@mrbobbytables/kubernetes-day-2-operations-authn-authz-with-oidc-and-a-little-help-from-keycloak-de4ea1bdbbe)
* [kubectl with OpenID Connect. TL;DR \| by Hidetake Iwata \| Medium](https://medium.com/@int128/kubectl-with-openid-connect-43120b451672)
* [Kubernetes configure OIDC - Google Search](https://www.google.com/search?q=kubernetes+configure+oidc&oq=kubernetes+configure+oidc&aqs=chrome..69i57j0.4772j0j7&sourceid=chrome&ie=UTF-8)

You can deploy k8dash with OIDC support using something like the following script.

> **NOTE:** never trust a file downloaded from the internet. Make sure to review the contents of [kubernetes-k8dash-oidc.yaml](https://raw.githubusercontent.com/herbrandson/k8dash/master/kubernetes-k8dash-oidc.yaml) before running the script below.

```
OIDC_URL=<put your endpoint url here... something like https://accounts.google.com>
OIDC_ID=<put your id here... something like blah-blah-blah.apps.googleusercontent.com>
OIDC_SECRET=<put your oidc secret here>

kubectl create secret -n kube-system generic k8dash \
--from-literal=url="$OIDC_URL" \
--from-literal=id="$OIDC_ID" \
--from-literal=secret="$OIDC_SECRET"

kubectl apply -f https://raw.githubusercontent.com/herbrandson/k8dash/master/kubernetes-k8dash-oidc.yaml
```

Additionally, there are a few other OIDC options you can provide via environment variables. First is `OIDC_SCOPES`. The default value for this value is `openid email`, but additional scopes can also be added using something like `OIDC_SCOPES="openid email groups"`.

The other option is `OIDC_METADATA`. k8dash uses the excellent [node-openid-client](https://github.com/panva/node-openid-client) module. `OIDC_METADATA` will take a json string and pass it to the `Client` constructor. Docs [here](https://github.com/panva/node-openid-client/blob/master/docs/README.md#client). For example, `OIDC_METADATA='{"token_endpoint_auth_method":"client_secret_post"}`

## Running k8dash with NodePort

If you do not have an ingress server setup, you can utilize a NodePort service as configured in the [kubernetes-k8dash-nodeport.yaml](https://raw.githubusercontent.com/herbrandson/k8dash/master/kubernetes-k8dash-nodeport.yaml). This is ideal when creating a single node master, or if you want to get up and running as fast as possible.
This will map the k8dash port 4654 to a randomly selected port on the running node. The assigned port can be found using

```
$ kubectl get svc --namespace=kube-system

NAME       TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
k8dash     NodePort    10.107.107.62   <none>        4654:32565/TCP   1m
```

