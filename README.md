# Devoxx Workshop requirements

In this workshop we are going to use a lightweigh k8s distribution: K3d/k3s.

[K3d](https://github.com/rancher/k3d) is a wrapper to easily launch a Kubernetes cluster using the very lightweight [Rancher k3s distribution](https://github.com/rancher/k3s).

It fits particularly well in a development environnement when you want to test your application with the k8s manifests in real condition or as an administrator to validate behaviours or evaluate new k8s features.

For more information see https://medium.com/@yannalbou/k3d-k3s-k8s-perfect-match-for-dev-and-testing-896c8953acc0

## Prerequis

* Docker:
    * Docker Desktop on Mac: https://docs.docker.com/docker-for-mac/install/
    * Docker Desktop on Windows: https://docs.docker.com/docker-for-windows/install/
    * Other distributions https://docs.docker.com/install/

* kubectl: https://kubernetes.io/fr/docs/tasks/tools/install-kubectl/

* Vault: 
    * https://www.vaultproject.io/downloads/
    * After downloading Vault, unzip the package. Vault runs as a single binary named vault.
    * The final step is to make sure that the vault binary is available on the PATH
    * autocompletion : 
        ```
        vault -autocomplete-install
        exec $SHELL
        ```

## K3D/K3S Installation

* linux:
    ```
    wget: wget -q -O - https://raw.githubusercontent.com/rancher/k3d/master/install.sh | bash
    curl: curl -s https://raw.githubusercontent.com/rancher/k3d/master/install.sh | bash
    ```
* MacOS: 
    ```
    brew install k3d
    ```
* Other (Windows): download directly the binary of latest release: https://github.com/rancher/k3d/releases


# Configure a kubernetes cluster with 2 worker nodes

For this workshop we will use a kubernetes with 1 master and 3 worker nodes:

```
k3d create --name vault --api-port 6552 --publish 8280:80 --workers 3
export KUBECONFIG="$(k3d get-kubeconfig --name='vault')"
```

check everything works as expected:
```
kubectl cluster-info

kubectl get nodes
# all nodes should be in a Ready state

kubectl get pods --all-namespaces
# all pods should be in a Running status
```
