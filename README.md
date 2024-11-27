# 0.0 Proyecto AWS, Terraform, Web, PaaS y Monitorización.

# Proyecto AWS, Terraform, Web, PaaS y Monitorización

**Publicación de la Web Corporativa**  
- Usar la máquina Windows Server 2022 existente para alojar la web corporativa de Kappa.  
- Configurar entornos de desarrollo y preproducción para el frontal web.  
- Automatizar la migración de código entre entornos, con validación antes de pasar a producción.  

**Prueba de Concepto (PoC)**  
- Desplegar una instancia de WordPress en contenedores en una máquina Linux nueva:  
  - WordPress en un contenedor.  
  - Servidor MySQL en otro contenedor.  
- Esta PoC será la base para la nueva web de Kappa.  

**Seguridad y Alta Disponibilidad**  
- Separar el código de la web en una unidad independiente por seguridad.  
- Implementar alta disponibilidad (HA) para garantizar la continuidad del servicio.  
- Configurar un balanceador de carga para distribuir el tráfico de la web corporativa.  

**Monitorización y Observabilidad**  
- Supervisar los nodos de producción con Centreon.  
- La máquina de monitorización será independiente del grupo de máquinas de la solución web.  

**Modernización Digital y Responsabilidad Social**  
- **PaaS Clásico:** Crear una PoC con una plataforma como servicio (PaaS), aplicando SCRUM, para empoderar a jóvenes desarrolladores locales e impulsar la innovación.  
- **Microservicios:** Desplegar la aplicación en contenedores y orquestarlos con herramientas como Kubernetes.  
- Incluir monitorización y observabilidad para entender mejor el comportamiento y rendimiento del sistema digital.  

---

**Implementación Técnica**  
- **Infraestructura como Código (IaC):**  
  - Utilizar Terraform para definir y gestionar toda la infraestructura de Kappa.  
  - Todo será versionado en un repositorio Git con documentación detallada para todo el equipo.

---

### 0.0.1 Arquitectura del Proyecto:

imagen

## 0.1 Buenas prácticas, utilizadas para este proyecto:

### 0.1.1 Control de versiones de este proyecto.

1. En la Rama Main, se subirá todo, el Terraform, el php, etc... Producción.
2. se creará una copia, identica en otra rama. Preproducción.
3. Los cambios, se trabajarán desde una 3 rama. La de desarrollo.
4. Desde ahí se trabajarán diferentes cosas, rama para el php, rama para el terraform, etc...

