---
title: "Ferris Connect Quickstart"
linkTitle: "Ferris Connect Quickstart"
tags: [quickstart, connect, register] 
categories: ["Getting Started"]
weight: 100
description: >-
     With this guide, you learn how to quickly estbalish a secure connection to Ferris.
---

## Install OpenVPN / download profile

- Navigate the OpenVPN url for your selected environment
- Check the contact column to request login credentials 
- Download and install openvpn client if your haven't done so previously 
- Download the user profile and import into the openvpn client app
- Connect after import

OpenVPN servers and profiles per environment:

| PROJECT        | ENV  | OPENVPN                                      | CONTACT                                                      |
| :------------- | :--- | :------------------------------------------- | :----------------------------------------------------------- |
| fl-ferris-demo | DEMO | [fl-ferris-demo-vpn](https://34.133.137.127) | [Ferris Info](mailto:info@ferrislabs.net?subject=fl-ferris-demo-vpn%20Credentials%20Request) |
| ia-ferris-demo | DEMO | [ia-ferris-demo-vpn](https://35.193.224.161) | [Ferris Info](mailto:info@ferrislabs.net?subject=fl-ferris-demo-vpn%20Credentials%20Request) |
|ferris-dev        |DEV|[ferris-dev-vpn](https://34.136.49.29)           |[Ferris Info](mailto:info@ferrislabs.net?subject=fl-ferris-demo-vpn%20Credentials%20Request)|


## Import & Trust FerrisRootCA 

All Ferris environments start-off as purely private clusters with only internal IPs. Each environment automatically bootstraps a component responsible for minting and managing its own \*.ferris.ai based ingress level TLS certificate. 

To implement TLS for the clusters we use a custom Ferris Certificate Authority, which is used to sign all freshly minted `*.ferris.ai` ertificates, making them trustworthy for the Ferris user base.

As the FerrisRootCA is not part of the well-known certificate authorities trusted by the browsers, developers and users should import FerrisRootCA in their keychains or browsers and mark it as a trusted source, in order to trust the SSL handshake when using any of our Ferris platforms.  

Below you can find a visual example on how to import the FerrisRootCA on a Mac system. Or follow similar guides for [Linux](https://linuxkamarada.com/en/2018/10/30/how-to-install-website-certificates-on-linux/) or [Windows](https://docs.vmware.com/en/VMware-Adapter-for-SAP-Landscape-Management/2.0.1/Installation-and-Administration-Guide-for-VLA-Administrators/GUID-D60F08AD-6E54-4959-A272-458D08B8B038.html).

*Note: The file shared is the FerrisRootCA public key; The private key is only available to selected individuals and never shared publicly or un-encrypted.*

Save the file [FerrisRootCA](https://raw.githubusercontent.com/Ferris-Labs/platform-docs/master/wiki-resources/certificates/FerrisRootCA.crt)  locally and follow the visual instructions.  

![How to import FerrisRootCA](/images/import-FerrisRootCA.png)

## Request Platform Access
If you are 
- a new joiner
- not part of the core development team
- or haven't registered until the deadline on 18.6.2021

you will be required to [register](https://argocd.ferris.ai/applications) as a new user on each environment you want to onboard. Once registered as a fresh user, you will have to manually request the admin team for permissions to gain access to the platform in order to pass the authorization flow.  
The minimum required Keycloak group is `platform-access`  
You may request additional permissions such as reading/writing to minio, various argocd development roles, etc.  
*Note: You will have read-only argocd access from the get-go*  

*After these steps you are set to start your Ferris journey*
