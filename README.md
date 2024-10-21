# SaaS Microservices Guide

Welcome to the guide for setting up a multi-tenant SaaS using microservices architecture! This guide will help you deploy and run the following microservices:
- [AuthoSaaS](https://github.com/ThatLadyDev/autho-saas)
- [BillifySaaS](https://github.com/ThatLadyDev/billify-saas)
- [TenantrixSaaS](https://github.com/ThatLadyDev/tenantrix-saas)
- [NotifiSaaS](https://github.com/ThatLadyDev/notifi-saas)

## Prerequisites

Before starting, ensure you have the following installed:
- Docker
- Docker Compose (for local setup)
- Kubernetes CLI (`kubectl`)
- Azure CLI (for deploying to AKS)

## Local Setup

Follow the instructions in [local-setup.md](local-setup.md) to run all services locally.

## Production Setup

Check [production-setup.md](production-setup.md) for steps on deploying the microservices to a Kubernetes cluster using Azure AKS.

## Architecture Overview

For more details on how the microservices are designed and interact with each other, check out the [architecture overview](architecture-overview.md).
