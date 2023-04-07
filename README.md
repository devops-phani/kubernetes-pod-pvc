# kubernetes-pod-pvc

```
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/opt/old"
        name: old
      - mountPath: "/opt/new"
        name: new
  volumes:
    - name: old
      persistentVolumeClaim:
        claimName: old
    - name: new
      persistentVolumeClaim:
        claimName: new
```

```
kubectl get pod mypod
```

```
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  imagePullSecrets:
  - name: docker-hub-credentials
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/opt/old"
        name: old
      - mountPath: "/opt/new"
        name: new
  volumes:
    - name: old
      persistentVolumeClaim:
        claimName: old
    - name: new
      persistentVolumeClaim:
        claimName: new
  tolerations:
  - effect: NoSchedule
    operator: Exists
```  
