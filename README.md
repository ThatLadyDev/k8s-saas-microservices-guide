# SaaS Microservices Guide

Welcome to the guide for setting up a multi-tenant SaaS using microservices architecture! This guide will help you deploy and run the following microservices:
- [Authentication Service](https://github.com/ThatLadyDev/autho-saas)
- [Billing Service](https://github.com/ThatLadyDev/billify-saas)
- [Notification Service](https://github.com/ThatLadyDev/notifi-saas)
- [API Middleware](https://github.com/ThatLadyDev/saas-api-middleware)

## Prerequisites

Before starting, ensure you have the following installed:
- Docker Desktop
- Docker Compose (for local setup)
- Kubernetes CLI - for production setup (`kubectl`)

## Local Setup

Follow the instructions in [local-setup.md](local-setup.md) to run all services locally.

## Production Setup

Check [production-setup.md](production-setup.md) for steps on deploying the microservices to a Kubernetes cluster using Azure AKS.

## Architecture Overview

For more details on how the microservices are designed and interact with each other, check out the [architecture overview](architecture-overview.md).
