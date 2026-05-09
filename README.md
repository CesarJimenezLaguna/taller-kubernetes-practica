# Taller de Kubernetes

## Estructura del Proyecto

`hello-world-kubernetes/app/` –> contiene el código de la web junto con el Dockerfile 
`hello-world-kubernetes/k8s` –> contiene los manifiestos de Kubernetes:
    `front/` –> configuración de despliegue y el servicio. 
    `ingress/` –> acceso externo al clúster de Kubernetes. 
    `kustomization.yaml`–> orden de ejecución de los manifiestos. 


`hello-world-kubernetes/argocd` –> configuración de GitOps:
    `application.yaml` –> aplicación de ArgoCD.

`hello-world-kubernetes/docs` –> imágenes de la entrega. 


## Componentes

### 1. Capa de Aplicación (`app/`)

#### `Dockerfile`

Se utiliza la imagen `nginx:1.27-alpine` y se copia el archivo `index.html` en el directorio de Nginx. 

---

### 2. Manifiestos (`k8s/`)

#### `front/`

Se define el despliege con `deployment.yaml`, indicando el nombre del despliegue, el nombre de la plantilla, la imagen de docker que se usa (kurbenetes-hello-world:1.0.0) y los puertos de la aplicación. Además, se incluyen etiquetas para comprobar si sigue activa la app (liveness) o si puede recibir tráfico (readiness). 

Se define también el servicio con `service.yaml` para acceder a la app con IP interna (ClusterIP), y se mapea el puerto 80 del sevicio al puerto 80 del contenedor. 

##### `ingress/ingress.yaml`
Controladora de acceso externo al clúster con el dominio `hello.local`:

#### `kustomization.yaml`
Define el orden de la ejecución de la aplicación.

---

### 3. Argo CD (`argocd/`)

Se configura el manifiesto de Argo CD con `application.yaml` para declarar el estado deseado de la aplicación mediante los manifiestos. 

---

### 4. Documentación (`docs/`)

Imágenes de la ejecución. 
