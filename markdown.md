# Despliegue de un Servidor Nginx en IAW

Documentación para la puesta en marcha de un entorno web básico en el módulo de Implantación de Aplicaciones Web del IES Clara del Rey.

## Configuración y arranque del servicio

Para esta práctica montamos **Nginx** como servidor web principal sobre el sistema. El servicio se ejecuta en *segundo plano* gestionado por el demonio del sistema, y podemos validar que responde localmente ejecutando `curl -I http://localhost` desde la terminal.

### Comandos de instalación

A continuación se indican los comandos utilizados para instalar y dejar arrancado el servidor en una distribución basada en Debian/Ubuntu:

```bash
# Actualizar lista de paquetes e instalar nginx
sudo apt update
sudo apt install -y nginx

# Habilitar el arranque automático y comprobar el estado
sudo systemctl enable --now nginx
systemctl is-active nginx
```

---

## Verificación del entorno

Pasos seguidos para comprobar que el servicio funciona correctamente:

1. Verificar que el proceso está activo y sin fallos en el log.
2. Comprobar que el puerto 80 está escuchando conexiones TCP.
3. Abrir el navegador e ingresar a la dirección IP local para ver la página de bienvenida.

Rutas del sistema utilizadas en la configuración:

- `/etc/nginx/nginx.conf`: Archivo principal de configuración.
- `/etc/nginx/sites-available/`: Directorio con los bloques de configuración de sitios web.
- `/var/www/html/`: Directorio raíz donde se alojan los ficheros HTML a servir.

---

## Enlaces de referencia

- Documentación externa: [Guía oficial de Nginx](https://nginx.org/en/docs/).
- Documentación interna del proyecto: consultar más detalles sobre el entorno en [docs/detalles.md](docs/detalles.md).

---

## Recursos gráficos

### Imagen local del repositorio
Logotipo del servidor utilizado en la práctica, referenciado mediante ruta relativa:

![Logo Nginx](assets/mi-imagen.png)

### Sede del instituto (Wikimedia Commons)
Fotografía del IES Clara del Rey obtenida de Wikimedia Commons mediante su enlace directo:

![IES Clara del Rey](https://upload.wikimedia.org/wikipedia/commons/2/28/I.e.s._clara_del_rey_%28Prosperidad%2C_Madrid%29.jpg)

---

## Resumen de puertos y servicios

| Servicio | Puerto por defecto | Ruta / Parámetro principal |
| :--- | :--- | :--- |
| **HTTP (Nginx)** | 80 / TCP | `/var/www/html/` |
| **HTTPS (Nginx)** | 443 / TCP | `/etc/nginx/sites-available/default` |
| **SSH** | 22 / TCP | `/etc/ssh/sshd_config` |
