# PHP MySQL Kubernetes Project

Este proyecto muestra cómo desplegar una aplicación PHP con MySQL en Kubernetes usando Minikube.

## Estructura del Proyecto

```plaintext
.
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

cd "C:\Users\CursosTardes\Documents\nginx\Ejer php, mysql y docker\webapp"
minikube start
docker context use default
eval $(minikube docker-env)
minikube ip
minikube addons enable metrics-server

```plaintext
cd "C:\Users\CursosTardes\Documents\nginx\Ejer php, mysql y docker\webapp"
minikube start
docker context use default
eval $(minikube docker-env)
minikube ip
minikube addons enable metrics-server
```

<h2>Construcción de la Imagen Docker</h2>
Construye la imagen Docker de la aplicación PHP:
```plaintext
docker build --tag $(minikube ip):5000/php-webserver .
```
<h2>Despliegue en Kubernetes</h2>
Aplica las configuraciones de Kubernetes:
```plaintext
kubectl apply -k ./
```
<h2>Despliegue en Kubernetes</h2>
Expón el servicio en Minikube:
```plaintext
minikube service "servicios"
```
<h2>Configuración de la Base de Datos</h2>
Crea la tabla necesaria en la base de datos MySQL usando el siguiente SQL:
```plaintext
CREATE TABLE IF NOT EXISTS form_data (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    message TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
<h2>Detalles del Proyecto</h2>
Dockerfile
```plaintext
# Use an official PHP Apache runtime
FROM php:8.2-apache

# Enable Apache modules
RUN a2enmod rewrite

# Install MySQLi extension and other required extensions
RUN apt-get update \
    && apt-get install -y libpq-dev \
    && docker-php-ext-install pdo pdo_pgsql mysqli

# Set the working directory to /var/www/html
WORKDIR /var/www/html

# Copy the PHP code file in /html into the container at /var/www/html
COPY ./html .

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Install project dependencies
RUN composer install --no-dev --prefer-dist --optimize-autoloader

# Expose port 80
EXPOSE 80

```
