
# Tarea 6 - Deployment y Service en Kubernetes

- **Curso:** Docker & Kubernetes - Clase 6
- **Estudiante:** Ronald Choque Fuentes



**Opción 1: Nginx (Más Simple)**

- Imagen: `nginx:alpine`
- Puedes usar HTML personalizado (opcional)

## Parte 2: Requisitos del Deployment
[Deployment](deployment.yaml)
```bash
kubectl apply -f deployment.yaml

```
## Parte 3: Requisitos del Service
[Service](service.yaml)
```bash
kubectl apply -f service.yaml

```
## Parte 5: Desplegar y Probar
```bash
minikube service webapp-service --url

```
![alt text](/screenshots/image-1.png)
![alt text](/screenshots/image.png)

## deploy the index.html

1. create a web config.

```bash
kubectl create configmap mi-index-html --from-file="html/index.html"

```

2. update the deployment.yaml
```bash

    spec:
      containers:
      - name: nginx
        image: nginx:alpine
        ports:
        - containerPort: 80
        volumeMounts:
        - name: nginx-index-file
          mountPath: /usr/share/nginx/html/
      volumes:
      - name: nginx-index-file
        configMap:
          name: mi-index-html

```

3. redeploy the pods
```bash
kubectl apply -f deployment.yaml

```
4.  get the url of the service and check in the browser
```bash
minikube service webapp-service --url
```
![alt text](/screenshots/image-2.png)