gcloud beta container clusters create "demo" --project "mkhomytsia" --zone "europe-west3-a" --machine-type "e2-medium" --disk-type "pd-standard" --disk-size "100GB"

gcloud container clusters get-credentials "demo" --project "mkhomytsia" --zone "europe-west3-a"

kubectl create deployment hello --image=gcr.io/google-samples/hello-app:1.0

kubectl expose deployment hello --type=LoadBalancer --port=80 --target-port=8080

kubectl get svc -w
kubectl get svc -o wide

(Чекайте, поки в EXTERNAL-IP з'явиться адреса. Це може зайняти 1-2 хвилини в GCP).
Налаштування Uptime Robot:
Створіть монітор (Keyword).
URL: http://34.89.184.175
Keyword: Version: 1.0.0
Результат: Монітор має стати зеленим.


kubectl scale deployment hello --replicas=3

kubectl create deployment hello-v2 --image=gcr.io/google-samples/hello-app:2.0
kubectl get pods --show-labels
kubectl get pods -l app=hello


kubectl label po --all run=hello

kubectl edit svc hello

change 
  selector:
      run: hello

kubectl label po --all run=hello


for i in {1..10}; do curl -s 34.89.184.175 | grep "Version"; done


kubectl scale deployment hello --replicas=0
kubectl scale deployment hello-v2 --replicas=3


kubectl delete service hello
kubectl delete deployment hello
kubectl delete deployment hello-v2