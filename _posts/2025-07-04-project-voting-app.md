---
title: "voting-app"
layout: post
date: 2025-07-04
categories: [projects]
permalink: /blog/projects/voting-app
tags: [voting-app]
---

# Voting APP - Docker & Kubernetes

## Overview

* Voting application is a sample application to practice docker and kubernetes.
* It has vote and result components , where we can record our votes in voting component and can see result in result component.

## Deployment Plan

Our object to deploy this app by using docker images and then deploy on to a k8s cluster

### 1. Voting App
* This component provides thr user interface to vote and is devloped in python and runs on port 80

* need to create docker image

### 2. Result App
* This component gives the result of votes. It is also a user interface runs on Nodejs and port 80

* need to create a docker image

### 3. Worker App
* Processes votes by reading from Redis and updating PostgreSQL; this component runs in the background and does not require direct access.

* docker image required

### 4. Redis DB
* Acts as the datastore for votes, listening on port 6379. It is accessed by both the voting app (to record votes) and the worker app (to process votes).

### 5. Postgresql DB
* Maintains aggregated vote counts with a service listening on port 5432. It is accessed by the worker app (to update votes) and the result app (to display results)

