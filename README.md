# stocktrader-gitops

## Deploy OCS
  
From the `ocs` folder
* Ensure you have at least 3 nodes with 16 vcpu and 32GB of Memory
* Label three nodes using:
```
oc label node <<node-name>> cluster.ocs.openshift.io/openshift-storage=''
``` 
* Apply ibm-ocs-configmap.yaml -- Creates the OCS namespace and a config map specific to IBM Cloud config. 
* Apply ocs-namespace.yaml -- Required if not IBM Cloud
* Apply ocs-operator-group.yaml, ocs-subscription.yaml, ocs-storage-cluster.yaml

Underlying storage class set to **ibmc-vpc-block-metro-retain-10iops-tier**

## Deploy DB2 Operator

From the `db2` folder...

* Apply db2-namespace.yaml 
* Create your [entitlement key](https://myibm.ibm.com/products-services/containerlibrary) using this command:
```
oc create secret docker-registry ibm-entitlement-key \
    --docker-username=cp \
    --docker-password=<<myEntitlementKey>> \
    --docker-server=cp.icr.io \
    --namespace=db2
 ```
 * Apply db2-catalog.yaml, db2-scc.yaml, db2-operator-group.yaml, db2-subscription.yaml

## Create the Trader DB

From the `trader-db`

* Apply trader-db2.yaml
