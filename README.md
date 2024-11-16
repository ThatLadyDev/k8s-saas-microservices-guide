<p align="center"><a href="https://devfestlagos.com" target="_blank"><img src="https://devfestlagos.com/images/svg/devfest--logo.svg" width="400" alt="Devfest Lagos Logo"></a></p>

# Devfest Lagos 2024 Codelab - SaaS Microservices Guide

Welcome to the guide for setting up the multi-tenant SaaS I built for my codelab at Google DevFest Lagos 2024, titled ‘Building a Multi-Tenant SaaS with Microservices on Kubernetes,’ using a microservices architecture.

<p><a href="https://x.com/gdglagos/status/1853799346455617766/photo/1" target="_blank"><img src="https://github.com/user-attachments/assets/53267a1c-d84d-47a6-a3a2-1f23174f50f6" width="400" alt="My Codelab"></a></p>

This guide will help you deploy and run the microservices both locally and in a production environment (Kubernetes). The multi-tenant SaaS consists of a total of six services, working together to ensure the SaaS operates as expected as shown below.

![image](https://github.com/user-attachments/assets/c9a2945c-f5c7-4119-9c8e-be12b92bb7ea)

- [Authentication Service](https://github.com/ThatLadyDev/autho-saas)
- [Billing Service](https://github.com/ThatLadyDev/billify-saas)
- [Notification Service](https://github.com/ThatLadyDev/notifi-saas)
- [API Middleware](https://github.com/ThatLadyDev/saas-api-middleware)
- Mailing Service
- Database Service (mysql)

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
