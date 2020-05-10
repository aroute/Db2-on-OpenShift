# Db2-on-OpenShift
Db2 on OpenShift 4.x

## Run Db2 Community Edition on OpenShift on IBM Cloud.

This deployemnt recipe uses publicly available Db2 community edition from Docker Hub. The deployment will create a Statefulset using Block storage. This solution has been tested on IBM Cloud's OpenShift 3.11 and 4.3/stable. 

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
Use NodePort to connect to your database from outside. 

Access container: `oc rsh pod/db2-0` Change user: `su - db2inst1`. 

A pre-installed database "books" can be tested by following these steps:
```
oc rsh pod/db2-0

su - db2inst1

db2 list database directory

db2 connect to books

curl -o create.sql https://raw.githubusercontent.com/aroute/db2books/master/create.sql
curl -o data.sql https://raw.githubusercontent.com/aroute/db2books/master/data.sql
curl -o drop.sql https://raw.githubusercontent.com/aroute/db2books/master/drop.sql

db2 -stvf create.sql > /dev/null
db2 -stvf data.sql > /dev/null

db2

select COUNT(*) author_count FROM authors;
list tables
SELECT COUNT(*) FROM books;
quit
```
