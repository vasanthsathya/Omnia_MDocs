---

title: "Multi-Pod Gateways"
description: "This feature enables network gateway communication between device pairs in two separate PODS"
tags: [Fabric Configuration, POD, POD configuration, Gateway Profile to a LAG ,Service, VLAN configuration]
search:
  boost: 2           # ← Lower than main overview
parent: Advanced Configuration




hide:
- toc
---

# Inter-Pod Gateways

This feature enables network gateway communication between device pairs in two *separate* PODS.

To use this feature, the PODS must *not* be connected by a Super Spine.

The image below shows a basic system containing two independent PODS with each containing a device pair. The PODS are devoid of a Super Spine connecting them. It is assumed that the requisite physical connections are made (an example would be a Leaf Pair in each POD, with each leaf connected by two wires, totaling four wires and involving eight ports).

![](media/32f252d9d98c05d65c646e11c1ba28cb.png)

![](media/c6abc0c5bda4bc6d0930fae4451bf8bf.png)

## Create Gateway Profiles

Go to **Templates / Gateway Profiles** to create the needed Gateway Profiles. ![](media/gateway_profiles_6_5_menu.png){: class="pop"}

## Adding a Gateway Profile to a LAG

Adding a gateway profile to a LAG is needed to create the connection. You set the connection in the port editing window under the *center* form field. Here you enable the BGP LAG checkbox and chosen Gateway. The diagram below shows these settings for a *single* port.

![](media/40b749964da0890985cc122b4439a3f9.png)

## Object Configuration Description

The chart below presents an *example* configuration that includes 2 PODS, 4 switches and 8 switch ports. Object names, IP addresses and Autonomous System numbers will differ for your configuration.

Port numbers are presented in a blue background and are specific to the example above.

![](media/d95d1ff48baa68ca6e9c0053a3224048.png)
