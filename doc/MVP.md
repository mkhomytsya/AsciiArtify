
---

## Демо

![Демо роботи ArgoCD](demo2.gif)


```bash
kubectl port-forward svc/ambassador -n demo 8088:80
```

```bash
curl -F 'image=@demo.png' localhost:8088/img/
```