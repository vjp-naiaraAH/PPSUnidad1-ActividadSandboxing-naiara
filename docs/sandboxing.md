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

---

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
1. Clic sobre el símbolo de *copiar*

![Copiar el link](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img4.png)

En un terminal de la máquina virtual (en mi caso la vm Kali) me dirigiré al directorio Desktop con `cd Desktop` porque es donde tengo guardadas todas las tareas y me parece mucho más cómodo y visual para trabajar. A continuación pondré el comando 
~~~
git clone https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara 
~~~
para copiar el repositorio en el Escritorio de la máquina virtual.

![Clonación del repositorio en el Escritorio](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img5.png)

Me muevo al repositorio que acabo de crear con el comando cd nombre del repositorio que en mi caso sería 
~~~
cd /PPSUnidad1-ActividadSandboxing-naiara
~~~
Y dentro ejecuto un ls para ver si se ha clonado bien el repositorio y está el README.md

![cd y ls](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img6.png)

Ejecuto en el terminal de Kali 
~~~
sudo apt install firejail
~~~ 
para instalar el software firejail por si acaso no está instalado en Kali aún.

![instalar firejail](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img7.png)

Como voy a usar el programa de lavadero.py lo que voy ha hacer es volver a la actividad "Actividad-Elementos-Programa-Python" y busco donde está comprimida la carpeta del programa, clic sobre el programa [lavadero.py](https://github.com/jmmedinac03vjp/PuestaProduccionSegura/blob/main/Unidad1-PruebaAplicaciones/Actividad-ElementosProgramaPython/src.zip)

![lavadero](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img8.png)

A continuación para descargar el comprimido del programa, hay que seguir los siguientes pasos:
1. Clic encima de View rar
2. Comenzará una descarga, clic encima del símbolo de decarga
3. En el archivo comprimido que se nos ha descargado hacer clic en la carpeta que sale a la derecha del mismo. 

![lavadero](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img9.png)

Se nos abrirá la carpeta Downloads o Descargas de nuestra máquina. A continuación lo que hay que hacer es clic derecho sobre el archivo descargado y copiarlo.

![lavadero](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img10.png)

Ahora lo que tenemos que hacer es ir a la localización del repositorio que hemos clonado anteriormente. En mi caso es `~/Desktop/PPSUnidad1-ActividadSandboxing-naiara` y pegar el comprimido que habiamos copiado en el paso anterior. Lo descomprimo con clic derecho y selecciono la opción descomprimir aquí.

![copia-pega](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img11.png)

Y ahora para mayor comodidad a la hora de subirlo a GitHub lo que hago es abrir el repositorio en la aplicación Visual Studio Code. Para elllo he seguido los siguientes pasos:
1. File -> Open Folder -> 3. Desktop -> 4. PPSUnuidad1-ActividadSandboxing-naiara -> Open in new window -> Yes I trust the authors

![copia-pega](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img12.png)

 En esta captura se puede observar el repositorio abierto ya con el programa en su interior y descomprimido.

![copia-pega](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img13.png)

Llegó la hora de hacer un commit para que se guarden los cambios que hemos realizado (añadir el programa lavadero al repositorio). Para ello seguí los siguientes pasos:
Flecha 1: clic cobre el símbolo git en el menú de la izquierda de visual.
Flecha 2: clic sobre el símbolo + para añadir todo.
Flecha 3: pongo un mensaje para poner un titulo al commit
Flecha:  Clic sobre el botón Commit para subirlo  

![copia-pega](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img14.png)

Accedo a la 