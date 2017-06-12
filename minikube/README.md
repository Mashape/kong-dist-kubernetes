# [KONG][website-url] :heavy_plus_sign: [Kubernetes Deployment](http://kubernetes.io/)

[![Website][website-badge]][website-url]
[![Documentation][documentation-badge]][documentation-url]
[![Mailing List][mailing-list-badge]][mailing-list-url]
[![Gitter Badge][gitter-badge]][gitter-url]

[![][kong-logo]][website-url]

Kong can easily be provisioned to Kubernetes cluster using the following steps:

1. **Initial setup**
  
    Download or clone the following repo:

    ```bash
    $ git clone git@github.com:Mashape/kong-dist-kubernetes.git
    $ cd kong-dist-kubernetes/minikube
    ```
    
    Skip to step 3 if you have already provisioned a minikube cluster.

2.  **Deploy Kubernetes via Minikube**
    
    You need [minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/) and
    [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
    command-line tools installed and set up to run deployment commands.

    Using the `minikube` command, deploy a Kubernetes cluster.

    ```bash
    $ minikube start
    ```

    By now, you have provisioned a Kubernetes managed cluster locally.


3. **Deploy a Kong supported database**
  
    Before deploying Kong, you need to provision a Cassandra or PostgreSQL pod.

    For Cassandra, use the `cassandra.yaml` file from this repo to deploy a
    Cassandra `Service` and a `ReplicationController` in the cluster:  

    ```bash
    $ kubectl create -f cassandra.yaml
    ```
    
    For PostgreSQL, use the `postgres.yaml` file from the kong-dist-kubernetes 
    repo to deploy a PostgreSQL `Service` and a `ReplicationController` in the
    cluster:

    ```bash
    $ kubectl create -f postgres.yaml
    ```

4. **Deploy Kong**

    Using the `kong_<postgres|cassandra>.yaml` file from this repo, deploy
    a Kong `Service` and a `Deployment` to the cluster created in the last step:
    
    ```bash
    $ kubectl create -f kong_<postgres|cassandra>.yaml
    ```

5. **Verify your deployments**

    You can now see the resources that have been deployed using `kubectl`:

    ```bash
    $ kubectl get rc
    $ kubectl get deployment
    $ kubectl get pods
    $ kubectl get services
    $ kubectl get logs <pod-name>
    ```

    Once the kong-admin and kong-proxy pods are started, you
    can test Kong by making the following requests:

    ```bash
    $ curl $(minikube service --url kong-admin)
    $ curl $(minikube service --url kong-proxy|head -n1)
    ```

    It may take up to 3 minutes for all services to come up.

6. **Using Kong**

    Quickly learn how to use Kong with the 
    [5-minute Quickstart](https://getkong.org/docs/latest/getting-started/quickstart/).

## Important Note

When deploying into a Kubernetes cluster with Deployment Manager, it is
important to be aware that deleting `ReplicationController` Kubernetes objects
**does not delete its underlying pods**, and it is your responisibility to
manage the destruction of these resources when deleting or updating a
`ReplicationController` in your configuration.


## Enterprise Support

Support, Demo, Training, API Certifications and Consulting available at http://getkong.org/enterprise.

[kong-logo]: http://i.imgur.com/4jyQQAZ.png
[website-url]: https://getkong.org/
[website-badge]: https://img.shields.io/badge/GETKong.org-Learn%20More-43bf58.svg
[documentation-url]: https://getkong.org/docs/
[documentation-badge]: https://img.shields.io/badge/Documentation-Read%20Online-green.svg
[gitter-url]: https://gitter.im/Mashape/kong
[gitter-badge]: https://img.shields.io/badge/Gitter-Join%20Chat-blue.svg
[mailing-list-badge]: https://img.shields.io/badge/Email-Join%20Mailing%20List-blue.svg
[mailing-list-url]: https://groups.google.com/forum/#!forum/konglayer

