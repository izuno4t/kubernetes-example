# Kubernetes で Nginx のコンテナを起動

- DeploymentのマニフェストをK8sに追加
  
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
