kubectl create namespace mongodb
kubectl apply -f mongo-statefulset.yaml
kubectl apply -f mongodb-service.yaml

kubectl get statefulsets -n mongodb
kubectl get pods -n mongodb
kubectl get svc -n mongodb
kubectl get pvc -n mongodb
kubectl exec -it mongodb-0 -n mongodb -- mongosh
	test> show dbs;
	admin   40.00 KiB
	config  60.00 KiB
	local   40.00 KiB
	test> use mydb; 
	switched to db mydb
	mydb> db.createCollection("mycollection");
	{ ok: 1 }
  mydb> 
controlplane $ kubectl get all -n mongodb
NAME            READY   STATUS    RESTARTS   AGE
pod/mongodb-0   1/1     Running   0          19m
pod/mongodb-1   1/1     Running   0          18m
pod/mongodb-2   1/1     Running   0          18m

NAME              TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)     AGE
service/mongodb   ClusterIP   None         <none>        27017/TCP   38m

NAME                       READY   AGE
statefulset.apps/mongodb   3/3     19m
controlplane $ 
