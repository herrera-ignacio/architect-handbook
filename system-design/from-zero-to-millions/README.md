# Scaling From Zero to Millions of Users

## Overview

> The following text is from "System Design Interview" by Alex Xu.

The following techniques can be applied to scale a system to support millions of users:

* Keep web tier stateless
* Build redundancy at every tier
* Cache data as much as you can
* Support multiple data centers
* Host static assets in CDN
* Scale your data tier by sharding
* Split tiers into individual services
* Favor asynchronous communication (e.g., message queues)
* Monitor your system and use automation tools

## Simple App

![](2021-08-28-20-33-50.png)

## Example scalable design

![](2021-08-28-20-34-25.png)
