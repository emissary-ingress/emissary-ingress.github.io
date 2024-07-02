---
    Title: Migrate to Emissary $versionTwoX$
    description: "Instructions for how to upgrade Emissary to $versionTwoX$. Transfer your current configuration of Ambassador Edge Stack or Emissary to $versionTwoX$."
---
import Alert from '@material-ui/lab/Alert';

# Upgrading Emissary $versionTwoX$ with a separate cluster

You can upgrade from any version of Ambassador Edge Stack or Emissary to
any version of either by installing the new version in a new Kubernetes cluster,
then copying over configuration as needed. This is the way to be absolutely
certain that each installation cannot affect the other: it is extremely safe,
but is also significantly more effort.

For example, to upgrade from some other version of Ambassador Edge Stack or
Emissary to Emissary $versionTwoX$:

1. Install Emissary $versionTwoX$ in a completely new cluster.

2. **Create `Listener`s for Emissary $versionTwoX$.**

   When Emissary $versionTwoX$ starts, it will not have any `Listener`s, and it will not
   create any. You must create `Listener` resources by hand, or Emissary $versionTwoX$
   will not listen on any ports.

3. Copy the entire configuration from the Emissary 1.X cluster to the Emissary
   $versionTwoX$ cluster. This is most simply done with `kubectl get -o yaml | kubectl apply -f -`.

   This will create `getambassador.io/v2` resources in the Emissary $versionTwoX$ cluster.
   Emissary $versionTwoX$ will translate them internally to `getambassador.io/v3alpha1`
   resources.

4. Each Emissary instance has its own cluster, so you can test the new
   instance without disrupting traffic to the existing instance.

5. If you need to make changes, you can change the `getambassador.io/v2` resource, or convert the
   resource you're changing to `getambassador.io/v3alpha1` by using `kubectl edit`.

6. Once everything is working with both versions, transfer incoming traffic to the Emissary
   $versionTwoX$ cluster.
