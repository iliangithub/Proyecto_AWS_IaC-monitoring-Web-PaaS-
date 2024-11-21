# 0.0 Proyecto AWS, Terraform, Web, PaaS y Monitorización.

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
> - https://grafana.com/docs/grafana/latest/setup-grafana/installation/
> - https://download.centreon.com/
> - ![image](https://github.com/user-attachments/assets/93cf2881-e959-4529-bb5a-9285269072ff)
>
> Así que, tras leer las documentaciones y consultarme, voy a proceder a utilizar el Amazon Linux.
> 
> ![image](https://github.com/user-attachments/assets/03f5a158-48a8-4ec1-97b5-7363777176f9)



Y el código del terraform para AWS va a ser:

```
provider "AWS"{

}
```
