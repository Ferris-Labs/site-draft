---
title: "A Guide to Config Namespaces"
linkTitle: "Config Namespaces"
weight: -10
description: >-
  A Guide to Config Namespaces.
---

## Key Concepts
Ensuring easy and consequent configuration management is very important for platforms such as DX which must integrate with a number of systems. Further each integration or connection may require to be specific to a technical service account. 

We therefor have adopted a simple yet powerful mechanism for configuration management which may already be familiar to you.

There are 2 types of configurations

- Plain Text Configurations
- Secrets



<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" width="487px" viewBox="-0.5 -0.5 487 164" content="&lt;mxfile host=&quot;app.diagrams.net&quot; modified=&quot;2022-03-05T06:29:27.819Z&quot; agent=&quot;5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.51 Safari/537.36&quot; etag=&quot;LfWMO_MqYFsY4A_CoFYK&quot; version=&quot;16.6.6&quot; type=&quot;device&quot;&gt;&lt;diagram id=&quot;mnDSCzE9BJ2rOylmClfJ&quot; name=&quot;Page-1&quot;&gt;zZbfc6IwEMf/Gh57I6Coj2rFdryb3umMbZ860ayQXmCdGATur78gicBIaztXZ84HJ/vd/GA/u1mw3EmUzQTZhT+QArecDs0s99ZynGHXU/+FkJdCtz8ohUAwWkp2JSzZH9BiR6sJo7BvTJSIXLJdU9xgHMNGNjQiBKbNaVvkzVN3JIAzYbkh/Fx9ZFSGpTpw+pV+BywIzcm2Nyw9ETGTdST7kFBMa5I7tdyJQJTlKMomwAt2hku5zn/De3owAbH8yAIvOdjJYbDGX/jUWeSHfrqKbvQuB8ITHbDleFztN16rQVAMRj9Hk7upmjQf+fORcatzTjN0fDI30AQmMYXi3I5ypyGTsNyRTeFNVZUoLZQRV5Z9Wl2PwzwUCAlZTdJxzQAjkCJXU4y3oxnrIrMH2k6rlNlDrYW1dHW1RnSVBKetK5BqoFl+gqtzmet48TCfLj7J077Mcy8F/oYJchRKiTGGQjTF90XEu3a3QdxpI+60EPeuRbzXQvxfynLLODcQLcf1fVf9rkCyd7l0e1eq3If71cvckc8z31u9MPcm7Y3XhmMNG1DVEbUJfI3ptBLGKGSIAcaEf0fcaSyvIGWuezlJJDbJQsbkU238XCTkW09bt5nOz9HIjRHTUdHNlYkqxaXisyK0o795QyjZhyejjKcI4s3GqaU9JmID77DRJSWJCEC+U4tOe8YFcCLZofkcX57AD7Sea7f01hZUv1AUtiQ5Htpync7uTkuy/otXgTKr1/fRV/sGcqd/AQ==&lt;/diagram&gt;&lt;/mxfile&gt;" onclick="(function(svg){var src=window.event.target||window.event.srcElement;while (src!=null&amp;&amp;src.nodeName.toLowerCase()!='a'){src=src.parentNode;}if(src==null){if(svg.wnd!=null&amp;&amp;!svg.wnd.closed){svg.wnd.focus();}else{var r=function(evt){if(evt.data=='ready'&amp;&amp;evt.source==svg.wnd){svg.wnd.postMessage(decodeURIComponent(svg.getAttribute('content')),'*');window.removeEventListener('message',r);}};window.addEventListener('message',r);svg.wnd=window.open('https://viewer.diagrams.net/?client=1&amp;page=0&amp;edit=_blank');}}})(this);" style="cursor:pointer;max-width:100%;max-height:164px;"><defs/><g><rect x="50" y="0" width="190" height="40" fill="rgb(255, 255, 255)" stroke="rgb(0, 0, 0)" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 188px; height: 1px; padding-top: 20px; margin-left: 51px;"><div data-drawio-colors="color: rgb(0, 0, 0); " style="box-sizing: border-box; font-size: 0px; text-align: center;"><div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: rgb(0, 0, 0); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;"><b>APACHE KAFKA</b></div></div></div></foreignObject><text x="145" y="24" fill="rgb(0, 0, 0)" font-family="Helvetica" font-size="12px" text-anchor="middle">APACHE KAFKA</text></switch></g><rect x="364" y="100" width="120" height="60" rx="9" ry="9" fill="#000000" stroke="none" pointer-events="all" transform="translate(2,3)" opacity="0.25"/><rect x="364" y="100" width="120" height="60" rx="9" ry="9" fill="rgb(255, 255, 255)" stroke="none" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 118px; height: 1px; padding-top: 130px; margin-left: 365px;"><div data-drawio-colors="color: rgb(0, 0, 0); " style="box-sizing: border-box; font-size: 0px; text-align: center;"><div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: rgb(0, 0, 0); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;"><b>BROKER</b></div></div></div></foreignObject><text x="424" y="134" fill="rgb(0, 0, 0)" font-family="Helvetica" font-size="12px" text-anchor="middle">BROKER</text></switch></g><rect x="0" y="0" width="50" height="40" fill="#000000" stroke="#000000" pointer-events="all" transform="translate(2,3)" opacity="0.25"/><rect x="0" y="0" width="50" height="40" fill="#ff3333" stroke="rgb(0, 0, 0)" pointer-events="all"/><path d="M 240 20 L 292 20 Q 302 20 302 30 L 302 120 Q 302 130 312 130 L 361 130" fill="none" stroke="rgb(0, 0, 0)" stroke-miterlimit="10" stroke-dasharray="3 3" pointer-events="stroke"/><ellipse cx="364" cy="130" rx="3" ry="3" fill="none" stroke="rgb(0, 0, 0)" pointer-events="all"/><rect x="50" y="0" width="190" height="40" fill="#000000" stroke="none" pointer-events="all" transform="translate(2,3)" opacity="0.25"/><rect x="50" y="0" width="190" height="40" fill="rgb(255, 255, 255)" stroke="none" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility" style="overflow: visible; text-align: left;"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 188px; height: 1px; padding-top: 20px; margin-left: 51px;"><div data-drawio-colors="color: rgb(0, 0, 0); " style="box-sizing: border-box; font-size: 0px; text-align: center;"><div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: rgb(0, 0, 0); line-height: 1.2; pointer-events: all; white-space: normal; overflow-wrap: normal;"><b>APACHE KAFKA</b></div></div></div></foreignObject><text x="145" y="24" fill="rgb(0, 0, 0)" font-family="Helvetica" font-size="12px" text-anchor="middle">APACHE KAFKA</text></switch></g></g><switch><g requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"/><a transform="translate(0,-5)" xlink:href="https://www.diagrams.net/doc/faq/svg-export-text-problems" target="_blank"><text text-anchor="middle" font-size="10px" x="50%" y="100%">Text is not SVG - cannot display</text></a></switch></svg>

As the names suggest the plain text configurations may be viewd as plain text whereas the secrets cannot be viewed in the management UI once they are loaded to the platform. Secrets can be updated by updating the values of a named secret, they can be created and deleted but not viewed.

The storage of the configs are handled in the backend by the Key-Value store Consul. 

- The Values are held as JSON. 
- While the keys themselves have a reasonbale level of flexibility we nonetheless specify certain key spaces which are reserved/pre-defined. These keyspaces normally hold configurations which are specific to pre-built adapters or packages which are distributed with Ferris.

The following are the key namespaces.

ferris.apps.* 

ferris.packages.*

ferris.adapters.*

ferris.env

ferris



