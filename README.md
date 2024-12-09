# P9

# Pasos previos

**Previo** Para esta práctica necesitaremos una máquina con docker compose instalado.

**Compose** Dentro del docker compose necesitaremos un conteendor que nos haga de servidor DNS y otro que contenga los servicios de apache.

# Creacción del compose

**Contenedor 1** -> en el primer contenedor definiremos el servidor apache que será donde guardaremos las páinas web que tenemos en local.

    Tendremos que definir dos volúmenes, que serán www (en donde guardamos el index de la página) y confApache (donde guardaremos la información y los alias de las páginas web)

**Contenedor 2** -> en el segundo contenedor definiremos aquel que va a actuar de DNS, para que esto funcione correctamente emplearemos una imagen de *bind9*. Tendremos también que darle una IP fija. 

    En este conteendor también definiremos dos volumenes, que serán conf (donde guardaremos la información de la configuración del DNS) y zonas (donde guardaremos las zonas de nuestro sitio).

**Network** -> Aquí crearemos la subred a la que se engancharán los contenedores lanzados, indicaremos el driver y la dirección de *gateway*.

# Configuración del DNS

Para configurar el DNS tendremos que tocar los archivos de este. Lo más importante es en el archivo *db.asircastelao* indicar al final la dirección IP del servidor DNS y el apache indicando el nombre de la página, ya que tenemos que dirigir el tráfico a este (en este caso pondremos las dos páginas aunque ambas se alojen en la misma IP).

# Configuración del Apache

**www** en esta carpeta tendremos que colocar los index de nuestras páginas dentro de carpetas dedicadas a cada página. En estos escribiremos directamente el código y css de estas.

**confApache** dentro de esta carpeta tendremos que dirigirnos a *sites-avaliable* y dentro de ella definiremos la configuración de la página. Tendremos que indicar el puerto donde se aloja, y sus alias para que puedan ser encontradas mediante url por nombre en lugar de por la IP.

# Paso final

Una vez terminado todo y configuradas nuestras páginas. Tendremos que abrur el archivo **/etc/systemd/resolved.conf** y en el tendremos que indicar que el resolutor de DNS será la IP que corresponde con nuestro servidor DNS, con todo esto configurado ya podremos buscar por nombre la página configurada y nos la encontrará el navegador web.