# Helm Chart - demo-chart

Este chart despliega una aplicación **NGINX** parametrizada en un clúster de Kubernetes, con soporte para Ingress utilizando el host `demo.local`.

---

## 📦 Requisitos

* Kubernetes (Docker Desktop o Minikube)
* Helm 3 instalado
* Ingress Controller (`ingress-nginx`) activo en el clúster

---

## 🚀 Instalación

1. **Clonar este repositorio:**

   ```bash
   git clone https://github.com/<tu-usuario>/demo-chart.git
   cd demo-chart
   ```

2. **Instalar el chart:**

   ```bash
   helm install demo-nginx ./demo-chart
   ```

3. **Validar el despliegue:**

   ```bash
   kubectl get pods
   kubectl get svc
   kubectl get ingress
   ```

4. **Editar el archivo `hosts` en Windows:**

   ```text
   127.0.0.1 demo.local
   ```

5. **Acceder a la aplicación:**

   ```text
   http://demo.local
   ```

---

## ⚙️ Valores configurables

Podés sobrescribir los valores por defecto modificando el archivo `values.yaml` o creando uno nuevo (`my-values.yaml`).

| Parámetro               | Descripción                                                | Valor por defecto |
| ----------------------- | ---------------------------------------------------------- | ----------------- |
| `replicaCount`          | Número de réplicas del Deployment                          | `2`               |
| `image.repository`      | Imagen del contenedor                                      | `nginx`           |
| `image.tag`             | Versión de la imagen                                       | `alpine`          |
| `service.type`          | Tipo de servicio (`ClusterIP`, `NodePort`, `LoadBalancer`) | `ClusterIP`       |
| `service.port`          | Puerto expuesto por el servicio                            | `80`              |
| `ingress.enabled`       | Habilitar Ingress                                          | `true`            |
| `ingress.hosts[0].host` | Hostname para el Ingress                                   | `demo.local`      |

---

## 📌 Ejemplo de instalación con valores personalizados

```bash
helm install demo-nginx ./demo-chart -f my-values.yaml
```

Ejemplo de `my-values.yaml`:

```yaml
replicaCount: 3
image:
  repository: nginx
  tag: stable
service:
  type: NodePort
  port: 8080
ingress:
  enabled: true
  hosts:
    - host: demo.local
      paths:
        - path: /
          pathType: ImplementationSpecific
```

---

## 🧹 Desinstalación

Para eliminar el despliegue:

```bash
helm uninstall demo-nginx
```

---

## 📄 Notas

* Se requiere un **Ingress Controller** activo en el clúster para que funcione el host `demo.local`.
* El nombre `demo.local` debe agregarse en el archivo `hosts` de tu sistema para la resolución local.
* Probado en Kubernetes local usando Docker Desktop y Helm 3.
