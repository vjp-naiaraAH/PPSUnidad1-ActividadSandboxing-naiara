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