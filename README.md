# Db2-on-OpenShift
Db2 on OpenShift 4.x

## Run Db2 Community Edition on OpenShift on IBM Cloud.

This deployemnt recipe uses publicly available Db2 community edition from Docker Hub. The deployment will create a Statefulset using Block storage. This solution has been tested on IBM Cloud's OpenShift 4.3/stable. 

```
oc new-project db2b
oc create serviceaccount db2b
oc adm policy add-scc-to-user privileged -n db2b -z db2b
```

## Deploy
Change your zone/region before deploying. 
```
oc create -f deploydb2.yaml
```
Use NodePort to connect to your database. Access container: `oc rsh pod/db2-0` Change user: `su - db2inst1`. 
