---
title: "k8s-Commands"
layout: post
date: 2025-07-23
categories: [k8s]
permalink: /blog/k8s/k8s-Commands
tags: [kubernetes, k8s, cluster]
---


<h1 style="color:orange">Kubectl Commands Cheat Sheet</h1>
<h2 style="color: #4a19d2ff; font-size: 1.3em; font-weight: bold; background-color: #92cddcff; display: inline-block; padding: 2px 12px; border-radius: 6px; margin-top: 0.5em;">Pods</h2>


<span style="color: #f2540bff; font-weight: 700;">To Get List of Pods</span><br>
<code style="color: white; background-color: rgba(57, 134, 241, 1); font-size: 1.05em; padding: 2px 6px; border-radius: 4px; display: inline-block;">kubectl get pods</code>

<span style="color: #f2540bff; font-weight: 700;">To Get List of Pods of a namespace</span><br>
<code style="color: white; background-color: rgba(57, 134, 241, 1); font-size: 1.05em; padding: 2px 6px; border-radius: 4px; display: inline-block;">kubectl get pods -n dev</code>

<span style="color: #f2540bff; font-weight: 700;">To describe pod</span><br>
<code style="color: white; background-color: rgba(57, 134, 241, 1); font-size: 1.05em; padding: 2px 6px; border-radius: 4px; display: inline-block;">kubectl describe pod nginx-pod</code>

<span style="color: #f2540bff; font-weight: 700;">To describe pod in a particular namspace</span><br>
<code style="color: white; background-color: rgba(57, 134, 241, 1); font-size: 1.05em; padding: 2px 6px; border-radius: 4px; display: inline-block;">kubectl describe pod nginx-pod -n dev</code>
