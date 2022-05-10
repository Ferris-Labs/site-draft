---
title: "Development Quickstart"
linkTitle: "Development Quickstart"
tags: [quickstart] 
categories: ["Getting Started"]
weight: 100
description: >-
     Understand the Ferris technologies and become a master developer.
---

# Core ferris components
* argocd.ferris.ai
* alertmanager.ferris.ai
* consul.ferris.ai
* grafana.ferris.ai
* home.ferris.ai
* jhub.ferris.ai
* kafkahq.ferris.ai
* keycloak.ferris.ai
* kibana.ferris.ai
* minio.ferris.ai
* pgadmin.ferris.ai
* presto.ferris.ai

  
# Accessing the cluster

Follow the connectivity [intructions](https://github.com/Ferris-Labs/platform-docs/wiki/Ferris-Connect-Quickstart)

# Deploying your application inside the cluster
## Prerequisites

1. [Install Google Cloud SDK](https://cloud.google.com/sdk/docs/install)
2. Build your docker images with the full application code and requirements inside.
3. Request permissions to push/pull from google container registry
4. Tag your images appropriately (this is required in order to push your images to our google container registry

<span></span>

	docker build -t eu.gcr.io/talent-test-drive/<image>:<version> .

Or tag existing image

    docker tag <source-image>:<version> eu.gcr.io/talent-test-drive/<image>:<version>

* Configured Docker to use `gcloud` as a credential helper

<span></span>

    gcloud auth configure-docker

<span></span>

	docker push eu.gcr.io/talent-test-drive/<image>:<version>

## Deploying the application

Two methods of deployment are made available to the developers
* Using a helm chart (a basic template where you only populate predefined variables - local to argo)
* Using Kubernetes manifests (the official method - sourced from Git)
  

*Note that the helm method should only be used during testing, while it is a quick way to test how your locally developed app would function in the cluster context, it is not reliable. The application spec is only stored on argocd and is basically localised to the particular project. It is also more error prune with not as many recoverability options. We should always use Git as the source of truth.* 

### Using our custom Helm chart (alpha version):   

1. In your browser navigate to argocd.ferris.ai
2. Create new application and give it a name
3. Project: `ferris` / `app`
4. Repository url:  `git@github.com:Ferris-Labs/ferris-app.git`
5. Path: `ferris-helm-chart`
6. Cluster: `https://kubernetes.default.svc`
7. Namespace: `ferris` / `app`
8. Customise the chart values 

### Using manifests:
To get you started we are providing basic Kubernetes resource [manifests templates](https://github.com/Ferris-Labs/platform-docs/tree/master/manifests-tmpl)

Legend:
- configmap.yaml: Use this to define your non-sensitive environmental key:value variable pairs
- deployment.yaml: Use this to define your main application spec (application name, image, container name, ports, map variables from configmaps or secrets, etc.)
- ingress.yaml: Use this to define a DNS record on the reverse proxy which will resolve to your application service (external communication)
- secret.yaml: Use this to define your sensitive environmental key:value variable pairs
- service.yaml: Use this to define a service name and port for your app which other apps may use to communicate (internal/cluster communication)

*Note there will be times where you won't have to make use of all the available resource manifests, you may just remove the entire resource definition or comment out the specification not required.* 

*For example:*  
*If you are deploying an API in most cases you don't want the users trying to reach your routes directly (external communication) - in that case you can omit the ingress resource all-together. The application communicating with your API will still be able to connect via the service resource (internal/cluster communication) by referencing the [service name and port](https://github.com/Ferris-Labs/platform-docs/wiki/02.-Development-Quickstart#cluster-communication)*  
    
*Other times you may requires some additional specifications, check out some official Kubernetes docs or contact the Ferris Ops team*

[Example](https://github.com/Ferris-Labs/platform-docs/tree/master/ferris-example) of a configured app based on the templates

Guidelines:
1. Download the templates locally 
2. Inside your specific manifests repo (the manifest repos are segregated per tenant and provided by the Ferris Ops team) create a directory for your application and copy the required resources into that directory
3. Populate the placeholder values and review your resources
4. Commit and push your changes to a development branch on your specific manifests repo
5. In your browser navigate to argocd.ferris.ai
6. Create new application and give it a name
7. Project: `ferris` / `app`
8. Sync Policy: `Manual` / `Automatic`
9. Repository url:  `git@github.com:Ferris-Labs/ferris-app.git` / `Your specific manifests repo will be made available by the Ferris Ops team`
10. Revision: `Your development branch`
11. Path: `The manifests directory you created for your application`
12. Cluster: `https://kubernetes.default.svc`
13. Namespace: `ferris` / `app`

*Note wether you can use the projects `ferris` / `app` or deploy to the corresponding namespaces `ferris`/ `app` will be determined by your Keycloak access rights.*  
Project access and permissions:
* core: Ferris Ops team
* ferris: Ferris core Dev team
* app: Tenant developers

## Cluster communication

Kubernetes provides inter cluster communication via an abstraction called services. Different applications can reference each others service name in order to connect (similarly to how Docker provides connectivity via container names running on the same network)  
    
Often you will be required to connect your application to a core Ferris service like a postgres database running in a different namespace - connecting to a service in a different namespace requires you to set the full \<service\>.\<namespace\> as your connection string. Eg: `postgres.core:5432`

### How to find the required service name and port for a particular app

Since all the apps are required to be deployed via argocd, we can use it as the main source for all our specifications.  
1. Navigate to argocd.ferris.ai
2. Find and select the app you are interested in (eg. postgres)
3. Using the default tree-view in argo, you will see all the main resources branching out from the main app starting from the left, and the sub components branching out from those resources, etc.
4. Find and select the resource with the abbreviation "svc" - short for service 
5. In the new window you will find all the necessary details like the service name, port & namespace  

_Note when looking and the service manifest you will find both "targetPort" and "port" - make sure to use the "port" spec._

## TLS implementation
TLS has been implemented on the ingress level  
All core components are served on a private *.ferris.ai domain and use SSL certificates signed by the custom FerrisRootCA  

### Enable via manifests
Using Ferris manifests templates the SSL redirection and TLS domain will be set by default.  
If during testing you wish to omit SSL redirection set the following to your ingress.yaml definition annotations section
```
annotations:
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
```
Additionally comment out the following section
```
  tls:
    - hosts:
      - HOSTNAME.ferris.ai
```

### Enable via ferris-helm-chart  
SSL redirection will be enabled by default when using ferris-helm-chart to deploy your app  
To disable set  
`ingress.annotations.nginx.ingress.kubernetes.io/ssl-redirect: false`

*For more details on the chart check [ferris-helm-chart](https://github.com/Integration-Alpha/ferris-argon/tree/ferris-labs-ferris/ferris-helm-chart#version-120)*

## OAuth implementation

OAuth2 has been implemented on the ingress level  
All core components will require Keycloak authentication before they can be accessed over HTTP  

As the authentication happens over the reverse proxy layer the application is still responsible for its own OAuth implementation if it wants to manage users/groups/tokens etc.  
But since the auth is cookie based, as long as the app and ingress make use of the same Keycloak client the integration will be seamless from one layer down to the other.  

### Enable via manifests 
For the minimum requirements add the following to your ingress.yaml definition annotations section  
```
annotations:
    kubernetes.io/ingress.class: "nginx"
    nginx.ingress.kubernetes.io/enable-cors: "true"
    nginx.ingress.kubernetes.io/auth-url: "https://auth.ferris.ai/oauth2/auth"
    nginx.ingress.kubernetes.io/auth-signin: "https://auth.ferris.ai/oauth2/start?rd=https://$host$request_uri$is_args$args"
    ingress.kubernetes.io/auth-send-body: "true"
    ingress.kubernetes.io/auth-method: "POST"
    nginx.ingress.kubernetes.io/auth-response-headers: "Authorization"
```

### Enable via ferris-helm-chart
OAuth will be enabled by default when using ferris-helm-chart to deploy your app  
To disable set  
`ingress.oauthEnabled: false`  

*For more details on the chart check [ferris-helm-chart](https://github.com/Integration-Alpha/ferris-argon/tree/ferris-labs-ferris/ferris-helm-chart#version-120)*

## Public access

As [stated](https://github.com/Ferris-Labs/platform-docs/wiki/01.-Ferris-Connect-Quickstart#import--trust-ferrisrootca), all Ferris platforms start-off as fully private clusters with no public endpoints and the only method of access being the OpenVPN server.  
In some cases clients will want to build apps for wider audiences, or developers will be required to receive callbacks or other forms of communication from external APIs and services - with an on-demand approach the Ferris Ops team will provide a public load balancer for those types of requests. 

### Make your app public

Once the load balancer serving the public endpoint is ready, make sure you have a registered domain pointing to the public IP address.  
Selecting the type of endpoint you want to provide with your application is as easy as selecting the proper ingress class within your ingress.yaml resource.  

The default selection for Ferris will be the private endpoint  
`kubernetes.io/ingress.class: "nginx"` 

Or route via the public endpoint by specifying  
`kubernetes.io/ingress.class: "nginx-ext"`
