# Db2-on-OpenShift
Db2 on OpenShift 4.x

## Run Db2 Community Edition on OpenShift on IBM Cloud.

```
oc new-project db2b
oc create serviceaccount db2b
oc adm policy add-scc-to-user privileged -n db2b -z db2b
```
```
oc create -f deploydb2.yaml
```
