# Homelab 🏡

## Intro

This repo contains all configurations, manifests, and documentation for my Homelab. I've created this project to experiment with a tech stack I enjoy working within an environment I fully control.

## Architectural Decisions

The main principle behind this project is to automate everything. For this reason, I decided to use Flux for a GitOps-based deployment strategy. Image updates happen using the Renovate bot, so I don't need to manually look for updates on any of the images I currently use for this project. 

## Structure

I've bootstrapped this project using Flux and Github as the git provider. I decided to commit to the suggested repository structure, following a [monorepo](https://fluxcd.io/flux/guides/repository-structure/#monorepo) approach. I use a base layer for most of my manifests and the staging and production layers for environment-specific configuration, notably CloudFlare tunnels (this is how I connect to my self-hosted Homelab outside my home network).


## Tech Stack
As mentioned above, I'm using Flux to handle deployments through GitOps and Github as the Git provider for my deployments, but there are a few other tools worth mentioning:

- K3s—I used K3s to provision my entire cluster. It is probably one of the easiest ways to provision a Kubernetes cluster on-prem, and it ships with a storage class out of the box, which is handy.
- CloudFlare Tunnels - I use CloudFlare tunnels to route traffic from my domain into my Homelab servers.
- Renovate—I'm using Renovate to check for new images every hour and create PRs for the updates. I could use Flux to handle this process, but I enjoy how Renovate creates and decorates the PR description for these updates. It gives me just enough information so that I feel fully in control of my updates while also automating the most tedious tasks.
- Sops with age encryption—I use Sops to encrypt and decrypt secret data on my cluster. Using Sops is helpful because I can commit my secrets to Git and keep them secure. It allows me to automate everything through Git-commit/Git-push.

## Hardware

I have a single-node cluster running on an Asus Vivobook S15 laptop. I'm currently looking into options to purchase new nodes. In the future, I'll have staging and production clusters, each with two nodes—control plane and worker. In production, I'll taint the control plane (my laptop) node to prevent scheduling. I will use a couple of lower-powered machines for the staging cluster, such as Raspberry Pis.


