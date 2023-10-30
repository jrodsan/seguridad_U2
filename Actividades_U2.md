## 2. Analiza y describe los sistemas biométricos que actualmente se están utilizando, así como los estudios de implantación de nuevas tecnologías respecto a este campo.

Los sistemas biométricos son una forma avanzada de autenticación e identificación que se basa en características únicas de las personas. Actualmente, se utilizan una variedad de sistemas biométricos y se están realizando investigaciones para mejorar y ampliar sus aplicaciones.

### Tipos de sistemas biométricos
1. **Rasgos Fisiológicos:** Estos incluyen huellas dactilares, geometría de la mano/dedo, iris, ADN, etc.
2. **Rasgos del Comportamiento:** Estos comprenden la voz, la firma, etc.

### Sistemas biométricos
1. **Reconocimiento de huellas dactilares:** Utiliza las características únicas de las huellas dactilares para la identificación.
2. **Reconocimiento facial:** Analiza características faciales para identificar a las personas.
3. **Reconocimiento de voz:** Se basa en patrones vocales para la autenticación.
4. **Reconocimiento de iris:** Escanea el patrón del iris del ojo para la identificación.
5. **Reconocimiento de venas de la palma:** Analiza las venas de la palma de la mano para la autenticación.
6. **Reconocimiento de escritura a mano:** Examina la escritura a mano para identificar a un individuo.
7. **Reconocimiento de ADN:** Utiliza el material genético para la identificación, aunque es menos común en aplicaciones cotidianas.

### Características de los sistemas biométricos
1. **Rendimiento:** Se refiere a la precisión del proceso de identificación. Los sistemas biométricos han mejorado en términos de precisión.
2. **Aceptabilidad:** La aceptación social y personal de los sistemas biométricos es importante. La comodidad y la percepción pública juegan un papel vital en su adopción.
3. **Evitabilidad:** La capacidad de eludir el sistema mediante procedimientos fraudulentos. Los sistemas biométricos deben ser resistentes a ataques como la suplantación de identidad.

### Estudios de implantación de nuevas tecnologías
- Continúan surgiendo avances en la precisión y la seguridad de los sistemas biométricos.
- La implantación de sistemas biométricos en dispositivos móviles y aplicaciones de la vida cotidiana está en constante crecimiento.
- Se están explorando aplicaciones en la atención médica, la banca y otros sectores.
- La regulación y la privacidad de los datos biométricos son temas importantes que se abordan a medida que se implementan nuevas tecnologías.

## 6. Configura y automatiza la copia de seguridad en un entorno linux de una estructura de directorios. Utiliza para ello el comando tar y el servicio crond – consideramos que la copia se realiza en el mismo equipo.

Primero he creado una estructura de directorios:

<p align="center">
    <img src="imagenes/A6_1.png" alt="captura1_actividad6" width="430" height="318">
</p>

A continuación creo el script que se usará para crear el backup en otra carpeta de destino.

<p align="center">
    <img src="imagenes/A6_2.png" alt="captura2_actividad6" width="416" height="190">
</p>

Después se le añaden permisos de ejecución con: **chmod +x backup_script.sh**

Podemos probar el script manualmente mediante **./backup.sh** lo que creará un archivo de respaldo en el directorio de destino indicado, en este caso “**Prueba_backup**”

Ahora podemos automatizar este proceso mediante el servicio cron, para ello modificamos el fichero crontab con **sudo nano /etc/crontab**

En este caso lo he programado para que se ejecute a las 10:10 de Lunes a Viernes, en el usuario usuario y señalando la ubicación del script.

<p align="center">
    <img src="imagenes/A6_3.png" alt="captura3_actividad6" width="498" height="348">
</p>

Cuando llega la hora establecida, comprobamos que efectivamente nos crea el archivo

<p align="center">
    <img src="imagenes/A6_4.png" alt="captura4_actividad6" width="403" height="158">
</p>

Podemos comprobar, extrayendo el archivo creado, que dentro está todo guardado correctamente.

<p align="center">
    <img src="imagenes/A6_5.png" alt="captura5_actividad6" width="460" height="148">
</p>

## Actividad 7.-Configura y automatiza la copia de seguridad en un entorno linux de una estructura de directorios, considerando que la copia se realiza en otro equipo linux/windows (host remote).

Hacemos lo mismo que en el ejercicio anterior, pero cambiándolo para que se guarde también en otra máquina, para ello tenemos que tener otra máquina en la misma red.

<p align="center">
    <img src="imagenes/A7_1.png" alt="captura1_actividad7" width="489" height="184">
</p>

Además, para que no pida contraseña al realizar el scp cuando se temporalice con el crontab, añadiremos la clave pública, para ello creamos una clave pública en la máquina remota con el comando: 

**ssh-keygen -t rsa**

y luego lo pasamos a la otra máquina con: 

**ssh-copy-id usuario@ip_del_servidor**

Además aquí se cambiaron los archivos /etc/hostname y /etc/hosts para poder conectar usando el nombre de la máquina, como podemos comprobar aquí, además de que ya no nos pide la clave para el ssh

