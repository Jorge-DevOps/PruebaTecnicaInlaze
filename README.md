# PruebaTecnicaInlaze

## Diseño de Infraestructura

## Arquitectura AWS
![Arquitecture.png](https://lh3.googleusercontent.com/fife/ALs6j_Ebi_BH5CkgriyeKBWl3Dp4shwGToTFgn8hCwEFAkTbDgENnetoNjkbF5Vl3GSobex07UickDfzicozC1qBjivIAZsYJiiqClP7qpm-uIg6ye2mXlVb3NAaY91kVOYVqFRN0SSWrrEwSbukiyHjiGp9fIgpQF4faUXHFsmoUfnzhppApOutbWtVvgFHnCkVShGvTm9MsJP_3zdwTPjrYlwXML9KNLsnNovNooaxaFD25iNEKCNohS33KhPbU6dLrkM3NsRFUI0TfbJb08Kmtr37ZAy1QHnI-rE3FDSAjgmRkkXyMiWxcTy480fspNpZr-n_lSOIzOriz-EWrvAWYYt_wVc81v-0u49d8bkj-X9CjBcZXbh5MZpUbauhUbp8JqegpT3cZI0hcQnGiUZJ3LSmZZk0tn1x4g9hQ8UIb8JiVYdzaK7OodBOHghqEie7XikvqYO0vpdj7Uvw8bG2x13tvbeVHB5L2FeHz6J42WBqFLuYIpUHoHnOeHW75cY5lWLOl3jp9nwANZZ1lnRO_DNu60NszT5_wWSGRxp_BmI2SGmVTdPGzywIcLkqcAIsII-DAaZqF6I6_vAHSLA2MnRrJDxVyI2a92AGR_nsVd8Vu8RrQW9HB7oPYdvHHW5gUyMxSwhT8Aw6kUgcR8ZST5GJe5IyOCWMdjjUpmCNQwQTzCt9uuLq6olhRQHbZBD4su3mUokUCMB0N_1wj_HNzqm2Ui5d5LlpayUei0TOLhyAOL3G9jp08WWO1iZ1uqtV9YIfe7XgFGxnnHNTAgpiQ-TxGz36AmKUkBtua2xJ-VnZDEWWAW8cTafAm5quTIW3hUbR7vToUu6W0lUsStIm0yH2zWqbwZ-sDW2ktQTW3rZr3tA_FwweTVxwzDRoTXxhSytUn_XVDoR1zV9KkZ84tq-knEPVsxsFWBI1UufjuTA0rmdH4aHomBSug8vm307fqEEFxSzb7TtQfEY9iXUhAGEbvQGa8OsdV855IJBPcjoAHSdzPObRqccjVxjsiuMeeX-4-HU4eMzh8gKcP7hYSu3bTrp91nHlXLB-Ub9R3tEIxNQIKwWkJnt_dHyXQtyPFUh47Fa-evmDy7aisWRv1Cpa0CVuZzD3aO7ErWadIeEQlWvYZam3mTEEnmZd4JcH62WO7W2Gzee_jryl_5zgynVW-HBvCQuanB5SjSaseV6DxUkPUTFEfGyrL2lh1ZgUZFqJMtss8r0oVO3OsE20kpHDmNV-aLy7914xHRPavXt7yu3BULuew95ThaMhPWIthhoWd1tTU4G15uErE8OXwTP0n0EBhfDuCR_9mdhUPG212CIy17ab5-ZBwhpxZyVv8dRVckCigpYCdpSTnhF_aJc13v8BcEAbbOllKVaIguMvcwsz8sEyGdCr8ONePqOMr9nPdqOCitmNp45vPNaoZOlR8DN6nXVpfjpHgha9NF1hrj1GqDLFMXqD3PQb1WaR3uf9eQvVb_FG5CTJnyrukrBotFBq4I_lYgrgmi4RZWAkEsT2mjjGrHDsXIOOPUKEHzyiNC8IHcsvSQpH1ENvuL11Sjs2nWtVFX_mWCRZMWm7glMKNrrrrqPTF2vfrdWiiGFNwxDMgaMhJR5rpw=w1920-h925)

Esta arquitectura está diseñada sobre la infraestructura de Amazon Web Services (AWS), teniendo en cuenta factores clave para garantizar una estructura escalable y resiliente. El objetivo principal es implementar una aplicación web que se integre con una base de datos de alta disponibilidad.

La arquitectura consta de un frontend implementado en **AWS Amplify**, que se comunica con el backend a través de **API Gateway**, encargado de centralizar y exponer los endpoints de forma eficiente. Además, utilizamos un balanceador de cargas (Application Load Balancer) para distribuir el tráfico HTTPS que ingresa al backend.

En cuanto a medidas de seguridad, hemos incorporado un **Application Firewall (AWS WAF)** para mitigar amenazas como inyecciones SQL, ataques XSS y otros riesgos comunes en aplicaciones web.

Para garantizar alta disponibilidad, la arquitectura está diseñada con **dos zonas de disponibilidad (AZs)** y utiliza **escalamiento horizontal automático** para los microservicios bajo Kubernetes. La base de datos está gestionada por **Amazon Aurora**, configurada en modo **multi-AZ** para proporcionar alta disponibilidad y conmutación automática por error entre zonas de disponibilidad, asegurando la continuidad operativa incluso si una AZ presenta problemas. Además, Aurora puede configurarse con réplicas en cada zona de disponibilidad para una mayor redundancia y capacidad de lectura. Por otro lado, se integra **Redis** como sistema de almacenamiento en memoria, optimizado para la lectura y escritura rápida de datos frecuentes, lo que mejora significativamente el rendimiento de la aplicación.

Para proteger la infraestructura, se implementó una estrategia de separación de componentes prioritarios dentro de una **subred privada** en la **VPC** de AWS. Esto garantiza un mayor nivel de seguridad y control, ya que estos componentes no están directamente expuestos a Internet y solo pueden ser accedidos mediante mecanismos específicos.

---

### DevOps CI/CD

Para el proceso de **DevOps**, se diseñó un flujo eficiente y automatizado que abarca las etapas clave de integración y despliegue continuo. El flujo opera de la siguiente manera:

1. **Commit y Activación del Pipeline**:
    
    Cuando los desarrolladores realizan un commit en la rama **dev** del repositorio, se activa un **trigger** en el pipeline, iniciando automáticamente el flujo de integración continua.
    
2. **Ejecución del Pipeline**:
    
    El pipeline realiza los siguientes pasos de manera secuencial:
    
    - **Descarga del Código**: Recupera la última versión del código desde el repositorio.
    - **Pruebas Automáticas**: Ejecuta pruebas unitarias, de integración y cualquier conjunto adicional de pruebas para garantizar la calidad del código y detectar errores tempranos.
    - **Construcción de Imágenes Docker**: Compila el código y construye imágenes de Docker optimizadas tanto para el backend como para el frontend, asegurando un entorno estandarizado para la ejecución de la aplicación.
    - **Generación de Artefactos**: Crea artefactos (por ejemplo, contenedores Docker, paquetes de frontend estáticos o binarios) que son almacenados en un registro de artefactos para garantizar su rastreabilidad y reusabilidad.
3. **Despliegue Automatizado (CD)**:
    - Los artefactos generados son desplegados en entornos automáticamente para validar su funcionamiento.

La retroalimentación de los resultados del pipeline, como fallos en las pruebas o problemas de construcción, es enviada automáticamente a los desarrolladores para acciones correctivas rápidas.

Este flujo asegura entregas rápidas, fiables y consistentes, reduciendo el tiempo de comercialización y facilitando un ciclo de desarrollo ágil y de alta calidad. 

### Monitoreo

Para garantizar la visibilidad y el control total sobre la infraestructura y las aplicaciones, se implementaron herramientas de monitoreo continuo, proporcionando métricas clave de rendimiento, alertas en tiempo real y capacidades de diagnóstico avanzado. Estas herramientas incluyen:

1. **Amazon CloudWatch**:
    - Recopila y monitorea métricas de rendimiento, como el uso de CPU, memoria, tráfico de red, y latencia de aplicaciones.
    - Proporciona **alarmas personalizables** para notificar eventos críticos, como caídas de servicio o aumentos en el consumo de recursos.
    - Ofrece integración nativa con otros servicios de AWS, como **Auto Scaling**, para reaccionar automáticamente a cambios en la demanda.
2. **Prometheus**:
    - Utilizado para recopilar métricas detalladas de los servicios y aplicaciones mediante un modelo basado en **series temporales**.
    - Se integra con aplicaciones contenedorizadas y orquestadas en **Kubernetes**, permitiendo monitorear recursos a nivel de pod, nodo y clúster.
    - Ofrece la capacidad de definir **alertas avanzadas** con reglas precisas que se integran con sistemas como Slack, PagerDuty o Amazon SNS para notificaciones inmediatas.
3. **Grafana**:
    - Actúa como una herramienta de visualización que consume métricas de **CloudWatch y Prometheus**.
    - Proporciona **dashboards interactivos y personalizables**, facilitando el análisis de datos de rendimiento y tendencias.
    - Permite la correlación de métricas entre diferentes servicios para diagnosticar problemas complejos.
4. **Logs y Auditoría**:
    - **CloudWatch Logs** se configuran para capturar y analizar logs de aplicaciones, eventos del sistema, y tráfico de red.
    - Los logs se centralizan y se indexan para facilitar búsquedas rápidas y análisis históricos.
5. **Alertas y Respuesta Proactiva**:
    - Configuración de **notificaciones automáticas** a través de Amazon SNS, correo electrónico, o plataformas de mensajería como Slack, para mantener al equipo informado sobre problemas críticos.
    - Integración con herramientas de automatización para ejecutar **acciones correctivas automáticas**, como reiniciar instancias defectuosas o ajustar políticas de escalado.

Esta estrategia asegura una supervisión de toda la infraestructura y las aplicaciones, ayudando a prevenir problemas antes de que impacten a los usuarios finales y proporcionando las herramientas necesarias para una resolución rápida y eficiente.

## Implementación de un Pipeline CI/CD


### Ajustes al Proyecto Next.js

Cabe mencionar que se realizaron algunos ajustes en el proyecto Next.js debido a problemas en la compilación de la imagen. Los cambios realizados fueron los siguientes:

1. Se comentó la línea 3 en el archivo `next.config.js`:  
   ```javascript
   // output: "export",
   ```
   Esto se debió a que, al cambiar la forma de ejecutar la compilación de los archivos estáticos de JavaScript, no era posible utilizar el comando `npm start`. Con este ajuste, se pudo ejecutar correctamente el proyecto.

2. Se actualizó el archivo `.eslintrc.js` en la línea 91 para corregir un error en el estándar de nombramiento de funciones. La regla `@typescript-eslint/naming-convention` estaba configurada con el valor `camelCase`, lo que causaba un error durante la compilación debido a que algunas funciones no seguían este estándar. Se cambió el valor a `PascalCase` para resolver el problema.

3. Finalmente, se modificó el comando de inicio `npm start` para permitir el acceso desde cualquier red. El comando se ajustó a:
   ```bash
   npm run next start -H 0.0.0.0
   ```
   Este cambio permitió que el servidor fuera accesible desde cualquier dirección IP, facilitando el acceso remoto durante el desarrollo.

Este ajuste asegura que el proceso de compilación y ejecución del proyecto Next.js se realice correctamente y de manera más flexible.

Se generaron los siguientes archivos para asegurar la correcta ejecución del pipeline de integración y despliegue continuo (CI/CD):

- **Jenkinsfile**: Define las etapas del pipeline y las acciones a ejecutar durante el proceso de integración y despliegue. El archivo se puede consultar en el siguiente enlace:  
  [Jenkinsfile](https://github.com/Jorge-DevOps/PruebaTecnicaInlaze/frontend-challenge-base/blob/main/Jenkinsfile)

- **Dockerfile**: Contiene las instrucciones necesarias para construir la imagen Docker del proyecto. Este archivo configura el entorno de ejecución y asegura que la aplicación se ejecute de manera consistente en cualquier máquina. Puedes ver el archivo aquí:  
  [Dockerfile](https://github.com/Jorge-DevOps/PruebaTecnicaInlaze/frontend-challenge-base/blob/main/dockerfile)


## Implementación de ArgoCD

Para implementar ArgoCD y gestionar el despliegue de aplicaciones en Kubernetes, se siguieron los siguientes pasos:

1. **Crear el Namespace de ArgoCD**:
   ```bash
   kubectl create namespace argocd
   ```

2. **Instalar ArgoCD en el cluster de Kubernetes**:
   ```bash
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   ```

3. **Verificar los servicios de ArgoCD**:
   ```bash
   kubectl get svc -n argocd
   ```

4. **Hacer un port-forward para acceder al servidor de ArgoCD**:
   ```bash
   kubectl port-forward svc/argocd-server -n argocd 8080:443 --address 0.0.0.0 &
   ```

5. **Obtener la contraseña inicial del administrador de ArgoCD**:
   ```bash
   kubectl get secret -n argocd argocd-initial-admin-secret -o yaml
   ```

6. **Decodificar la contraseña base64**:
   ```bash
   echo NTV1WHplajNxZFhLd1B3dg== | base64 -d
   ```

Con estos pasos realizados, se creó la aplicación en ArgoCD utilizando el siguiente archivo YAML:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: frontend-challenge
spec:
  destination:
    name: ''
    namespace: default
    server: https://kubernetes.default.svc
  source:
    path: manifests
    repoURL: https://github.com/Jorge-DevOps/frontend-challenge-base
    targetRevision: HEAD
  sources: []
  project: default
```

Además, se crearon los archivos necesarios para el despliegue de la aplicación los cuales se incluyeron dentro del proyecto:

### [deployment.yaml](https://github.com/Jorge-DevOps/PruebaTecnicaInlaze/frontend-challenge-base/blob/main/manifests/deployment.yaml)
### [service.yaml](https://github.com/Jorge-DevOps/PruebaTecnicaInlaze/frontend-challenge-base/blob/main/manifests/service.yaml)
### Detalles:

Para poder replicar el pipeline solo es necesario ajustar las variables contenidas en el encabezado del archivo:

- REPOSIOTRY → Hace referencia a la URL del repositorio en la nube (GitLab, GitHub, etc)
- DOCKER_REGISTRY → Hace referencia al nombre de su perfil en DockerHub
- DOCKER_IMAGE → Hace referencia al nombre que se le va a colocar a la imagen de docker


## Optimización y Mejora de Dockerfile
### Detalles:

Aunque la imagen de Docker se construye correctamente y funciona según lo esperado, se realizaron algunos ajustes para optimizar su funcionamiento y rendimiento:

- **Propiedad `restart: always`**: Se añadió esta propiedad en todos los servicios, lo que garantiza que los contenedores se reinicien automáticamente en caso de fallos o reinicios inesperados, asegurando alta disponibilidad y resiliencia.
  
- **Ajuste de la versión Alpine en Redis**: Se actualizó la versión de la imagen Alpine de Redis para reducir el tamaño de la imagen y mejorar la eficiencia general de la construcción, lo que también optimiza el uso de recursos.

- **Red independiente para contenedores**: Se configuró una red independiente para los contenedores, lo que permite que se comuniquen entre sí y con el host de manera segura y aislada, mejorando la seguridad y el control sobre el tráfico de red.

