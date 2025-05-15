
# Tarea 2.3: Montado de un sistema de ficheros con `chroot`

---

## Pasos de la tarea

---

### 1. Instalación desde cero de una máquina Debian

- Crear una nueva máquina virtual en VirtualBox.
- Instalar Debian desde la imagen `.iso`.
- Configurar los siguientes parámetros:
  - Idioma: Español
  - Teclado: Español
  - Zona horaria: tu región
  - Particionado guiado: todo en una sola partición
- Crear un usuario con tu nombre personal:
  - Nombre completo: Hugo
  - Nombre de usuario: hugo
  - Contraseña: (la que elijas) en este caso utilizaremos "abc123."

![imagen1](./Imagenes/1creacionmaquina.png)

![imagen2](./Imagenes/2creacionmaquina.png)

![imagen3](./Imagenes/3creacionmaquina.png)

![imagen4](./Imagenes/4creacionmaquina.png)

![imagen5](./Imagenes/5instalaciondebian.png)

![imagen6](./Imagenes/6instalacion.png)

![imagen7](./Imagenes/7instalacion.png)

![imagen8](./Imagenes/8instalacion.png)

![imagen9](./Imagenes/9instalacion.png)

![imagen10](./Imagenes/10instalacion.png)

![imagen11](./Imagenes/11instalacion.png)

![imagen12](./Imagenes/12instalacion.png)

![imagen13](./Imagenes/13instalacion.png)

![imagen14](./Imagenes/14instalacion.png)

![imagen15](./Imagenes/15instalacion.png)

![imagen16](./Imagenes/16instalacion.png)

![imagen17](./Imagenes/17instalacion.png)

![imagen18](./Imagenes/18instalacion.png)

![imagen19](./Imagenes/19instalacion.png)

![imagen20](./Imagenes/20InstalacionCompletada.png)

---

### 2. Configurar VirtualBox con la ISO de Kali Linux

- Apagar la VM si está encendida.
- Ir a `Configuración > Almacenamiento`.
- Añadir la imagen `.iso` de Kali Linux como unidad óptica.
- En `Configuración > Sistema > Orden de arranque`, colocar la unidad óptica antes que el disco duro.

![imagen21](./Imagenes/21DiscoKali.png)

![imagen22](./Imagenes/22discoKali.png)

![imagen23](./Imagenes/23discoKali.png)

![imagen24](./Imagenes/24discoKali.png)

---

### 3. Arrancar la máquina virtual desde Kali Linux Live

- Iniciar la máquina virtual.
- Kali Linux debería cargar como sistema Live.
- Abrir una terminal para realizar los pasos siguientes.

![imagen25](./Imagenes/25Kali.png)

![imagen26](./Imagenes/26Kali.png)

---

### 4. Comandos a ejecutar desde la terminal de Kali Linux

#### 4.1 Cambiar a castellano el teclado

```bash
loadkeys es
```
![imagen27](./Imagenes/27CambioTeclado.png)

---

#### 4.2 Acceder a la consola de root

```bash
sudo su
```
![imagen28](./Imagenes/28Root.png)

---

#### 4.3 Mostrar el sistema de ficheros montado

```bash
mount
```
![imagen29](./Imagenes/29Mount.png)

![imagen30](./Imagenes/30Mount.png)

---

#### 4.4 Listar la tabla de particiones del disco `/dev/sda`

```bash
fdisk -l /dev/sda
```

![imagen31](./Imagenes/31sda.png)

---

#### 4.5 Crear el directorio `/mnt/recuperar`

```bash
mkdir /mnt/recuperar
```
![imagen32](./Imagenes/32recuperar.png)

---

#### 4.6 Montar la partición 1 del disco duro en `/mnt/recuperar`

```bash
mount -t auto /dev/sda1 /mnt/recuperar
lsblk -f
```
![imagen33](./Imagenes/33mount.png)

![imagen34](./Imagenes/34Comprobacionmontaje.png)

---

#### 4.7 Montar `/dev` `/proc` `/sys` dentro de la ruta montada

```bash
mount --bind /dev /mnt/recuperar/dev
```
```bash
mount --bind /proc /mnt/recuperar/proc
```
```bash
mount --bind /sys /mnt/recuperar/sys
```
![imagen35](./Imagenes/35MontajeDPS.png)

---

#### 4.8 Crear una jaula con `chroot`

```bash
chroot /mnt/recuperar
```
Una vez dentro de la jaula:
- Estás trabajando directamente sobre el sistema Debian instalado.
- Puedes realizar tareas administrativas como cambiar contraseñas.
- Puedes realizar tareas varias como la creacion y edicion de archivos

Ejemplo: Creacion de archivo de texto en el directorio personal:

```bash
echo Hugo estuvo aqui > /home/hugo/prueba.txt
```
![imagen36](./Imagenes/36chroot.png)

#### 4.9 Desmontar los directorios utilizados

Salir de la jaula:

```bash
exit
```
Desmontar todo:

```bash
umount /mnt/recuperar/dev
umount /mnt/recuperar/proc
umount /mnt/recuperar/sys
umount /mnt/recuperar
```
![imagen37](./Imagenes/36umount.png)

---

### 5. Apagar y reiniciar el sistema Debian

- Apagar la máquina virtual:

```bash
poweroff
```
![imagen38](./Imagenes/37apagar.png)

- Quitar la ISO de Kali Linux desde la configuración de almacenamiento de VirtualBox.
- Reiniciar la VM.
- Iniciar sesión en Debian como usuario `hugo`.
- Verificar que existen las pruebas realizadas desde `chroot`:

```bash
ls /home/hugo
cat /home/hugo/prueba.txt
```
![imagen39](./Imagenes/38debian.png)

![imagen40](./Imagenes/39Comprobacionexistencia.png)

---

##  Conclusión

La práctica demuestra cómo se puede montar y recuperar un sistema Linux utilizando una distribución Live y el comando `chroot`, accediendo directamente al sistema de archivos montado desde otro entorno.
