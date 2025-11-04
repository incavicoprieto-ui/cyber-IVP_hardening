## **Guía para Bastionar la BIOS/UEFI**

Garantizar la seguridad del equipo desde la BIOS/UEFI es esencial en cualquier entorno organizacional o personal, ya que muchas amenazas pueden aprovecharse de configuraciones por defecto. A continuación se explica, de forma práctica, cómo proteger firmemente tu sistema.

## **Contraseña de usuario o Power-On (Contraseña de arranque)**

1. **Ingresar a la BIOS/UEFI:**  
   Reinicia el equipo y durante los primeros segundos, según la marca, presiona repetidamente la tecla indicada (usualmente F2, SUPR, ESC o F10) hasta desplegar la configuración del firmware.  
2. **Ubica el menú de Seguridad (Security):**  
   Utiliza las flechas para navegar hasta encontrar el apartado **Security**.  
3. **Selecciona la opción de “Set Administrator Password”:**  
   Pulsa Enter y el sistema te pedirá que escribas una contraseña nueva. Vuelve a ingresarla para confirmarla. Se recomienda elegir una contraseña robusta.  
4. **Guarda los cambios antes de salir:**  
   Presiona F10 y elige “Save and Exit”.  
   **Resultado:** Al encender el equipo, deberás ingresar la nueva contraseña para iniciar el sistema operativo.  
   ![contraseña de usuario][img/bioscontrasena.png]

## **Contraseña de administrador (Supervisor Password)**

1. **Accede al menú de Seguridad dentro de la BIOS/UEFI:**  
   Normalmente se encuentra bajo el nombre **Security**.  
2. **Busca y configura la “Administrator Password”:**  
   Selecciona la opción, pulsa Enter y escribe una contraseña diferente y fuerte, que te permita modificar cualquier ajuste de la BIOS/UEFI. Confírma la contraseña.  
3. **Importante:**  
   Esta clave impide que otros usuarios accedan o alteren las opciones críticas del BIOS/UEFI, aunque puedan arrancar el sistema.

![supervisor password][img/biossetsupervisorpassword.png]

## **Arranques externos (bloquear arranque desde USB, CD/DVD, red)**

1. **Localiza el menú “Boot” o “Startup”:**  
   Dentro de la BIOS/UEFI, navega hasta la sección de prioridades de arranque.  
2. **Deshabilita el arranque desde dispositivos externos:**  
   Localiza las opciones tales como **USB Boot, CD/DVD Boot, Network/PXE Boot** y, una a una, cámbialas a "Disabled".  
3. **Opcional:**  
   Algunos equipos permiten deshabilitar puertos USB completamente o limitar su función sólo a teclado/ratón en el menú de **Security/Advanced**.

![control de arranque USB][img/bioscontrolarelarranque.png]

## **Orden de arranque (establecer un orden seguro)**

1. **Dentro del menú “Boot”, revisa el listado de prioridades:**  
   Usa las flechas o instrucciones indicadas para asegurarte de que Windows Boot Manager está en el primer lugar.  
2. **Baja o elimina de la lista otras opciones como CD/DVD/USB/Red:**  
   Así previenes que, si algún arranque externo se habilita por error, tenga prioridad sobre el disco principal.

![orden de arranque][img/biosordendearranque.png]

## **Secure Boot.**

Habilita “Secure Boot” dentro de la BIOS/UEFI para evitar que sistemas operativos no firmados puedan arrancar en el equipo.

![secure boot habilitado][img/biossecureboothabilitado.png]  

## **Otras opciones de seguridad recomendadas**

* TPM (Trusted Platform Module):  
  Activa el TPM si planeas usar cifrado a nivel del sistema operativo, como BitLocker. Esto se encuentra usualmente en “Security” \> “TPM”.​  
* Contraseña de disco (HDD/SSD Password):  
  Algunos equipos permiten proteger físicamente el disco duro con una contraseña independiente a la del BIOS. Esto impide que el disco se pueda leer, incluso si se extrae y monta en otro PC.​  
* Deshabilitar puertos o conectividad no utilizada:  
  Desactiva dispositivos integrados (WiFi, Bluetooth, lectores de tarjetas) si no se usan, desde el menú “Advanced” o “Integrated Peripherals”.  
* Desactivar CSM/Legacy Boot:  
  Esto fuerza al sistema a usar solo el modo UEFI, que es más seguro; se hace desde “Boot” o “Compatibility Support Module (CSM)”.​

## **Recomendaciones finales**

* Cambia las contraseñas periódicamente y nunca uses las predeterminadas.​​  
* Anota y resguarda las contraseñas en un lugar seguro.  
* Protege con la contraseña de administrador toda la BIOS, especialmente después de definir un arranque seguro y deshabilitar opciones externas.  
* Ante cualquier duda, consulta la documentación de tu fabricante para localizar los menús o términos exactos.

Esta metodología te permitirá asegurar la BIOS/UEFI de un equipo de forma robusta y siguiendo tanto los requisitos solicitados como las mejores prácticas actuales.​​



author: Inca Vico Prieto
summary: Guía para bastionado BIOS/UEFI
id: identificador-unico-del-codelab
categories: codelab,markdown
environments: Web
status: Published
feedback link: Un enlace en el que los usuarios puedan darte feedback (quizás creando un issue en un repositorio de git)
analytics account: ID de Google Analytics