<p align="center">
    <img src="imagenes/A7_2.png" alt="captura2_actividad7" width="481" height="273">
</p>

Ya no tendremos problemas para cuando se ejecute el scp programado.

Modificamos el archivo crontab una vez más, en este caso se programa de lunes a viernes a las 13:25 las copias de seguridad.

<p align="center">
    <img src="imagenes/A7_3.png" alt="captura3actividad7" width="456" height="321">
</p>

Así quedó el script a ejecutar al final, mediante uso de nombre de máquina:

<p align="center">
    <img src="imagenes/A7_4.png" alt="captura4actividad7" width="409" height="204">
</p>

Ahora comprobamos que se ejecute correctamente con el crontab:

<p align="center">
    <img src="imagenes/A7_5.png" alt="captura5actividad7" width="514" height="181">
</p>

Ya funciona correctamente la copia de seguridad en otro dispositivo.

## 8. Analizar, implementa, configura en un entorno Windows la herramienta rsync.

Rsync es una herramienta de línea de comandos utilizada para la sincronización y copia de archivos de forma eficiente en sistemas Unix y Linux. Sin embargo, Rsync no es una herramienta nativa en Windows, por lo que para usarla en un entorno Windows, hay que realizar una serie de pasos que implican la instalación de software adicional.

Para esta práctica he usado la herramienta Cygwin.

Los pasos que he seguido son:

1. Descargar el instalador de Cygwin desde el sitio web oficial: https://www.cygwin.com/.

2. Ejecutar el instalador descargado.

3. En la primera pantalla del instalador, seleccionar "Install from internet" y hacer clic en "Next".

4. Elegir la ubicación donde se desea instalar Cygwin y establecer el directorio de instalación. El directorio por defecto es "C:\cygwin64". Luego, hacer clic en "Next".

5. En la pantalla "Select Local Package Directory", se puede elegir dónde guardar los paquetes temporales descargados. Dejar el valor predeterminado y haz clic en "Next".

6. A continuación, se debe elegir un servidor de espejo para descargar los paquetes. Dejar la opción predeterminada seleccionada y hacer clic en "Next".

7. En la pantalla "Select Packages," se mostrará una lista de paquetes disponibles. Se busca y selecciona los siguientes paquetes marcándose con un clic en la columna "Skip" y escoger la versión más reciente:

rsync: Busca "rsync" y marca la última versión.
openssh: Busca "openssh" y marca la última versión.

8. Después de seleccionar los paquetes, haz clic en "Next" y se iniciará la descarga e instalación de los paquetes seleccionados.

Una vez se instale, abrimos el terminal de Cygwin

<p align="center">
    <img src="imagenes/A8_1.png" alt="captura1actividad8" width="547" height="367">
</p>

Comprobamos que se han instalado correctamente.

<p align="center">
    <img src="imagenes/A8_2.png" alt="captura2actividad8" width="522" height="547">
</p>

Si  se desea configurar Rsync con opciones específicas o configurar un servidor Rsync, se tendrá que crear un archivo rsyncd.conf en tu sistema. Por ejemplo, se puede configurar una sincronización bidireccional o establecer reglas de exclusión.

Ahora, si ya tenemos la máquina Windows y otra máquina, en este caso usaré un Ubuntu y tienen conexión entre ellos, probaremos a enviarle algo:

<p align="center">
    <img src="imagenes/A8_3.png" alt="captura3actividad8" width="622" height="506">
</p>

Como podemos comprobar, ha pasado el archivo exitosamente.

Ahora probaremos a hacerlo a la inversa, a copiar un archivo de Ubuntu a Windows.

<p align="center">
    <img src="imagenes/A8_4.png" alt="captura4actividad8" width="598" height="479">
</p>

Se completa satisfactoriamente la transferencia de archivos y vemos que se ha enviado correctamente.

## 9. Analizar, implementa, configura en un entorno linux la herramienta rsync.

Para esta práctica, utilizaré el script de la copia de seguridad en otro dispositivo (ejercicio 7) y lo usaré con el rsync.

Simplemente cambio la línea de scp por la nueva de rsync y queda así:

<p align="center">
    <img src="imagenes/A9_1.png" alt="captura1actividad9" width="589" height="412">
</p>

Ejecutamos el script:

<p align="center">
    <img src="imagenes/A9_2.png" alt="captura2actividad9" width="472" height="425">
</p>

Y efectivamente, en la máquina remota se crea el backup de la misma forma.

<p align="center">
    <img src="imagenes/A9_3.png" alt="captura3actividad9" width="617" height="251">
</p>

## 10. Configura y automatiza la copia de seguridad en un entorno linux de una estructura de directorios. Utiliza para ello el comando dd y el servicio crond – consideramos que la copia se realiza en el mismo equipo-. Considerar distintos programas de copia, cada uno de ellos con sus correspondientes momentos.

