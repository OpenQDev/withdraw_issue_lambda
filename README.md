# OpenQ API

This is the API middleware between the OpenQ frontend and the OpenQ backend.

## Stack
Package Manger: yarn
Containerization: Docker
Orchestration (Development): Docker Compose
Orchestration (Production): Kubernetes
CI/CD: CircleCI
Server: Node + Express

## Getting Started

### Environment Variables

`RPC_NODE`
The Ethereum RPC node to connect to. Defaults to `http://127.0.0.1:8545`

`OPENQ_ADDRESS`
Address of deployed `OpenQ` contract.

`WALLET_KEY`
OpenQ owner address which was used to deploy the OpenQ smart contract on whichever network you are connected to via `RPC_NODE`
This is necessary to call `onlyOwner` functions like withdraw.

### Starting OpenQAPI
Once you have the above environment variables configured to your needs, run:

```bash
docker compose up
```

### Stopping OpenQAPI

#### In the same terminal
```bash
Control + C
```
#### From a different terminal
```bash
docker compose down
```

## Deployments

### Environments
OpenQ API has three environments, listed below in order of maturity.

https://development.openq.dev
https://staging.openq.dev
https://production.staging.openq.dev

### CircleCI
OpenQ API runs a pipeline on CircleCI with any push 

The configuration for builds and deploys can be found at [./.circleci/config.yml](./.circleci/config.yml).

Pipeline runs can be watched here: [OpenQ API CircleCI Pipeline](https://app.circleci.com/pipelines/github/OpenQDev/OpenQ-API)

### Kubernetes
OpenQ API is orchestrated on Kubernetes.

The configuration can be found at [./k8s](./k8s).

Notably, the routing for our environment domains is also here, including SSL: [./k8s/ingress.yml](./k8s/ingress.yml).

SSL Certtificates were provided by Let's Encrypt certbot with the dns-0 challenge.