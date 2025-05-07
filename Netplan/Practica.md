
#  Configuración de Red Interna en VirtualBox con Netplan y NetworkManager

## Objetivo

Configurar una red interna entre dos máquinas virtuales en VirtualBox utilizando direcciones IP estáticas, haciendo que la configuración sea persistente mediante `netplan` (máquina A) y `NetworkManager` (máquina B).

---

##  Paso 1: Clonar dos máquinas virtuales

- Usamos una máquina base con Ubuntu.
- Clonamos dos veces usando la opción de **clonado enlazado** y activamos la casilla **reinicializar direcciones MAC**.
- Nombramos las máquinas como `maquinaA` y `maquinaB`.

![Imagen1](./Imagenes/1ClonacionA.png)
![Imagen2](./Imagenes/3ClonacionB.png)
![Imagen3](./Imagenes/2clonacionEnlaceA.png)
---

## Paso 2: Configurar adaptadores de red

- En VirtualBox → Configuración de cada máquina:
  - Activamos el **Adaptador 2**.
  - Modo: **Red Interna**
  - Nombre: `intnet_FH`

![Imagen4](./Imagenes/4adaptador2deA.png)
![Imagen5](./Imagenes/5adaptador2deB.png)

---

## Paso 3: Asignar IPs estáticas (no persistentes)

### En máquina A:
![Imagen6](./Imagenes/6ConexionA.png)
![Imagen7](./Imagenes/7rootA.png)

```bash
sudo ip addr add 192.168.100.2/24 dev enp0s8
sudo ip link set enp0s8 up
```
![Imagen10](./Imagenes/10SegundaIpA.png)

### En máquina B:
![Imagen8](./Imagenes/8ConexionB.png)
</br>
![Imagen9](./Imagenes/9rootB.png)
```bash
sudo ip addr add 192.168.100.3/24 dev enp0s8
sudo ip link set enp0s8 up
```
![Imagen11](./Imagenes/11TerceraIPB.png)

---

##  Paso 4: Verificar conectividad con `ping`

Desde `maquinaA`:
```bash
ping 192.168.100.3
```
![Imagen12](./Imagenes/12PingDesdeA.png)

Desde `maquinaB`:
```bash
ping 192.168.100.2
```
![Imagen13](./Imagenes/13PingDesdeB.png)

---

##  Paso 5: Configuración persistente

###  Máquina A: Usando **Netplan**

1. Editamos el archivo:
```bash
sudo nano /etc/netplan/01-netcfg.yaml
```
![Imagen14](./Imagenes/14NetplanEdicionFichero.png)
2. Contenido del archivo:
```yaml
network:
  version: 2
  ethernets:
    enp0s8:
      addresses:
        - 192.168.100.2/24
      dhcp4: no
```
![Imagen15](./Imagenes/15EscrituraFicheroNetplan.png)
3. Ajustar permisos:
```bash
sudo chmod 600 /etc/netplan/01-netcfg.yaml
```

4. Aplicar configuración:
```bash
sudo netplan apply
```
![Imagen16](./Imagenes/16RestriccionPermisosNetplanYAplicamos.png)
![Imagen17](./Imagenes/17ComprobacionIpA.png)

---

###  Máquina B: Usando **NetworkManager (nmcli)**

1. Crear conexión:
```bash
nmcli con add type ethernet ifname enp0s8 con-name intnet-b ip4 192.168.100.3/24
```
![Imagen18](./Imagenes/18CreamosConexionB.png)
2. Activar conexión:
```bash
nmcli con up intnet-b
```
![Imagen19](./Imagenes/19ActivamosConexion.png)
3. Verificar:
```bash
ip addr show enp0s8
```
![Imagen20](./Imagenes/20Comprobamos.png)
---

##  Verificación final

- Ambas máquinas tienen IP estática correctamente configurada.
- Se pueden hacer ping entre sí incluso después de reiniciar.

![Imagen21](./Imagenes/21hacemosPingHaciaA.png)

---

## Conclusion

- Se conecta dos máquinas en red interna sin DHCP.
- Se usa `netplan` y `nmcli` para configuración persistente de red.
