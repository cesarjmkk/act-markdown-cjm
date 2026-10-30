![Banner Ubuntu](assets/mi-imagen.png)

# Instalación de Ubuntu Desktop 24.04 LTS en VirtualBox

Guía para la creación y configuración de una máquina virtual para el módulo de ASO.

---

## Recursos previos y especificaciones

Antes de iniciar la instalación de la máquina virtual, consulta los siguientes enlaces:

- Documentación y descarga: [Página oficial de descarga de Ubuntu 24.04](https://ubuntu.com/download/desktop).
- Requisitos de hardware y configuración del hipervisor: [docs/detalles.md](docs/detalles.md).

---

## Preparación del entorno de virtualización

Para desplegar **Ubuntu 24.04** en VirtualBox, descargamos la imagen ISO oficial, creamos una nueva máquina de tipo *Linux (64-bit)* y verificamos que la aceleración por hardware esté activa con el comando `vboxmanage --version` en el equipo anfitrión.

---

## Pasos para la instalación en la máquina virtual

El procedimiento completo para el despliegue dentro del hipervisor es el siguiente:

1. **Creación de la máquina virtual:** Abrir VirtualBox, pulsar en *Nueva*, asignar el nombre a la máquina y seleccionar la imagen ISO descargada.
2. **Asignación de hardware:** Configurar al menos 4 GB de memoria RAM y 2 núcleos de CPU dedicados.
3. **Creación del disco virtual:** Asignar un disco duro virtual en formato VDI de al menos 25 GB con almacenamiento dinámico.
4. **Arranque del instalador:** Iniciar la máquina virtual y seleccionar la opción *Try or Install Ubuntu* en el menú GRUB.
5. **Configuración del asistente:** Elegir idioma y distribución de teclado, marcar la instalación interactiva con utilidades mínimas y seleccionar el particionado automático del disco virtual.
6. **Creación de la cuenta de usuario:** Definir el nombre del equipo, nombre de usuario y contraseña de administración para el acceso por `sudo`.
7. **Finalización:** Esperar a que concluya el volcado de paquetes, pulsar en reiniciar y presionar *Enter* cuando el sistema solicite retirar el medio de instalación virtual.

Ajustes iniciales que debemos comprobar en la máquina tras el primer inicio:

- Instalar las **Guest Additions** de VirtualBox para habilitar pantalla completa y portapapeles bidireccional.
- Comprobar la conectividad de red con el comando `ip a` o `ping -c 3 8.8.8.8`.
- Asegurar que el usuario pertenece al grupo `sudo` para tareas administrativas.

---

## Actualización y paquetes básicos post-instalación

Una vez arrancado el sistema virtual, abrimos la terminal (`Ctrl + Alt + T`) y ejecutamos los siguientes comandos para actualizar el sistema e instalar utilidades básicas:

```bash
# Actualizar el índice de repositorios y paquetes del sistema
sudo apt update && sudo apt upgrade -y

# Instalar utilidades esenciales para administración en consola
sudo apt install -y curl wget git net-tools build-essential
```

---

## Particionado del disco virtual

Esquema de particionado aplicado automáticamente por el instalador sobre el disco VDI:

| Punto de montaje | Sistema de ficheros | Función principal |
| :--- | :--- | :--- |
| `/boot/efi` | FAT32 | Partición EFI para el cargador de arranque GRUB |
| `/` (raíz) | ext4 | Sistema operativo, librerías y aplicaciones |
| `/home` | ext4 | Directorios personales de los usuarios del sistema |

---

## Centro 

Práctica realizada en IES Clara del Rey, en Madrid:

![IES Clara del Rey](https://upload.wikimedia.org/wikipedia/commons/2/28/I.e.s._clara_del_rey_%28Prosperidad%2C_Madrid%29.jpg)
