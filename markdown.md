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
2. **Asignación de hardware:** Configurar la memoria RAM y los núcleos de CPU dedicados.
3. **Creación del disco virtual:** Asignar un disco duro virtual en formato VDI con almacenamiento dinámico.
4. **Arranque del instalador:** Iniciar la máquina virtual y seleccionar la opción *Try or Install Ubuntu* en el menú GRUB.
5. **Configuración del asistente:** Elegir idioma y teclado, marcar la instalación interactiva y seleccionar el particionado automático del disco virtual.
6. **Creación de la cuenta de usuario:** Definir el nombre del equipo, usuario y contraseña de administración para el acceso con permisos de superusuario.
7. **Finalización:** Esperar a que concluya la instalación, reiniciar la máquina y retirar el medio virtual.

Ajustes a comprobar tras el primer inicio:

- Instalar las **Guest Additions** de VirtualBox para mejorar la resolución de pantalla y la integración del ratón.
- Comprobar que la máquina virtual tiene conexión a Internet.
- Verificar que el usuario creado tiene permisos de administrador.

---

## Actualización del sistema

Una vez arrancado el sistema, abrimos la terminal (`Ctrl + Alt + T`) y ejecutamos los siguientes comandos para dejar el sistema actualizado:

```bash
# Actualizar los paquetes del sistema a su última versión
sudo apt update && sudo apt upgrade -y
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
