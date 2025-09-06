# Manual de Instalación de Docker, Kubernetes y Minikube en Ubuntu Server 22.04

Este manual explica paso a paso cómo instalar Docker, Kubernetes y
Minikube en Ubuntu Server 22.04.\
Cada instrucción se acompaña de una breve explicación sobre su función.

------------------------------------------------------------------------

## ✅ Requisitos previos

-   Ubuntu Server 22.04 (actualizado).
-   Al menos 2 CPU, 2 GB de RAM y 20 GB de disco libre.
-   Conexión a Internet.
-   Acceso como usuario con privilegios de **sudo**.

------------------------------------------------------------------------

## 🔹 Paso 1: Actualizar lista de paquetes

``` bash
sudo apt-get update
```

Actualiza el índice de paquetes de Ubuntu para obtener las últimas
versiones disponibles.

------------------------------------------------------------------------

## 🔹 Paso 2: Instalar Docker

``` bash
sudo apt install docker.io -y
```

Instala Docker, el motor de contenedores necesario para Kubernetes y
Minikube.\
La opción `-y` acepta la instalación sin pedir confirmación.

------------------------------------------------------------------------

## 🔹 Paso 3: Habilitar Docker en el arranque

``` bash
sudo systemctl enable docker
```

Configura Docker para iniciarse automáticamente cada vez que arranque el
servidor.

------------------------------------------------------------------------

## 🔹 Paso 4: Verificar estado de Docker

``` bash
sudo systemctl status docker
```

Muestra si el servicio Docker está activo y funcionando.\
(Sal con `q` para cerrar la vista de estado).

------------------------------------------------------------------------

## 🔹 Paso 5: Configurar repositorio de Kubernetes

### 5.1 Agregar la clave GPG oficial

``` bash
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```

Descarga y guarda la clave GPG que asegura que los paquetes de
Kubernetes sean auténticos.

### 5.2 Agregar el repositorio a la lista de APT

``` bash
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

Agrega el repositorio oficial de Kubernetes para instalar `kubeadm`,
`kubelet` y `kubectl`.

------------------------------------------------------------------------

## 🔹 Paso 6: Actualizar lista de paquetes

``` bash
sudo apt update
```

Refresca la lista de paquetes, ahora incluyendo Kubernetes.

------------------------------------------------------------------------

## 🔹 Paso 7: Instalar herramientas de Kubernetes

``` bash
sudo apt install kubeadm kubelet kubectl
```

-   **kubeadm** → inicializa y administra clusters de Kubernetes.\
-   **kubelet** → agente que corre en cada nodo y maneja contenedores.\
-   **kubectl** → CLI para interactuar con el cluster.

------------------------------------------------------------------------

## 🔹 Paso 8: Verificar la instalación

``` bash
kubeadm version
```

Muestra la versión instalada de `kubeadm` para confirmar que todo quedó
correcto.

------------------------------------------------------------------------

## 🔹 Paso 9: Instalar Minikube

``` bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
```

Descarga e instala **Minikube**, la herramienta que permite correr
Kubernetes en un entorno local.

------------------------------------------------------------------------

## 🔹 Paso 10: Dar permisos al usuario actual para usar Docker

``` bash
sudo usermod -aG docker $USER && newgrp docker
```

Agrega al usuario actual al grupo `docker` para poder usar Docker sin
`sudo`.\
El comando `newgrp docker` actualiza la sesión con los nuevos permisos.

------------------------------------------------------------------------

## 🔹 Paso 11: Iniciar Minikube

``` bash
minikube start
```

Crea y arranca un cluster de Kubernetes local usando Docker como
backend.

------------------------------------------------------------------------

## 🎯 Resultado final

Si todos los pasos fueron correctos, tendrás un **cluster Kubernetes
local funcionando en Minikube**, listo para practicar despliegues y
probar aplicaciones.

Puedes comprobarlo con:

``` bash
kubectl get nodes
kubectl get pods -A
```