Para este ejercicio, he añadido un disco duro de 200MiB para realizar una copia de seguridad de disco, para ello se le engancha el disco duro al VirtualBox y le di una tabla de particiones gpt y cree una partición primaria con el disco (usando GParted).

Después de tener el nuevo /dev/sdb creé un script para la automatización de la copia de seguridad del disco.

<p align="center">
    <img src="imagenes/A10_1.png" alt="captura1actividad10" width="667" height="422">
</p>

Con eso nos creará la copia de seguridad en la ubicación y el nombre seleccionados, donde pondrá la fecha de la copia de seguridad.

Aquí hago una prueba manual de la ejecución y comprobamos que se crear correctamente la copia de seguridad.

<p align="center">
    <img src="imagenes/A10_2.png" alt="captura2actividad10" width="591" height="330">
</p>

Ya que el script contiene líneas con sudo, a la hora de configurar el crontab pondré como usuario root, para que cree sin problema el archivo, de otra manera no lo crearía.
Quedaría de esta manera, en esta ocasión lo he programado para que se ejecute a las 22:15 todos los días.

<p align="center">
    <img src="imagenes/A10_3.png" alt="captura3actividad10" width="606" height="435">
</p>

Como podemos comprobar, de esta manera automatizará bien el backup.

<p align="center">
    <img src="imagenes/A10_4.png" alt="captura4actividad10" width="712" height="395">
</p>

## 11. Investigar sobre AWS backup.

**Características de AWS Backup**

AWS Backup es una solución de gestión de respaldo de datos que ofrece una serie de características clave para garantizar la protección y disponibilidad de datos en entornos en la nube de AWS. Algunas de las características son:

**Gestión Centralizada:** AWS Backup permite la gestión centralizada de respaldos para múltiples servicios de AWS, lo que simplifica la administración de respaldos en un entorno diverso.

**Políticas de Respaldo:** Los administradores pueden definir políticas de respaldo personalizadas para cada servicio, lo que permite una mayor flexibilidad en la programación y retención de respaldos.

**Automatización:** AWS Backup ofrece programación automatizada de respaldos, lo que reduce la carga de trabajo manual y garantiza la coherencia en la ejecución de respaldos.

**Restauración Flexible:** Los datos respaldados se pueden restaurar de manera selectiva, lo que permite recuperar elementos específicos en lugar de restaurar todo el conjunto de datos.

**Auditoría y Cumplimiento:** AWS Backup registra las actividades de respaldo y proporciona información detallada sobre quién accede a los datos respaldados, lo que facilita el cumplimiento de regulaciones y políticas de seguridad.

**Comparación con Otras Soluciones de Respaldo**
En comparación con otras soluciones de respaldo en la nube y en las instalaciones, AWS Backup presenta ventajas significativas. La capacidad de gestionar respaldos de múltiples servicios de AWS en un solo lugar y la integración nativa con otros servicios de AWS son ventajas clave. Además, AWS Backup se beneficia de la infraestructura y la seguridad robusta de AWS.

Sin embargo, es importante señalar que AWS Backup puede no ser la solución óptima para todas las necesidades de respaldo. En algunos casos, soluciones especializadas pueden ofrecer características más avanzadas y precisas.

## 12. Configura y automatiza la copia de seguridad en un entorno linux de una estructura de directorios. Utiliza para ello el comando duplicity y el servicio crond – consideramos que la copia se realiza en el mismo equipo-.

Lo primero que hay que hacer es generar una clave gpg, aquí la creo yo:

<p align="center">
    <img src="imagenes/A12_1.png" alt="captura1actividad12" width="662" height="526">
</p>

Después de generar la clave, vemos la id de nuestra clave, la podemos ver mediante el siguiente comando:

<p align="center">
    <img src="imagenes/A12_2.png" alt="captura2actividad12" width="500" height="277">
</p>

Copiamos lo señalado y luego creamos el script y usamos el id:

<p align="center">
    <img src="imagenes/A12_3.png" alt="captura3actividad12" width="630" height="435">
</p>

Una vez lo tengamos hecho el script le damos permisos de ejecución con:

**sudo chmod +x backup_duplicity.sh**

Luego probamos la ejecución manual, y comprobamos que no haya errores.

<p align="center">
    <img src="imagenes/A12_4.png" alt="captura4actividad12" width="730" height="368">
</p>

Aquí comprobamos que se ha creado.

<p align="center">
    <img src="imagenes/A12_5.png" alt="captura5actividad12" width="602" height="180">
</p>

Ahora para automatizarlo añadimos la sentencia oportuna al crontab.

<p align="center">
    <img src="imagenes/A12_6.png" alt="captura6actividad12" width="556" height="335">
</p>

Aquí comprobamos que se crea el backup a la hora estimada.

<p align="center">
    <img src="imagenes/A12_7.png" alt="captura7actividad12" width="730" height="168">
</p>

<p align="center">
    <img src="imagenes/A12_8.png" alt="captura8actividad12" width="600" height="171">
</p>

## 22. Instalación y puesta en marcha de un sistema de almacenamiento compartido SAN. Utilizar Openfiler.
