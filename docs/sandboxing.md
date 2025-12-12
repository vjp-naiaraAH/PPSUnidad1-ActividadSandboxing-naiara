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

## Prueba de aplicación en un entorno controlado (Sandboxing)
En esta actividad voy a documentar como he podido realizar la prueba de la aplicación lavadero en un entorno controlado. 
Los objetivos de la actividad han sido:
- Conocer como se puede ejecutar programas, malware, etc en entornos controlados y aislados para su análisis
- Ser capaz de hacer Sandboxing de un programa

---

### Desarrollo de la actividad
Lo primero es puntualizar que esta actividad la he realizado en la máquina Kali Linux de la asignatura, la cual tiene instalados ya Visual Studio code y tiene creadas PKI para poder conectarme a GitHub.
Una vez aclarado esto lo primero que hago siempre antes de comenzar a realizar cualquier actividad es ejecutar en la terminal el comando `sudo apt update` para actualizar la lista de paquetes disponibles de los repositorios por si acaso hay nuevas versiones de programas. 

![apt udpate](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img1.png)
---

### Creación del repositorio en GitHub
A continuación voy a ir a mi cuenta de GitHub y voy a crear un repositorio tal y como indica el profesor, ya que habrá que entregar el mismo como muestra de realización de la actividad. 
para crearlo lo que hay que hacer es 
1. Dar al símbolo + del menú superior de GitHub
1. Poner el nombre que nos pide la tarea "PPSUnidad1-ActividadSandboking-TuNombre" en mi caso sería PPSUnidad1-ActividadSandboxing-naiara
1. Añado un archivo readme
1. Clic encima de crear repositorio (botón verde al final de la página) 

![Pasos para crear un repositorio](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img2.png)
---

En esta imágen se puede observar como el repositorio ya está creado y tiene únicamente en su interior el archivo README.md

![Repositorio ya creado](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img3.png)
---

### Clonación del repositorio
El proximo paso es clonar el repositorio que acabamos de crear, para ello tan solo hay que seguir los siguientes pasos:
1. Clic encima del botón `<> Code`
1. Se abrirá un menú hacia abajo con diferentes opciones, https, ssh (que es la que elegimos) y GitHub CLI
1. Clic sobre el símbolo de *copiar*

![Copiar el link](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img4.png)
---

En un terminal de la máquina virtual (en mi caso la vm Kali) me dirigiré al directorio Desktop con `cd Desktop` porque es donde tengo guardadas todas las tareas y me parece mucho más cómodo y visual para trabajar. A continuación pondré el comando 
~~~
git clone https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara 
~~~
para copiar el repositorio en el Escritorio de la máquina virtual.

![Clonación del repositorio en el Escritorio](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img5.png)
---

Me muevo al repositorio que acabo de crear con el comando cd nombre del repositorio que en mi caso sería 
~~~
cd /PPSUnidad1-ActividadSandboxing-naiara
~~~
Y dentro ejecuto un ls para ver si se ha clonado bien el repositorio y está el README.md

![cd y ls](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img6.png)
---

