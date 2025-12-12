# Sandbox
Un ***sandbox*** es un **entorno controlado**, aislado y seguro que se utiliza para ejecutar programas, procesar archivos o probar código sin que estos tengan la capacidad de afectar al sistema operativo principal ni a otros recursos críticos. La idea es crear un “espacio cerrado”, como una caja de arena donde los niños juegan sin peligro, pero aplicado a la informática.

### ¿Para qué sirve?
+ Probar programas o código sin riesgo de daña el sistema
+ Analizar archivos sospechosos (como por ejemplo malware) sin infectar el equipo.
+ Ejecutar aplicaciones con permisos muy limitados
+ Simular entornos para desarrollo o experimentación

### ¿Cómo funciona?
Un **sandbox** funciona creando un entorno aislado donde un programa puede ejecutarse sin afectar al sistema real. Para lograrlo, limita los permisos del software: controla qué archivos puede tocar, qué procesos puede ver, cuánta memoria puede usar o si puede acceder a internet. Cada acción que intenta realizar pasa por un **filtro de seguridad**, y el sandbox decide si permitirla o bloquearla.

Además, utiliza un **sistema de archivos temporal** donde todo lo que el programa hace queda encerrado. De este modo, aunque intente modificar el sistema o comportarse de forma peligrosa, los cambios quedan atrapados en ese espacio aislado y se eliminan al cerrar el sandbox. Esto permite *probar código, analizar archivos* o *ejecutar software desconocido* sin riesgos.

### Ejemplos de Sandbox
- Máquinas virtuales (VirtualBox, VMware)
- Espacios de pruebas en navegadores (Chrome Sandbox)
- Herramientas coo Firejail, Sandboxie o Docker

---

## Prueba de aplicación en un entono controlado (Sandboxing)
En esta actividad voy a documentar como he podido realizar la prueba de la aplicación lavadero en un entorno controlado. 
Los objetivos de la actividad han sido:
- Conocer como se puede ejecutar programas, malware, etc en entornos controlados y aislados para su análisis
- Ser capaz de hacer Sandboxing de un programa

### Desarrollo de la actividad
Lo primero es puntualizar que esta actividad la he relizado en la máquina Kali Linux de la asignatura, la cual tiene instalados ya Visual Studio code y tiene creadas PKI para poder conectarme a GitHub.
Una vez aclarado esto lo primero que hago siempre antes de comenzar a realizar cualquier actividad es ejecutar en la terminal el comando `sudo apt update` para actualizar la lista de paquetes disponibles de los repositorios por si acaso hay nuevas versiones de programas. 

![apt udpate](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img1.png)

A continuación voy a ir a mi cuenta de GitHub y voy a crear un repositorio tal y como indica el profesor, ya que habrá que entregar el mismo como muestra de realización de la actividad. 
para crearlo lo que hay que hacer es 
1. Dar al símbolo + del menú superior de GitHub
1. Poner el nombre que nos pide la tarea "PPSUnidad1-ActividadSandboking-TuNombre" en mi caso sería PPSUnidad1-ActividadSandboking-naiara
1. Añado un archivo readme
1. Clic encima de crear repositorio (botón verde al final de la página) 

![Pasos para crear un repositorio](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img2.png)

En esta imágen se puede observar como el repositorio ya está creado y tiene únicamente en su interior el archivo README.md

![Repositorio ya creado](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img3.png)

El proximo paso es clonar el repositorio que acabamos de crear, para ello tan solo hay que seguir los siguientes pasos:
1. Clic encima del botón `<> Code`
1. Se abrirá un menú hacia abajo con diferentes opciones, https, ssh (que es la que elegimos) y GitHub CLI
1. CLic sobre el símbolo de *copiar*

![Copiar el link](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img4.png)

En un terminal de la máquina (en mi caso Kali Linux) me dirigiré al directorio Desktop con `cd Desktop` porque es donde tengo guardadas todas las tareas y me parece mucho más cómodo y visual para trabajar. A continuación pondré el comando `git clone https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara` para copiar el repositorio en el Escritorio de la máquina virtual.

![Clonación del repositorio en el Escritorio](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img5.png)

Me muevo al repositorio que acabo de crear con el comando cd nombre del repositorio que en mi caso sería 
~~~
cd /PPSUnidad1-ActividadSandboxing-naiara
~~~
Y dentro ejecuto un ls para ver si se ha clonado bien el repositorio y está el README.md

![cd y ls](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img6.png)
