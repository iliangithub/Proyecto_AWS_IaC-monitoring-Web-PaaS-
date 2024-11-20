# Proyecto_IaC-monitoring-Web-PaaS-

Publicación de la Web Corporativa: 
Utilizar la máquina Windows Server 2022 existente para alojar la 
web corporativa de "Kappa". 
Crear entornos de desarrollo y preproducción para el frontal 
web. 
Automatizar la subida de código entre los entornos, con 
validación en producción. 
Prueba de Concepto (PoC): En una máquina nueva linux, desplegar 
una instancia de WordPress en un contenedor local. El servidor 
MySQL también estará en un contenedor diferente. Esta PoC 
servirá como base para la nueva web sobre "Kappa". 
Seguridad y Alta Disponibilidad: 
Separar el código de la web en una unidad diferente por motivos 
de seguridad. 
Implementar alta disponibilidad (HA) para garantizar la 
continuidad del servicio. 
Configurar un balanceador de carga para distribuir el tráfico de 
la web corporativa. 

Monitorización y Observabilidad: 
Supervisar los nodos de producción utilizando una solución 
basada en Centreon. 
La máquina dedicada para monitorización no formará parte del 
grupo de máquinas con la solución web. 

Modernización Digital y Responsabilidad Social: 
Explorar dos enfoques:  
PaaS Clásico: Crear una prueba de concepto (POC) utilizando una 
plataforma como servicio (PaaS) alineada con la metodología 
SCRUM del equipo de desarrollo. Gata To To ve esto como una 
oportunidad para empoderar a jóvenes desarrolladores locales y 
fomentar la innovación. 
Arquitectura de Microservicios: Desplegar la aplicación en 
contenedores y orquestarla (por ejemplo, utilizando Kubernetes). 
Monitorizar los nuevos elementos digitales, incluyendo tanto la 
aplicación PaaS como los microservicios. Introducir el concepto 
de observabilidad, que va más allá de la simple monitorización y 
permite comprender mejor el rendimiento y el comportamiento de 
los sistemas digitales 

3. Beneficios Esperados 
Mayor Eficiencia: La automatización y la observabilidad 
mejorarán la eficiencia operativa. 
Mayor Disponibilidad: La HA y el balanceo de carga garantizarán 
la disponibilidad de la web corporativa. 
Innovación Tecnológica y Cambio Social: Crazy Maraca Inc no solo 
busca el éxito comercial, sino también contribuir a causas 
sociales. Gata To To está comprometida con proyectos que 
promuevan la educación digital en comunidades desfavorecidas. 


4. Implementación Técnica 
Para lograr estos objetivos, proponemos lo siguiente: 
Infraestructura como Código (IaC):  
Utilizaremos Terraform para definir y gestionar la 
infraestructura de "Kappa". Todo estará codificado y 
versionado en un repositorio Git. 
La documentación será exhaustiva y estará disponible para todo 
el equipo. 


## Buenas prácticas, utilizadas para este proyecto:

### Control de versiones de este proyecto.

1. En la Rama Main, se subirá todo, el Terraform, el php, etc... Producción.
2. se creará una copia, identica en otra rama. Preproducción.
3. Los cambios, se trabajarán desde una 3 rama. La de desarrollo.
4. Desde ahí se trabajarán diferentes cosas, rama para el php, rama para el terraform, etc...

![image](https://github.com/user-attachments/assets/9b8b9bfd-937a-489c-a920-0ac9f6e089ec)

### Seguridad.

1. Las claves API, NO SE VAN A SUBIR **DIRECTAMENTE EN EL GITHUB, en el repositorio remoto**. (hay bots que los buscan y pueden darnos "sorpresas").
2. Prohibido iniciar sesión en AWS con el usuario ROOT.
