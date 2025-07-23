
---
title: "k8s-Commands"
layout: post
date: 2025-07-23
categories: [k8s]
permalink: /blog/k8s/k8s-Commands
tags: [kubernetes, k8s, cluster]
header_includes:
  - <link rel="stylesheet" href="/assets/css/custom.css">

---


<h1 style="color:orange">Kubectl Commands Cheat Sheet</h1>

<h2 style="color: #2f196bff; font-size: 1.3em; font-weight: bold; background-color: #daf510ff; display: inline-block; padding: 2px 12px; border-radius: 6px; margin-top: 0.5em;">Pods</h2>


<span style="color: #f2540bff; font-weight: 700;">To Get List of Pods</span><br>

<code style="color: white; background-color: rgba(21, 63, 121, 1); font-size: 1.05em; padding: 2px 6px; border-radius: 4px; display: inline-block;">kubectl get pods</code>

<span style="color: #f2540bff; font-weight: 700;">To Get List of Pods of a namespace</span><br>

<code style="color: white; background-color: rgba(21, 63, 121, 1); font-size: 1.05em; padding: 2px 6px; border-radius: 4px; display: inline-block;">kubectl get pods -n dev</code>

<span style="color: #f2540bff; font-weight: 700;">To describe pod</span><br>

<code style="color: white; background-color: rgba(21, 63, 121, 1); font-size: 1.05em; padding: 2px 6px; border-radius: 4px; display: inline-block;">kubectl describe pod nginx-pod</code>

<span style="color: #f2540bff; font-weight: 700;">To describe pod in a particular namspace</span><br>

<code style="color: white; background-color: rgba(21, 63, 121, 1); font-size: 1.05em; padding: 2px 6px; border-radius: 4px; display: inline-block;">kubectl describe pod nginx-pod -n dev</code>


<h2 style="color: #2f196bff; font-size: 1.3em; font-weight: bold; background-color: #daf510ff; display: inline-block; padding: 2px 12px; border-radius: 6px; margin-top: 0.5em;">Declarative Commands</h2>

<span style="color: #f2540bff; font-weight: 700;">Create an NGINX Pod</span><br>

<code style="color: white; background-color: rgba(21, 63, 121, 1); font-size: 1.05em; padding: 2px 6px; border-radius: 4px; display: inline-block;">kubectl run nginx --image=nginx</code>

<span style="color: #f2540bff; font-weight: 700;">Generate POD Manifest YAML file (-o yaml). Don’t create it(–dry-run)</span><br>

<code style="color: white; background-color: rgba(21, 63, 121, 1); font-size: 1.05em; padding: 2px 6px; border-radius: 4px; display: inline-block;">kkubectl run nginx --image=nginx --dry-run=client -o yaml</code>

# Example using custom CSS classes:
<span class="k8s-desc">Delete a pod</span><br>
<code class="k8s-command">kubectl delete pod nginx-pod</code>
