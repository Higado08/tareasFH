# Tarea SSH y SCP
## Primero configuraremos las máquinas 
Las pondremos en una misma red interna que permita que se conecten para poder realizar la practica
![Imagen1](./SSH/1configA.png) ![Imagen2](./SSH/3ConfigB.png) </br>
Además cambiaremos el puerto destinado al ssh de la máquina B manteniendo el de A en el 2222
![imagen3](./SSH/3ConfigB.png)</br>
## Configuracion de Red
Configuramos las ip de las máquinas en este caso 192.168.100.20 para la maquina A </br>
![imagen4](./SSH/4ConfigredA.png) ![imagen5](./SSH/5RedA.png)</br>
Repetimos el proceso con la máquina B y la IP 192.168.100.30</br>
![iamgen6](./SSH/6ConfigredB.png) ![imagen7](./SSH/7RedB.png)</br>
Comprobamos que las maquinas pueden comunicarse facendo ping </br>
![imagen7.5](./SSH/7,5ComunicacionMaquinas.png)</br>
## Creacion de Usuarios
Creamos el usuario Alex para la máquina A y Brais para la B
![imagen8](./SSH/8CreacionAlex.png) ![imagen9](./SSH/9CreacionBrais.png)</br>
Nos conectamos a estes usuarios en cada una de las máquinas</br>
![imagen10](./SSH/10AccesoAlex.png) ![imagen11](./SSH/11AccesoBrais.png)</br>
## Conexion máquina A hacia B
Conectamos la máquina A mediante ssh a la máquina B con el usuario Brais recien creado</br>
![imagen12](./SSH/12ConexionBraisDesdeA.png)</br>
## Creamos un archivo de texto
Mediante comandos crearemos un archivo de texto en el directorio temporal y lo transmitiremos hacia el servidor (máquina B)</br>
![imagen13](./SSH/13CreacionFicherodesdeAySubirloaB.png)</br>
Repetimos el proceso en la máquina B </br>
![imagen14](./SSH/14Archivodesdeserver.png)</br> 
Y ahora lo llevamos hacia A </br>
![imagen15](./SSH/15Prueba2HaciaAlex.png)</br>
## Descraga en el anfitrion
Descargaremos los archivos generados anteriormente en el ordenador anfitrion concretamente en el escritorio en mi caso en ASIR107 que es mi usuario</br>
![imagen16](./SSH/16descargaanfitrion.png)</br>
Y comprobamos</br>
![imagen17](./SSH/17comprobaciondescarga.png)</br>
### 2ª Descarga en el anfitrion
Ahora en esta ocasion haremos uso de un bucle para la creacion de 200 archivos de texto que ma starde volcaremos sobrer el anfitrion</br>
![imagen18](./SSH/18creacionbrutaarchivos.png) ![imagen19](./SSH/19comprobacioncreacionarchivos.png)
Ahora descargamos en el anfitrion, que en mi caso cree una carpeta para que el escritorio no se llenase de elementos</br>
![imagen20](./SSH/20descargaarchivosenanfitrion.png) 
Y comprobamos</br>
![imagen21](./SSH/21ComprobacionArchivos200.png)</br>
## Clave de conexion 
Ahora crearemos una clave para evitar  utilizar constantemente la contraseña al conectarnos al servidor ssh en nuestro caso utilizaremos una clave sencilla para facilitar este proceso 
![imagen22](./SSH/22Clavedeconexion.png) </br>
Una vez hecha la compartiremos con el servidor</br>
![imagen23](./SSH/23copiadelaclaveenelserver.png)</br>
Y comprobamos si podemos hacer la conexion mediante el uso de la clave 
![imagen24](./SSH/24Comprobacionclavedeconexion.png)</br>
En este caso la crecaion de la clave la hacemos al final pero hacerla al principio tampoco supondria ningun tipo de inconveniente, con esto dasmos por finalizada la practica.
