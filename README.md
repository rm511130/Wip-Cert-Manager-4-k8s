# Wip-Cert-Manager-4-k8s
Cert Manager for K8s

- Let's start by executing the following command to create a CRD (Custom Resource Definition):

```
kubectl apply --validate=false -f https://raw.githubusercontent.com/jetstack/cert-manager/release-0.14/deploy/manifests/00-crds.yaml
```

- The command above should produce an output similar to the example shown below:

```
customresourcedefinition.apiextensions.k8s.io/certificaterequests.cert-manager.io created
customresourcedefinition.apiextensions.k8s.io/certificates.cert-manager.io created
customresourcedefinition.apiextensions.k8s.io/challenges.acme.cert-manager.io created
customresourcedefinition.apiextensions.k8s.io/clusterissuers.cert-manager.io created
customresourcedefinition.apiextensions.k8s.io/issuers.cert-manager.io created
customresourcedefinition.apiextensions.k8s.io/orders.acme.cert-manager.io created
```

- We'll be using the `cert-manager` namespace:

```
kubectl get ns  # if you don't see the "cert-manager" namespace, please create it using $ kubectl create ns cert-manager
```

- Add the Jetstack Helm repository and update your local Helm chart repo cache:

```
helm repo add jetstack https://charts.jetstack.io
helm repo update
```

- Let's install the cert-manager helm chart:

```
helm install cert-manager --namespace cert-manager --version v0.15.1 jetstack/cert-manager
```

- The command above should produce an output similar to the example shown below:

```
NAME: cert-manager
LAST DEPLOYED: Sun Jul  5 18:03:28 2020
NAMESPACE: cert-manager
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
cert-manager has been deployed successfully!

In order to begin issuing certificates, you will need to set up a ClusterIssuer
or Issuer resource (for example, by creating a 'letsencrypt-staging' issuer).

More information on the different types of issuers and how to configure them
can be found in our documentation:

https://cert-manager.io/docs/configuration/

For information on how to configure cert-manager to automatically provision
Certificates for Ingress resources, take a look at the `ingress-shim`
documentation:

https://cert-manager.io/docs/usage/ingress/
```

- Let's make sure you have the 3 required pods up and running. Execute the following command:

```
kubectl get pods -n cert-manager
```
- You should see something similar to the output shown below. If the pods are not running, wait a few seconds and check again.

```
NAME                                       READY   STATUS    RESTARTS   AGE
cert-manager-9b8969d86-9xmxr               1/1     Running   0          108s
cert-manager-cainjector-8545fdf87c-9rsbm   1/1     Running   0          108s
cert-manager-webhook-8c5db9fb6-cgdcq       1/1     Running   0          108s
```

- hmmmm    
