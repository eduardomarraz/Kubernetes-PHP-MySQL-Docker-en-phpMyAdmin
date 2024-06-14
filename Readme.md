# PHP MySQL Kubernetes Project

Este proyecto muestra cómo desplegar una aplicación PHP con MySQL en Kubernetes usando Minikube.

## Estructura del Proyecto

```plaintext
.
|-- Readme.md
|-- composer.json
|-- kustomization.yaml
|-- mysql
|   |-- deployment-mysql.yaml
|   |-- kustomization.yaml
|   |-- pv-mysql.yaml
|   |-- pvc-mysql.yaml
|   `-- service-mysql.yaml
|-- phpmyadmin
|   |-- deployment-phpmyadmin.yaml
|   |-- kustomization.yaml
|   `-- service-phpmyadmin.yaml
`-- webapp
    |-- Dockerfile
    |-- deployment-webapp.yaml
    |-- html
    |   |-- index.html
    |   |-- submit.php
    |   `-- vendor
    |       `-- autoload.php
    |-- kustomization.yaml
    `-- service-webapp.yaml

```

<h2>Prerrequisitos</h2>

<h3>Docker</h3>
<h3>Minikube</h3>
<h3>kubectl</h3>
<h3>Composer</h3>

<h2>Configuración del Entorno</h2>

```plaintext
cd "C:\Users\CursosTardes\Documents\nginx\Ejer php, mysql y docker\webapp"
minikube start
docker context use default
eval $(minikube docker-env)
minikube ip (Sustituir el deployment-webapp.yaml con la ip que sale aqui)
minikube addons enable metrics-server
docker build --tag $(minikube ip):5000/php-webserver .
kubectl apply -k ./
minikube service "servicios" (Creas los servicio)
```
