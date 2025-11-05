id: bastionado-debian
title: Guía de Bastionado de Servidor Debian
summary: Guía de Bastionado de Servidor Debian
authors: Inca Vico Prieto
status: published

# **Informe de bastionado del arranque en Debian (VirtualBox)**

## **1\. Inicio de la instalación y elección del método**

Arranco la máquina virtual con la ISO de Debian y elijo el modo de instalación (puede ser gráfico o por texto).

![Instalación Debian](img/debianinstalacion.png)  
​

## **2\. Selección de método de particionado**

Elijo “Manual” para configurar particiones acorde a las buenas prácticas.

![Partición manual](img/debianparticionadomanual.png)  
​

## **3\. Selección del disco para particionado**

Selecciono el disco duro virtual disponible.

![Partición guiada](img/debianparticionguiada.png)  
​

## **4\. Creación de las particiones**

Creo las siguientes particiones, seleccionando "espacio libre" y definiendo una por una:

![Espacio libre](img/debianparticionespaciolibre.png)

### /boot 

1 GB, primaria, ext4, marca de arranque activada  
![Boot](img/debianparticiondediscoboot.png)

### / 

10 GB, primaria, ext4  
![Raíz](img/debianparticionraiz.png)

### swap 

2 GB, lógica, área de intercambio  
![swap](img/debianparticiondediscoswap.png)

### /home 

Resto del disco, lógica, ext4
![home](img/debianparticiondediscohome.png)

​  
​  
​

## **5\. Confirmación de todas las particiones**

Verifico que las particiones han quedado correctamente configuradas.

![Confirmación](img/debiantodaslasparticiones.png) 
​

## **6\. Instalación del sistema base**

Dejo que el instalador copie los archivos y configure la base de Debian.

## **7\. Configuración del gestor de paquetes y repositorios**

Elijo el repositorio recomendado de Debian para obtener actualizaciones (por defecto: deb.debian.org), omitiendo proxy si no es necesario.  
​![Actualizaciones](img/debianconfiguraciondegestiondepaquetes.png)

## **8\. Selección de programas**

Marco únicamente el entorno de escritorio deseado y "Utilidades estándar del sistema", para evitar servicios innecesarios y reducir superficie de ataque.  
​![Programas](img/debianselecciondeprogramasainstalar.png)

## **9\. Instalación del cargador de arranque GRUB**

Instalo GRUB en /dev/sda, el disco principal, para gestionar el arranque.

![Instalación GRUB](img/debianconfiguraciondegrub.png)
​

## **10\. Creación y verificación de contraseña de superusuario (root)**

Configuro correctamente la contraseña de root durante la instalación.  
​![Configuración](img/debiancontrasenasuperusuario.png)

## **11\. Mantenimiento del sistema: actualización de paquetes**

Tras la instalación, actualizo el sistema con:


`apt update && apt upgrade`

## **12\. Ocultación del menú de GRUB**

Edición de /etc/default/grub para ocultar el menú de arranque y reducir el vector de ataques físicos:


`GRUB_TIMEOUT_STYLE=hidden`  
`GRUB_TIMEOUT=0`  
![Time out](img/debiangrubtimeout.png)

![GRUB oculto](img/debiangruboculto.png)

​  
​

Actualizo la configuración:


`update-grub`

## **13\. Protección del GRUB con contraseña**

Genero el hash de la contraseña con:


`grub-mkpasswd-pbkdf2`

Modifico /etc/grub.d/40\_custom para definir usuario y hash:


`set superuser="NOMBRE"`  
`password_pbkdf2 NOMBRE HASH`

Actualizo GRUB:


`update-grub`

## **14\. Copias de seguridad de configuración del arranque**

Guardo copia de los principales archivos de configuración:


`cp /boot/grub/grub.cfg /boot/grub/grub.cfg.bak`  
`cp /etc/default/grub /etc/default/grub.bak`  
`cp /etc/grub.d/40_custom /etc/grub.d/40_custom.bak`

## **15\. Desactivar combinaciones de teclas peligrosas**

Desactivo la tecla Ctrl+Alt+Supr para evitar reinicios no autorizados:


`systemctl mask ctrl-alt-del.target`  
`systemctl daemon-reload`

## **16\. Justificación BIOS/UEFI**

No se protege la BIOS/UEFI ni el orden de arranque porque en VirtualBox no es posible implementar esta medida, pero se documenta que en hardware real se debería poner contraseña y bloquear arranque externo.