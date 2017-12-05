## Introduction

This chart bootstraps a Kong deployment on a [Kubernetes](http://kubernetes.io)
cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.4+ with Beta APIs enabled
- PV provisioner support in the underlying infrastructure (Only when persisting data)
- [Helm](https://docs.helm.sh/using_helm/#quickstart-guide) is installed and initialized

## Installing the Chart

1. Clone or download the repo and change the working directory to
`./kong-dist-kubernetes/charts/`

```bash
$ git clone git@github.com:Kong/kong-dist-kubernetes.git
$ cd ./kong-dist-kubernetes/charts
```

2. Install the Kong chart
```bash
$ helm install --name <release_name> kong
```

The command deploys Kong and backing database(if enabled) on the Kubernetes cluster
using the default configuration in the `./kong/values.yaml` file. Update the
parameter's value in file to change default behaviour.

The following tables lists the configurable parameters of the Kong chart and
their default values. For [`Cassandra`](./charts/cassandra/README.md) and
[`PostgreSQL`](./charts/postgresql/README.md), check corresponding chart README.md

| Parameter                  | Description                                     | Default                          |
| -----------------------------------    | --------------------------------------------------------------------   | -------------------   |
| kong.image                             | Kong image and version                                                 | `kong:latest`         |
| kong.nameOverride                      | Kong app name, overrides the auto generated app name                   | ``                    |
| kong.kongInstanceCount                 | Kong instance count                                                    | `1`                   |
| kong.admin.servicePort                 | TCP port on which Kong Admin Service is exposed                        | `8001`                |
| kong.admin.serviceSSLPort              | Secure TCP port on which Kong Admin                                    | `8444`                |
| kong.admin.containerPort               | TCP port on which Kong app listen to for admin traffic                 | `8001`                |
| kong.admin.containerSSLPort            | Secure TCP port on which Kong app listen to for Admin traffic          | `8444`                |
| kong.admin.type                        | k8s service type exposing ports, e.g. `NodePort`                       | `NodePort`            |
| kong.admin.loadBalancerIP              | Static IP address                                                      | `null`                |
| kong.proxy.useTLS                      | Secure Admin traffic                                                   | `true`                |
| kong.proxy.servicePort                 | TCP port on which Kong Proxy Service is exposed                        | `8000`                |
| kong.proxy.serviceSSLPort              | Secure TCP port on which Kong Proxy Service is exposed                 | `8443`                |
| kong.proxy.containerPort               | TCP port on which Kong app listen to for Proxy traffic                 | `8000`                |
| kong.proxy.containerSSLPort            | Secure TCP port on which Kong app listen to for Proxy traffic          | `8443`                |
| kong.proxy.type                        | k8s service type exposing ports, e.g. `NodePort`                       | `NodePort`            |
| kong.proxy.loadBalancerIP              | Static IP address                                                      | `null`                |
| kong.proxy.useTLS                      | Secure Proxy traffic                                                   | `true`                |
| kong.logLevel                          | Kong log level                                                         | `debug`               |
| kong.database.useCassandra             | set it to `true` for Cassanddra as Kong DB                             | `false`               |
| kong.database.postgres.username        | Postgres username                                                      | `kong`                |
| kong.database.postgres.database        | Postgres database name                                                 | `kong`                |
| kong.database.postgres.password        | Postgres database password                                             | `kong`                |
| kong.database.postgres.host            | Postgres database host, required if you using own database             | ``                    |
| kong.database.postgres.port            | Postgres database port                                                 | `5432`                |
| kong.database.cassandra.contactPoints  | Cassandra contact points, required if you using own database           | ``                    |
| kong.database.cassandra.port           | Cassandra query port                                                   | `9042`                |
| kong.database.cassandra.keyspace       | Cassandra keyspace                                                     | `kong`                |
| kong.database.cassandra.replication    | Replication factor for the Kong keyspace                               | `2`                   |
| kong.customConfig                      | Additional [Kong configurations](https://getkong.org/docs/latest/configuration/) |             |


## Uninstalling the Chart

To uninstall/delete the deployment:

```bash
$ helm delete <release_name>
```

The command removes all the Kubernetes components associated with the Kong chart
and deletes the release.


Note: This chart is not tested for production use.






