# INSTRUCTION.md

## 📦 Застосування Manifests

1. Створити namespace:
   ```bash
   kubectl apply -f .infrastructure/namespace.yml
   ```

2. Створити два pod'и ToDo застосунку:
   ```bash
   kubectl apply -f .infrastructure/todoapp-pod.yml
   ```

3. Створити pod з образом busyboxplus для тестування:
   ```bash
   kubectl apply -f .infrastructure/busybox.yml
   ```

4. Створити сервіс ClusterIP:
   ```bash
   kubectl apply -f .infrastructure/clusterip.yml
   ```

5. Створити сервіс NodePort:
   ```bash
   kubectl apply -f .infrastructure/nodeport.yml
   ```

## ✅ Перевірка готовності та активності

Переконайтесь, що обидва pod'и в `todoapp` namespace мають статус `Running` і `READY 1/1`:
```bash
kubectl get pods -n todoapp
```

## 🔍 Тестування з busybox (через ClusterIP)

1. Підключитися до контейнера busybox:
   ```bash
   kubectl exec -it busybox -n todoapp -- sh
   ```

2. Виконати curl-запит до сервісу:
   ```bash
   curl http://todoapp
   ```

## 🔌 Тестування через port-forward

1. Виконати port-forward для сервісу:
   ```bash
   kubectl port-forward service/todoapp 8000:80 -n todoapp
   ```

2. Перейти у браузері або через curl:
   ```
   http://localhost:8000
   ```

## 🌐 Тестування через NodePort

1. Дізнатись IP-адресу вузла (наприклад, для minikube):
   ```bash
   minikube ip
   ```

2. Відкрити у браузері:
   ```
   http://<NODE_IP>:30080
   ```

