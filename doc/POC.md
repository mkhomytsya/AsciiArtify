# Proof of Concept: Розгортання ArgoCD для AsciiArtify

## Опис

Цей PoC демонструє розгортання GitOps-системи ArgoCD у Kubernetes-кластері, створеному за допомогою k3d. ArgoCD забезпечує автоматизацію розгортання застосунків із git-репозиторію та надає зручний графічний інтерфейс для керування.

---

## Кроки розгортання

### 1. Створення Kubernetes-кластеру

```bash
k3d cluster create asciiartify-demo --agents 2
```
- Створюється кластер із 2-ма воркерами (агентами).

---

### 2. Встановлення ArgoCD

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
- Створюється окремий namespace для ArgoCD.
- Встановлюються всі необхідні ресурси ArgoCD.

---

### 3. Перевірка ресурсів

```bash
kubectl get all -n argocd
```
- Переконайтесь, що всі pod-и та сервіси ArgoCD працюють.

---

### 4. Доступ до графічного інтерфейсу ArgoCD

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
- Відкриває доступ до веб-інтерфейсу ArgoCD на локальному порту 8080.

Відкрийте у браузері: [https://127.0.0.1:8080](https://127.0.0.1:8080)

---

### 5. Отримання пароля адміністратора

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo
```
- Логін: **admin**
- Пароль: (значення з команди вище)

---

## Демо

![Демо роботи ArgoCD](demo1.gif)
