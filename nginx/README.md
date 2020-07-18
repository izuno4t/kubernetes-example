# Kubernetes で Nginx のコンテナを起動

## nginx をデプロイする

- Deployment のマニフェストファイルを Kubernetes に追加
  
```sh
$ kubectl apply -f deployment.yaml
deployment.apps/nginx-deployment created
```

- 追加直後のPodの状態
  
```sh
$ kubectl get pods
NAME                               READY   STATUS              RESTARTS   AGE
nginx-deployment-9bcf74994-9t6k5   0/1     ContainerCreating   0          23s
nginx-deployment-9bcf74994-n2xns   0/1     ContainerCreating   0          23s
nginx-deployment-9bcf74994-wzzpl   0/1     ContainerCreating   0          23s
```

- Podが起動語
  
```sh
$ kubectl get pods
NAME                               READY   STATUS    RESTARTS   AGE
nginx-deployment-9bcf74994-9t6k5   1/1     Running   0          116s
nginx-deployment-9bcf74994-n2xns   1/1     Running   0          116s
nginx-deployment-9bcf74994-
```

## 外部からのアクセスを可能にするため Service を追加

- Service のマニフェストファイルを Kubernetes に追加

```sh
$ kubectl apply -f service.yaml
service/nginx-deployment created
```

- Service の状態

```sh
$ kubectl get service
NAME               TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
kubernetes         ClusterIP      10.96.0.1        <none>        443/TCP          45m
nginx-deployment   LoadBalancer   10.109.227.141   localhost     8080:32561/TCP   23s
```

## nginx をアンデプロイする

- Service を削除

```sh
$ kubectl delete -f service.yaml
service "nginx-deployment" deleted
```

- Service の状態

```sh
miu:nginx izuno$ kubectl get service
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   55m
```

- Pod を削除

```sh
$ kubectl delete -f deployment.yaml
deployment.apps "nginx-deployment" deleted
```
- Pod を削除後の状態

```sh
$ kubectl get pods
No resources found in default namespace.
```
