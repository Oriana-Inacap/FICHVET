#Configuracion Local

Este documento explicara los pasos para la configuracion local de este proyecto en ambiente Windows.  
  
Para poder generar su ambiente local requiere tener un *bundle* WAMP. WAMP es un acronimo que hace referencia a Windows, Apache, MySQL y PHP. Sin embargo, si lo desea puede utilizar XAMP donde la X representa un sistema operativo variable.  
  
En este documento veremos la instalacion de Wamp y las librerias que debera instalar. Partiremos con los requisitos para instalar WAMP:  

- Microsoft Visual C++ 2008 SP1 Redistributable Package
- Microsoft Visual C++ 2010 SP1 Redistributable Package
- Visual C++ Redistributable for Visual Studio 2012 Update 4
- Visual C++ Redistributable Packages for Visual Studio 2013
- Visual C++ Redistributable Packages for Visual Studio 2015-2019

Los links de descarga los puede encontrar [aqui](http://wampserver.aviatechno.net/?lang=en&prerequis=afficher). Favor notar que estan librerias existen para arquitecturas x86 y x64. Si usted posee una arquitectura x64 debe instalar las librerias asociadas tanto a x86 como a x64.  

Una vez realizado eso puede descargar WAMP desde [aqui](https://sourceforge.net/projects/wampserver/files/WampServer%203/WampServer%203.0.0/wampserver3.1.7_x64.exe/download) para x64 o [aca](https://sourceforge.net/projects/wampserver/files/WampServer%203/WampServer%203.0.0/wampserver3.1.7_x86.exe/download) para x86.
La instalacion de WAMP es bastante estandar por lo que no se detallara en este documento el proceso.  
  
Una vez instalado WAMP, en orden de verificar su instalacion, debe acceder (en su navegador) a la IP 127.0.0.1 y debe visualizar la pÃ¡gina principal de WAMP. **NOTA: Para que esto funcione se debe ejecutar el programa.**

Para poder clonar este proyecto debe instalar git. Los instaladores estan [aqui](https://github.com/git-for-windows/git/releases/download/v2.21.0.windows.1/Git-2.21.0-32-bit.exe) para x86 y [aca](https://github.com/git-for-windows/git/releases/download/v2.21.0.windows.1/Git-2.21.0-64-bit.exe) para x64.  

Luego debe instalar en su equipo composer. Composer es un gestor de dependencias para PHP y es usado por Laravel. Puede descargar composer desde [aqui](https://getcomposer.org/Composer-Setup.exe) e instalelo de forma normal (**NOTA: Es un solo instalador para arquitecturas x86 y x64**). Por ultimo debera instalar Node desde [aca](https://nodejs.org/dist/v10.16.0/node-v10.16.0-x86.msi) para x86 o [aca](https://nodejs.org/dist/v10.16.0/node-v10.16.0-x64.msi) para x64. Nuevamente la instalacion es bastante directa y sin mayores dificultades, por lo que no se daran detalles. Node es utiliado por Laravel para compilar recursos asociados a CSS y JS.

Luego puede clonar este proyecto. Esto se realiza desde la consola de comandos y el comando a ejecutar es `git clone {{URL}}`, donde debe reemplazar la variable `{{URL}}` por la URL de este repositorio. **NOTA: Donde lo clone se generara la carpeta indicada y quedara asociada la ruta, por lo que se recomiendo una vez clonado no reubicar el proyecto.**  

Luego debemos crear un vhost en Apache. Para esto acceda [aqui](http://127.0.0.1/add_vhost.php?lang=english) donde debera indicar el nombre de este vhost (se recomienda usar `fichvet.local`). Respecto del `path` acceda por explorador de windows a su proyecto clonado, ingrese a la carpeta application y luego public. Copie la ruta desde la ventana del explorador y peguela en l pagina web. Una vez ingresados ambos datos presione el boton que dice `Start the creation of the VirtualHost (May take a while...)`. Esto creara de forma efectiva el vhost en su maquina. Por ultimo, en los iconos cercanos al reloj (esquina inferior derecha) ubique el icono de WAMP, haga click con el boton derecho de su mouse y seleccione `Tools->Restart DNS`. Luego puede cerrar todas las ventanas abiertas.

Por consola acceda a la ruta de su proyecto, ingrese a la carpeta application, y ejecute el siguiente comando `composer update`. Esto descargara todas las dependencias utilizadas por Laravel. Una vez finalizado eso ejecute (en la misma ruta) `npm install` que compilara los recursos usando Node.

A continuacion con el editor de su preferencia acceda a la carpeta application de su proyecto. Debe copiar el archivo `.env.example` y pegarlo con nombre `.env`. **NOTA: No borre el archivo `.env.example`**. En este archivo copiado debera editar algunos campos:

- DB_DATABASE
- DB_USERNAME
- DB_PASSWORD

La base de datos debe crearla desde [PHPMyAdmin](http://127.0.0.1/phpmyadmin/). Utilice el charset utf8_general_ci. Si lo desea puede trabajar con su usuario `root` o generar un usuario particular con permisos globales para esta base de datos. Este proceso esta bastante documentado en Internet por lo que no entrare en detalles. En su archivo `.env` favor reemplazar el nombre de su base de datos en DB_DATABASE; su usuario, en DB_USERNAME; su contraseÃ±a, DB_PASSWORD.

Por ultimo debemos ejecutar desde consola (ubicados en la ruta de la carpeta application) dos comandos Laravel:

- `php artisan generate:keys`
- `php artisan migrate`

Esto inicializara la aplicacion y generarÃ¡ la BD. Ahora puede acceder por navegador al vhost creado y vera la aplicacion.
