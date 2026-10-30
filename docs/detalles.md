# Detalles Técnicos y Políticas de LVM

Documento complementario con directrices para la administración de volúmenes en el módulo de Administración de Sistemas Operativos.

## Consideraciones sobre el Sistema

- **Distribución de referencia:** Debian 12 / Ubuntu Server 24.04 LTS
- **Paquete requerido:** `lvm2`
- **Herramientas de monitorización:** `lsblk`, `fdisk -l`, `df -hT`

---

## Políticas recomendadas en producción

1. **Margen en el Volume Group:** Dejar siempre al menos un 15-20% de espacio libre en el VG para permitir la creación de instantáneas (*snapshots*) previas a copias de seguridad o mantenimientos críticos.
2. **Redimensionado online:** En sistemas de archivos `ext4`, la ampliación de espacio se puede realizar en caliente ejecutando `lvextend -r` (el modificador `-r` ajusta el sistema de ficheros automáticamente mediante `resize2fs`).
3. **Persistencia en el arranque:** Todo volumen que deba montarse automáticamente al iniciar el servidor debe incluirse en `/etc/fstab` utilizando su UUID o la ruta persistente del dispositivo mapper.

---

[⬅ Volver al documento principal](../markdown.md)
