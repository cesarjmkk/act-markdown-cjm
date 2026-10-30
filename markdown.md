![Banner Ubuntu](assets/mi-imagen.png)

# Instalación de Ubuntu Desktop 24.04 LTS

Guía rápida de instalación y configuración inicial para el módulo de ASO.

## Preparación del sistema

Para instalar **Ubuntu 24.04**, arrancamos el equipo desde el medio de instalación en modo *UEFI* y verificamos la integridad del disco abriendo una terminal con `lsblk` antes de iniciar el asistente.

### Pasos de instalación

1. Seleccionar idioma y distribución del teclado.
2. Elegir instalación interactiva con software básico.
3. Definir el particionado del disco y crear el usuario administrador.
4. Reiniciar el equipo y retirar el medio de instalación.

Paquetes básicos a comprobar tras el primer inicio:

- `curl`: Descarga de recursos por terminal.
- `git`: Control de versiones.
- `build-essential`: Compiladores básicos del sistema.

---

## Actualización inicial post-instalación

Comandos ejecutados desde la terminal tras el primer arranque:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl git
```

---

## Enlaces

- Web oficial: [Descarga de Ubuntu 24.04](https://ubuntu.com/download/desktop).
- Configuración adicional: [docs/detalles.md](docs/detalles.md).

---

## Centro 

Práctica realizada en IES Clara del Rey, en Madrid:

![IES Clara del Rey](https://upload.wikimedia.org/wikipedia/commons/2/28/I.e.s._clara_del_rey_%28Prosperidad%2C_Madrid%29.jpg)

---

## Particionado recomendado

| Punto de montaje | Sistema de ficheros | Tamaño sugerido |
| :--- | :--- | :--- |
| `/boot/efi` | FAT32 | 512 MB |
| `/` (raíz) | ext4 | 40 GB |
| `/home` | ext4 | Resto del disco |