### Agregado del programa al repositorio
Como voy a usar el programa de lavadero.py lo que voy ha hacer es volver a la actividad "Actividad-Elementos-Programa-Python" y busco donde está comprimida la carpeta del programa, clic sobre el programa [lavadero.py](https://github.com/jmmedinac03vjp/PuestaProduccionSegura/blob/main/Unidad1-PruebaAplicaciones/Actividad-ElementosProgramaPython/src.zip)

![lavadero](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img8.png)
---

A continuación para descargar el comprimido del programa, hay que seguir los siguientes pasos:
1. Clic encima de View rar
2. Comenzará una descarga, clic encima del símbolo de descarga
3. En el archivo comprimido que se nos ha descargado hacer clic en la carpeta que sale a la derecha del mismo. 

![lavadero](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img9.png)
---

Se nos abrirá la carpeta Downloads o Descargas de nuestra máquina. A continuación lo que hay que hacer es clic derecho sobre el archivo descargado y copiarlo.

![lavadero](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img10.png)
---

Ahora lo que tenemos que hacer es ir a la localización del repositorio que hemos clonado anteriormente. En mi caso es `~/Desktop/PPSUnidad1-ActividadSandboxing-naiara` y pegar el comprimido que habiamos copiado en el paso anterior. Lo descomprimo con clic derecho y selecciono la opción descomprimir aquí.

![copia-pega](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img11.png)
---

Y ahora para mayor comodidad a la hora de subirlo a GitHub lo que hago es abrir el repositorio en la aplicación Visual Studio Code. Para elllo he seguido los siguientes pasos:
1. File -> Open Folder -> 3. Desktop -> 4. PPSUnuidad1-ActividadSandboxing-naiara -> Open in new window -> Yes I trust the authors

![apertura en visual studio code](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img12.png)
---

 En esta captura se puede observar el repositorio abierto ya con el programa en su interior y descomprimido.

![programa en visual](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img13.png)
---

Llegó la hora de hacer un commit para que se guarden los cambios que hemos realizado (añadir el programa lavadero al repositorio). Para ello seguí los siguientes pasos:
1. clic cobre el símbolo git en el menú de la izquierda de visual.
1. clic sobre el símbolo + para añadir todo.
1. pongo un mensaje para poner un titulo al commit
1.  Clic sobre el botón Commit para subirlo  

![commit](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img14.png)
---

 Ahora si entramos a GitHub y recargamos el repositorio de la actividad [PPSUnidad1-ActividadSandboxing-naiara](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/tree/main). Aparecerá el programa lavadero.

![github](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img15.png)
---

Una cosa interesante de saber para poder continuar con la tarea es saber si en la máquina en la que estoy trabajando, es decir Kali está instalado Python, ya que el programa lavadero está escrito en ese lenguaje.
Para conocer este dato lo que he hecho ha sido ejecutar en una terminal de Kali el comando <Python --version>, el resultado de dicho comando ha sido Python  3.13.7 lo que quiere decir que está instalado en esa versión. Podemos continuar con el ejercicio.

![github](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img16.png)
---

### Instalación de Firejail y Firetools
Ejecuto en el terminal de Kali 
~~~
sudo apt install firejail
~~~ 
para instalar el software firejail por si acaso no está instalado en Kali aún.

![instalar firejail](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img7.png)
---

Ejecuto en la terminal sudo apt install firejail firetools puesto que es necesario ambos paquetes para poder usar correctamente el *Sandbox*.

![github](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img17.png)
---

### Ejecución del Sandbox
Ahora sí ejecuto el programa dentro del Sandbox (entorno seguro) usando el comando 
~~~
firejail --private=. python3 main_app.py
~~~
Que sería el sandbox más básico de firejail
El resultado completo del firejail es el siguiente
~~~
Reading profile /etc/firejail/default.profile
Reading profile /etc/firejail/disable-common.inc
Reading profile /etc/firejail/disable-programs.inc
Reading profile /etc/firejail/landlock-common.inc
Warning: networking feature is disabled in Firejail configuration file

** Note: you can use --noprofile to disable default.profile **

firejail version 0.9.76

Parent pid 26642, child pid 26643
Warning: not remounting /var/lib/docker/overlay2/496d8f236f4874b190794e236f2699f12cbfc8a8a534fed6a4b1642cb1115c89/merged
Warning: not remounting /var/lib/docker/overlay2/c2b0fd92f4725f7bea99b07c335d646ec916132594f479316b3a19e5bd2a08de/merged
Warning: not remounting /var/lib/docker/overlay2/d2b2ff36569c4cc0893906ad61458840c88f3f70ef3c41384022d9558e4c4ee7/merged
Warning: not remounting /var/lib/docker/overlay2/7391c3341c935e0a627994b4db7fa67612122c6bb9501220ec77d122f4d01a14/merged
Warning: not remounting /var/lib/docker/overlay2/80f06f3463329cda539086cb9cbd8a7b4509bb0dbcdad15d549a62d957ed4e2c/merged
Warning: not remounting /var/lib/docker/overlay2/496d8f236f4874b190794e236f2699f12cbfc8a8a534fed6a4b1642cb1115c89/merged
Warning: not remounting /var/lib/docker/overlay2/c2b0fd92f4725f7bea99b07c335d646ec916132594f479316b3a19e5bd2a08de/merged
Warning: not remounting /var/lib/docker/overlay2/d2b2ff36569c4cc0893906ad61458840c88f3f70ef3c41384022d9558e4c4ee7/merged
Warning: not remounting /var/lib/docker/overlay2/7391c3341c935e0a627994b4db7fa67612122c6bb9501220ec77d122f4d01a14/merged
Warning: not remounting /var/lib/docker/overlay2/80f06f3463329cda539086cb9cbd8a7b4509bb0dbcdad15d549a62d957ed4e2c/merged
Warning: cannot find /var/run/utmp
Base filesystem installed in 34.50 ms
Child process initialized in 84.63 ms

=======================================================
EJEMPLO 1: Prelavado (S), Secado a mano (S), Encerado (S)
--- INICIO: Prueba de Lavado con Opciones Personalizadas ---
Opciones solicitadas: [Prelavado: True, Secado a mano: True, Encerado: True]

Coche entra. Estado inicial:
----------------------------------------
Ingresos Acumulados: 0.00 €
Ocupado: True
Prelavado a mano: True
Secado a mano: True
Encerado: True
Fase: 0 - Inactivo
----------------------------------------

AVANZANDO FASE POR FASE:
 (COBRADO: 8.70 €) -> Fase actual: 1 - Cobrando
-> Fase actual: 2 - Haciendo prelavado a mano
-> Fase actual: 3 - Echándole agua
-> Fase actual: 4 - Enjabonando
-> Fase actual: 5 - Pasando rodillos
-> Fase actual: 6 - Haciendo secado automático
-> Fase actual: 0 - Inactivo

----------------------------------------
Lavado completo. Estado final:
----------------------------------------
Ingresos Acumulados: 8.70 €
Ocupado: False
Prelavado a mano: False
Secado a mano: False
Encerado: False
Fase: 0 - Inactivo
----------------------------------------
Ingresos acumulados: 8.70 €
----------------------------------------

=======================================================
EJEMPLO 2: Sin extras (Prelavado: N, Secado a mano: N, Encerado: N)
--- INICIO: Prueba de Lavado con Opciones Personalizadas ---
Opciones solicitadas: [Prelavado: False, Secado a mano: False, Encerado: False]

Coche entra. Estado inicial:
----------------------------------------
Ingresos Acumulados: 8.70 €
Ocupado: True
Prelavado a mano: False
Secado a mano: False
Encerado: False
Fase: 0 - Inactivo
----------------------------------------

AVANZANDO FASE POR FASE:
 (COBRADO: 5.00 €) -> Fase actual: 1 - Cobrando
-> Fase actual: 3 - Echándole agua
-> Fase actual: 4 - Enjabonando
-> Fase actual: 5 - Pasando rodillos
-> Fase actual: 7 - Haciendo secado a mano
-> Fase actual: 0 - Inactivo

----------------------------------------
Lavado completo. Estado final:
----------------------------------------
Ingresos Acumulados: 13.70 €
Ocupado: False
Prelavado a mano: False
Secado a mano: False
Encerado: False
Fase: 0 - Inactivo
----------------------------------------
Ingresos acumulados: 13.70 €
----------------------------------------

=======================================================
EJEMPLO 3: ERROR (Encerado S, Secado a mano N)
--- INICIO: Prueba de Lavado con Opciones Personalizadas ---
Opciones solicitadas: [Prelavado: False, Secado a mano: False, Encerado: True]
ERROR DE ARGUMENTO: No se puede encerar el coche sin secado a mano

=======================================================
EJEMPLO 4: Prelavado (S), Secado a mano (N), Encerado (N)
Traceback (most recent call last):
  File "/home/PPSnaiara/main_app.py", line 83, in <module>
    ejecutarSimulacion(lavadero_global, prelavado=True, secado_mano=False)
    ~~~~~~~~~~~~~~~~~~^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
TypeError: ejecutarSimulacion() missing 1 required positional argument: 'encerado'

Parent is shutting down, bye...
~~~

![github](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img18.png)
---

Como se ve en la próxima imágen, el programa se ejecuta dentro de un sandbox completamente aislado del resto del sistema. Esto confirma que la aplicación queda protegida aunque sea maliciosa o tenga vulnerabilidades. La opción `--debug` muestra en pantalla todo lo que Firejail está haciendo.

![github](https://github.com/vjp-naiaraAH/PPSUnidad1-ActividadSandboxing-naiara/blob/main/docs/images/img19.png)

---

## Conclusiones y reflexión 
Gracias al uso de Firejail con la opción `--private`, la aplicación Python se ejecutó en un entorno completamente aislado:
- No tiene acceso al sistema de archivos real del host (solo ve una copia privada del directorio actual).
- No puede acceder a la red (por defecto está bloqueada en la mayoría de distribuciones modernas).
- No puede ver ni interactuar con otros procesos del sistema.
- Cualquier cambio o archivo creado desaparece al cerrar el sandbox.

Esto demuestra que, incluso si el script `lavadero.py` hubiera sido malicioso (por ejemplo, intentara borrar archivos del home, conectarse a un C2, crear procesos persistentes, etc.), no habría podido afectar al sistema real de Kali Linux.

Firejail es una herramienta extremadamente ligera y eficaz para sandboxing rápido de aplicaciones en Linux, ideal tanto para análisis de malware como para ejecutar software de procedencia desconocida con seguridad.