# TP4 Sistemas de Computacion

## Modulos de Kernel

## Desafío #1 

### ¿Qué es checkinstall y para qué sirve?

CheckInstall es un programa de computadora para Sistemas Operativos Unix-like que permite la instalación y desinstalación de software compilado desde el código fuente para ser administrado por un Sistema de gestión de paquetes . Después de la compilación del paquete este puede generar paquetes compartibles para Slackware-, RPM, o Debian. El paquete de generado puede ser eliminado limpiamente por el Sistema de gestión de paquetes.

Los beneficios principales de CheckInstall contra simplemente ejecutar make install es la habilidad de desinstalar el paquete del sistema usando su Sistema de gestión de paquetes, además de poder instalar el paquete resultante en varias computadoras. 

Frecuentemente ocurre que un programa está sólo disponible como código fuente tar.gz (no hay paquete disponible rpm o Debian). En ese caso se debe descargar el paquete fuente, demepaquetarlo y compilarlo manualmente. Sin embargo, muchas veces, no se provee una manera apropiada para desinstalar el programa. La herramienta CheckInstall fue escrita por Felipe Eduardo Sánchez Díaz Durán para resolver este problema. 

En un programa compatible con GNU Autoconf se instala el programa (luego de descargado y desempaquetado el paquete fuente) con la secuencia:
```sh
./configure && make && make install.
```

En cambio con checkinstall:
```sh
./configure && make && checkinstall
```

### ¿Se animan a usarlo para empaquetar un hello world ? 

Para hacer esto se debe crear un archivo .c con su respectivo makefile. Posteriormente se hace make y se utiliza checkinstall.Posteriormente se puede utilzar el gestor de paquetes del sistema para instalar el programa. 

### Revisar la bibliografía para impulsar acciones que permitan mejorar la seguridad del kernel, concretamente: evitando cargar módulos que no estén firmados. ¿Qué otras medidas de seguridad podemos implementar para asegurar nuestro ordenador desde el kernel ? 

enlace:  https://access.redhat.com/documentation/es-es/red_hat_enterprise_linux/8/html/managing_monitoring_and_updating_the_kernel/signing-kernel-modules-for-secure-boot_managing-kernel-modules

Si el Arranque Seguro está habilitado, los cargadores de arranque del sistema operativo UEFI, el kernel de Red Hat Enterprise Linux y todos los módulos del kernel tienen que ser firmados con una clave privada y autenticados con la clave pública correspondiente. Si no están firmados y autenticados, el sistema no podrá terminar el proceso de arranque. 

Requisitos:
Se necesita generar un par de claves X.509 públicas y privadas para tener éxito en utilizar módulos del kernel en un sistema habilitado para el Arranque Seguro. Se utilizará la clave privada para firmar el módulo del kernel. También tendrá que añadir la clave pública correspondiente a la Clave del Propietario de la Máquina (MOK) para el Arranque Seguro para validar el módulo firmado. 

Otras medidas de seguridad que se pueden implementar:
- Habilitar SELinux o AppArmor: Sistemas de control de acceso obligatorio que proporcionan políticas de seguridad estrictas.
- Usar Grsecurity/PaX: Conjunto de parches de seguridad que mejoran significativamente la seguridad del kernel.
- Habilitar Secure Boot: Asegura que el sistema arranca con software de confianza.
- Configurar kernel con KSPP (Kernel Self Protection Project): Implementa protecciones avanzadas contra vulnerabilidades.
- Deshabilitar SysRq: Reduce el riesgo desactivando la combinación de teclas que interactúa directamente con el kernel.
- Deshabilitar el acceso a dispositivos USB: Minimiza el vector de ataque restringiendo el uso de dispositivos USB.
- Implementar auditoría de seguridad: Utiliza un sistema de auditoría para monitorizar y registrar eventos de seguridad del sistema.

## Desafío #2

enlace: https://sysprog21.github.io/lkmpg/#preliminaries

### ¿Cómo empiezan y terminan unos y otros ?
### ¿Qué funciones tiene disponible un programa y un módulo ?

Programa: Primero construir un programa que llame a printf(), compilarlo (con opción -Wall y ejecutar strace (strace -tt y strace -c). Explicar lo que se observa.!!

Modulo: La definición de los símbolos proviene del propio kernel; las únicas funciones externas que puede utilizar un módulo, son las proporcionadas por el kernel. Investigar el contenido del archivo /proc/kallsyms .!!

### ¿Quien carga los modulos del kernel?
### Espacio de usuario vs espacio del kernel.
### Espacio de datos y espacio de codigo para usuario y kernel. Riesgos!!
### Drivers. Investigar contenido de /dev.

## Desafío #3

### ¿Qué diferencias se pueden observar entre los dos modinfo ? 
### ¿Qué divers/modulos estan cargados en sus propias pc? comparar las salidas con las computadoras de cada integrante del grupo. Expliquen las diferencias. Carguen un txt con la salida de cada integrante en el repo y pongan un diff en el informe.
### ¿cuales no están cargados pero están disponibles? que pasa cuando el driver de un dispositivo no está disponible. 
### Correr hwinfo en una pc real con hw real y agregar la url de la información de hw en el reporte. 
### ¿Qué diferencia existe entre un módulo y un programa  ? 
### ¿Cómo puede ver una lista de las llamadas al sistema que realiza un simple helloworld en c?
### ¿Que es un segmentation fault? como lo maneja el kernel y como lo hace un programa?
### ¿Se animan a intentar firmar un módulo de kernel ? y documentar el proceso ?  https://askubuntu.com/questions/770205/how-to-sign-kernel-modules-with-sign-file
### Agregar evidencia de la compilación, carga y descarga de su propio módulo imprimiendo el nombre del equipo en los registros del kernel. 
### ¿Que pasa si mi compañero con secure boot habilitado intenta cargar un módulo firmado por mi? 

