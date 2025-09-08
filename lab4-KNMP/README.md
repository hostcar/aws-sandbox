
Crear componentes

``` bash
kubectl apply -f 01-namespace.yaml
kubectl apply -f 02-mysql-secret-db.yaml
kubectl apply -f 03-persistent-volume.yaml
kubectl apply -f 04-persistent-volume-claim.yaml
kubectl apply -f 05-deployment-mysql.yaml
kubectl apply -f 06-service-mysql.yaml
kubectl apply -f 07-deployment-phpmyadmin.yaml
kubectl apply -f 08-service-phpmyadmin.yaml
kubectl apply -f 09-datadog-agent.yaml
```

Eliminar componentes

``` bash
kubectl delete -f 08-service-phpmyadmin.yaml
kubectl delete -f 07-deployment-phpmyadmin.yaml
kubectl delete -f 06-service-mysql.yaml
kubectl delete -f 05-deployment-mysql.yaml
kubectl delete -f 04-persistent-volume-claim.yaml
kubectl delete -f 03-persistent-volume.yaml
kubectl delete -f 02-mysql-secret-db.yaml
kubectl delete -f 01-namespace.yaml
```


``` bash
kubectl get no,pods,svc,ing -n knmp
```