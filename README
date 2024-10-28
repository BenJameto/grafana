
# Instalación de Grafana y Prometheus en Minikube mediante Helm

Autor: Benjamin Martinez para Zulunity

## Instalación de Grafana

Este documento proporciona los pasos para desplegar Grafana y Prometheus en un clúster de Minikube utilizando Helm.

1. **Paso 1: Agregar el repositorio de Helm de Grafana**

    Ejecuta el siguiente comando para agregar el repositorio oficial de Grafana:

    ```bash
    helm repo add grafana https://grafana.github.io/helm-charts
    ```

2. **Paso 2: Actualizar los repositorios de Helm**

    Actualiza los repositorios de Helm para asegurarte de tener la última versión de los charts:

    ```bash
    helm repo update
    ```

3. **Paso 3: Crear un Namespace para Grafana**

    Crea un namespace específico para Grafana:

    ```bash
    kubectl create namespace monitoring
    ```

4. **Paso 4: Desplegar Grafana en Minikube**

    Ejecuta el siguiente comando para desplegar Grafana en el namespace `monitoring`:

    ```bash
    helm install grafana grafana/grafana --namespace monitoring
    ```

5. **Paso 5: Verificar el Estado del Despliegue**

    Puedes verificar el estado del despliegue de Grafana con el siguiente comando:

    ```bash
    kubectl get pods -n monitoring
    ```

6. **Paso 6: Exponer Grafana en Minikube**

    Si deseas exponer Grafana a través de un puerto en Minikube, ejecuta:

    ```bash
    kubectl port-forward svc/grafana 3000:80 -n monitoring
    ```

    Luego, puedes acceder a Grafana en tu navegador en [http://localhost:3000](http://localhost:3000).

## Instalación de Prometheus

1. **Paso 1: Agregar el repositorio de Helm de Prometheus**

    Para instalar Prometheus, primero agrega el repositorio oficial de Helm de Prometheus:

    ```bash
    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    ```

2. **Paso 2: Actualizar los repositorios de Helm**

    Ejecuta el siguiente comando para asegurarte de que los repositorios de Helm estén actualizados:

    ```bash
    helm repo update
    ```

3. **Paso 3: Crear un Namespace para Prometheus**

    Usaremos el mismo namespace `monitoring` creado para Grafana:

    ```bash
    kubectl create namespace monitoring
    ```

4. **Paso 4: Desplegar Prometheus en Minikube**

    Para desplegar Prometheus, usa el siguiente comando en el namespace `monitoring`:

    ```bash
    helm install prometheus prometheus-community/prometheus --namespace monitoring
    ```

5. **Paso 5: Verificar el Estado del Despliegue**

    Puedes verificar el estado de Prometheus con el siguiente comando:

    ```bash
    kubectl get pods -n monitoring
    ```

## Consultas de Monitoreo en Prometheus

Esta sección proporciona algunas consultas útiles para monitorear el uso de recursos en el clúster, como CPU, memoria y el estado de los pods.

- **Uso de CPU por Nodo**
  
    ```prometheus
    sum(rate(container_cpu_usage_seconds_total{job="kubelet", image!="", container!="POD"}[5m])) by (node)
    ```

- **Memoria Usada por Nodo**
  
    ```prometheus
    sum(container_memory_usage_bytes{job="kubelet", image!=""}) by (node)
    ```

- **Uso de CPU por Pod**
  
    ```prometheus
    sum(rate(container_cpu_usage_seconds_total{namespace="<namespace>"}[5m])) by (pod)
    ```

- **Memoria Usada por Pod**
  
    ```prometheus
    sum(container_memory_usage_bytes{namespace="<namespace>"}) by (pod)
    ```

- **Estatus del Pod**
  
    ```prometheus
    count(kube_pod_status_phase{namespace="<namespace>", phase="Running"}) by (pod)
    ```

- **Número de Pods en un Namespace**
  
    ```prometheus
    count(kube_pod_info{namespace="<namespace>"}) by (pod)
    ```

- **Uso de Almacenamiento de Persistent Volumes**
  
    ```prometheus
    kubelet_volume_stats_used_bytes{namespace="<namespace>"}
    ```

- **Pods en Estado CrashLoopBackOff**
  
    ```prometheus
    count(kube_pod_container_status_restarts_total{namespace="<namespace>", reason="CrashLoopBackOff"}) by (pod)
    ```

**Nota**: Reemplaza `<namespace>` con el nombre específico de tu namespace y `<deployment>` con el nombre de tu despliegue al usar estas consultas.
