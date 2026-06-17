**Fecha:** Junio 2026 **Hardware:** Raspberry Pi 4 Model B 4GB + SanDisk Ultra 32GB

---
### Hardware utilizado

- Raspberry Pi 4 Model B 4GB RAM
- MicroSD SanDisk Ultra 32GB Clase 10
- Adaptador MicroSD incluido en el paquete
- Cable USB-C 5V 3A
- Portátil con lector de SD integrado

---
### Paso 1 — Flashear Ubuntu en la MicroSD

Se utilizó **Raspberry Pi Imager** descargado desde raspberrypi.com/software.
Configuración seleccionada:

- **Device:** Raspberry Pi 4
- **OS:** Ubuntu Server 24.04 LTS (64-bit)
- **Hostname:** aria-rpi
- **Usuario:** nadd
- **WiFi:** configurado durante el flash
- **SSH:** habilitado desde el imager

> Nota: Se instaló Ubuntu 24.04 en lugar de 22.04. ROS 2 Jazzy es compatible con ambas versiones.

---
### Paso 2 — Primer arranque y conexión SSH

Con la MicroSD insertada en la RPi y el USB-C conectado, se esperaron 3 minutos para el primer arranque.

Conexión desde PC Windows via PowerShell:
```bash
ssh nadd@aria-rpi.local
```

Resultado exitoso — Ubuntu 24.04.4 LTS operativo.

---
### Paso 3 — Actualización del sistema

```bash
sudo apt update && sudo apt upgrade -y
sudo reboot
```

---
### Paso 4 — Instalación de ROS 2 Jazzy

```bash
sudo apt install -y software-properties-common
sudo add-apt-repository universe
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
sudo apt update
```

---
### Problema encontrado — Dependencias rotas

Al intentar instalar `ros-jazzy-ros-base` se presentó un error de dependencias:

```
liblz4-dev : Depends: liblz4-1 (= 1.9.4-1build1) but 1.9.4-1build1.1 is to be installed
libzstd-dev : Depends: libzstd1 (= 1.5.5+dfsg2-2build1) but 1.5.5+dfsg2-2build1.1 is to be installed
```

**Causa:** Bug conocido de ROS 2 Jazzy en Ubuntu 24.04 arm64 — conflicto de versiones entre librerías del sistema actualizadas y las que ROS requiere estrictamente.

**Solución — Downgrade manual de librerías:**

```bash
sudo apt install liblz4-1=1.9.4-1build1 libzstd1=1.5.5+dfsg2-2build1 zlib1g=1:1.3.dfsg-3.1ubuntu2 -y --allow-downgrades
```

---
### Paso 5 — Instalación exitosa de ROS 2

```bash
sudo apt install ros-jazzy-ros-base -y
```

---
### Paso 6 — Configuración del entorno

```bash
echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

---
### Verificación

```bash
ros2 topic list
```

Resultado:

```
/parameter_events
/rosout
```

ROS 2 Jazzy operativo correctamente.

---
### Apagao seguro

```bash
sudo shutdown -h now
```

Esperar 30 segundos antes de desconectar el USB-C para evitar corrupción de la MicroSD.

---
### Estado final

- Ubuntu 24.04.4 LTS ✅
- ROS 2 Jazzy ✅
- SSH desde PC Windows ✅
- Listo para S3 del roadmap ARIA V2 ✅