![image](https://github.com/user-attachments/assets/9b8b9bfd-937a-489c-a920-0ac9f6e089ec)

### 0.1.2 Seguridad.

1. Las claves API, NO SE VAN A SUBIR **DIRECTAMENTE EN EL GITHUB, en el repositorio remoto**. (hay bots que los buscan y pueden darnos "sorpresas").
2. Prohibido iniciar sesión en AWS con el usuario ROOT.
3. Las credenciales **JAMÁS DEBEN SER EXPUESTAS EN EL GITHUB** Sin embargo, hay que encontrar alguna alternativa para poder subirla aquí.
   
## 0.2 Requisitos.

En mi S.O. Windows 10:
- Terraform.
- AWS.
- AWS CLI descargado.

## 0.3 ¿Cuales son las herramientas a utilizar, para qué sirven?

**¿Qué es Centreon?**
Centreon es una plataforma de monitorización de infraestructura y redes que permite supervisar servidores, aplicaciones, dispositivos de red, servicios, y más.
Diseñado para entornos empresariales, combina funciones de recopilación de métricas, generación de alertas y gestión de eventos.
Es modular, lo que permite integrarlo con otras herramientas (como Grafana o Prometheus) para extender sus capacidades.

Características principales:
Soporte Multi-Protocolo:
Usa protocolos como SNMP, SSH, WMI, NRPE, o API para monitorizar dispositivos y servicios.
Alertas y Notificaciones:
Genera alertas configurables para fallos en el sistema o rendimiento anómalo.
Informes y Paneles:
Incluye dashboards prediseñados y generación de informes periódicos.
Escalabilidad:
Ideal para redes pequeñas o grandes infraestructuras con miles de dispositivos.
Plugins:
Compatible con cientos de plugins para añadir soporte a tecnologías específicas.
¿Es reactivo?
Sí, Centreon es reactivo, porque funciona detectando eventos en tiempo real y generando alertas basadas en estados predefinidos:
Estados reactivos: "UP", "DOWN", "WARNING", "CRITICAL".
Estas alertas permiten al administrador tomar medidas correctivas.
No es exclusivamente reactivo: Centreon también puede generar métricas históricas para análisis y prever problemas futuros.

**¿Qué es Grafana?**
Grafana es una herramienta de visualización y análisis de datos.
Se utiliza para crear dashboards personalizados a partir de datos recopilados por herramientas como Prometheus, Centreon, InfluxDB, Elasticsearch, y más.
Características principales:
Dashboards Interactivos:
Permite combinar múltiples fuentes de datos en gráficos, tablas, y otros widgets interactivos.
Alertas Avanzadas:
Configura alertas basadas en reglas personalizadas y recíbelas por correo, Slack, o PagerDuty.
Integración Multi-Fuente:
Compatible con sistemas de monitorización, bases de datos, y APIs externas.
Fácil de Usar:
Interfaz intuitiva con soporte para plantillas y lenguajes de consulta (como PromQL para Prometheus).
Rol de Grafana en una infraestructura de monitorización:
No es un monitorizador en sí mismo. Grafana no recopila datos, sino que se conecta a herramientas como Prometheus o Centreon para mostrar esos datos de manera gráfica.
Su fortaleza radica en la capacidad de generar informes visuales avanzados y consolidar múltiples fuentes de datos en un solo lugar.

**¿Qué es Prometheus?**
Prometheus es un sistema de monitorización y almacenamiento de métricas en serie temporal.
Fue desarrollado originalmente por SoundCloud y ahora es parte de la Cloud Native Computing Foundation (CNCF).
Características principales:
Modelo Pull:
Prometheus recopila métricas de manera activa (pull) desde los endpoints configurados (expuestos por servicios o aplicaciones).
Serie Temporal:
Almacena métricas como datos de series temporales, lo que permite un análisis muy detallado.
Lenguaje de Consultas (PromQL):
Ofrece una potente forma de consultar y manipular métricas almacenadas.
Alertmanager:
Componente que gestiona las alertas generadas por Prometheus basadas en condiciones definidas por el usuario.
Ecosistema Extensible:
Se integra fácilmente con servicios en la nube, herramientas de orquestación como Kubernetes, y visualización en Grafana.
Rol de Prometheus en una infraestructura de monitorización:
Prometheus es proactivo, porque se anticipa a problemas mediante el análisis de métricas históricas y actuales.
Es ideal para entornos modernos de contenedores y microservicios (e.g., Kubernetes).
Comparación y Complementariedad
Característica	Centreon	Grafana	Prometheus
Rol principal	Monitorización y alertas	Visualización de datos	Monitorización y almacenamiento de métricas
Datos procesados	Estados (UP/DOWN, CRITICAL)	Métricas y gráficos	Métricas en series temporales
Recopilación de datos	Basado en plugins y protocolos	No recopila datos	Pull desde endpoints (scraping)
Alertas	Reactivas	Basadas en datos de otros	Proactivas
Escalabilidad	Ideal para infraestructura compleja	Escalable en visualización	Muy escalable en entornos cloud-native
Facilidad de uso	Configuración robusta y centralizada	Intuitivo para dashboards	Curva de aprendizaje más alta
¿Cómo trabajan juntos?
Centreon: Detecta problemas en tiempo real y genera estados críticos (UP/DOWN). Es excelente para la monitorización reactiva de sistemas tradicionales.
Prometheus: Recopila métricas detalladas, analiza patrones y genera alertas proactivas. Ideal para entornos modernos.
Grafana: Toma las métricas de Centreon, Prometheus, y otras fuentes para presentar datos en un formato visual atractivo y unificado.
En una infraestructura moderna, estas herramientas son altamente complementarias y pueden combinarse para obtener un sistema de monitorización robusto y completo.

# 1.0 AWS

## 1.1 Crear el usuario en AWS.

Para ello, buscamos IAM, y creamos el usuario:

![image](https://github.com/user-attachments/assets/416371b7-82ec-4abd-bd95-367156c6eda9)

Nos vamos a "Usuarios" y "Crear Usuario".

![image](https://github.com/user-attachments/assets/d66b53c2-9ab9-4ec7-b7d0-295860af2f07)

Los permisos van a ser:
- AdministratorAccess

![image](https://github.com/user-attachments/assets/deb7517d-2530-4439-888b-e30c17245ab0)

![image](https://github.com/user-attachments/assets/3db6af91-1fbe-4137-b3c2-8bff4d23b520)

Y descargamos las credenciales. VAMOS A TENER QUE SUBIRLAS AQUÍ DE ALGUNA MANERA SIN QUE PUEDA SER ABIERTO Y LEIDO O AL DESCARGARSE QUE SE LEA.

![image](https://github.com/user-attachments/assets/c5158e60-ee6a-4388-a4e3-d894815fe507)

Como podemos ver también nos pide el AWS Access Key ID.

![image](https://github.com/user-attachments/assets/e41f5ea1-4393-4d0b-abf5-3086e63b26d0)

Como se puede apreciar, no tengo, debo de crear una.

![image](https://github.com/user-attachments/assets/1e3f18f2-a462-4201-9ca4-701eff9ed22e)

![image](https://github.com/user-attachments/assets/2b5afae0-fcaa-492c-aac4-8083a6d9dfa5)

![image](https://github.com/user-attachments/assets/c0bcbcc7-117e-4977-9ace-0381a8fad34a)

Y voy a descargarla.

![image](https://github.com/user-attachments/assets/5f94e582-ed6b-4cfd-acac-30dd6773fb83)

Así que volveré al GitBash:

![image](https://github.com/user-attachments/assets/536a5d8a-b59a-455d-ab45-8ec544d3a23c)

## 1.2 Infraestructura como código, Terraform para AWS.

Ahora solo vamos a comprobar de que tenemos terraform descargado. `terraform --help`

Voy a crear una carpeta nueva, `terraform scripts` .

> [!TIP]
> Mientras estoy haciendo el código de terraform para las instancias de AWS, me doy cuenta de que necesito.
> El ID de las AMI's, es decir, si va  aser un Ubuntu, un CentOS, etc...
> Por lo tanto, primero voy a leerme la documentación, por ejemplo, para monitorización, en que S.O. puedo instalar Grafana, Prometheus, Centreon...
>
> - https://grafana.com/docs/grafana/latest/setup-grafana/installation/debian/
> 
> El puerto que utiliza es el 3000.
>
> 
> - https://download.centreon.com/
> - https://docs.centreon.com/docs/installation/compatibility/
> - https://docs.centreon.com/docs/installation/installation-of-a-central-server/using-packages/
> 
> El puerto que utiliza es el 80.
>
> 
> - ![image](https://github.com/user-attachments/assets/93cf2881-e959-4529-bb5a-9285269072ff)
>
> Así que, tras leer las documentaciones y consultarme, voy a proceder a utilizar el Amazon Linux.
> 
> ![image](https://github.com/user-attachments/assets/03f5a158-48a8-4ec1-97b5-7363777176f9)
>

> [!IMPORTANT]
> **Además.**
>
> Es todavía más conveniente y NECESARIO. Probarlo todo, antes de crear el Terraform. Así que voy a crear la instancia, y descargar todo.
> 



Y el código del terraform para AWS va a ser:

```
provider "AWS"{

}
```

# Crear la Web desde 0.

> [!IMPORTANT]
> Prohibido usar XAMPP.
> 
> La página va a ser programada y creada desde cero.
>
> Se van a usar frameworks como "Bootstrap" o "Django".
>

## Descargar las cosas

### Frameworks:

- Flask
- Boostrap

