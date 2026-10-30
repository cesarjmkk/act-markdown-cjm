# Administración de Almacenamiento con LVM en Linux

Apuntes prácticos sobre la gestión de volúmenes lógicos (LVM) para el módulo de Administración de Sistemas Operativos (ASO).

## Introducción a LVM

En entornos de servidores, particionar discos de forma fija suele dar problemas cuando el almacenamiento se queda corto. Con **LVM (Logical Volume Manager)** desacoplamos el almacenamiento físico del sistema de ficheros, permitiendo redimensionar particiones en *caliente* sin necesidad de reiniciar la máquina, utilizando utilidades de consola como `lvextend` de forma sencilla.

---

## Flujo de trabajo y creación de volúmenes

Para configurar un nuevo volumen lógico desde cero, el orden de creación es el siguiente:

1. Inicializar el disco o partición como volumen físico (Physical Volume).
2. Crear o extender un grupo de volúmenes (Volume Group) que agrupe los discos físicos.
3. Crear el volumen lógico (Logical Volume) con el espacio deseado.
4. Dar formato al volumen lógico (por ejemplo, con `ext4` o `xfs`) y montarlo.

Conceptos clave del esquema LVM:

- **PV (Physical Volume):** Discos duros reales o particiones estándar (ej. `/dev/sdb1`).
- **VG (Volume Group):** Fondo común de almacenamiento que une uno o varios PVs.
- **LV (Logical Volume):** La partición virtual final sobre la que se crea el sistema de ficheros.

---

## Comandos de aprovisionamiento

Script básico en Bash para preparar un disco secundario `/dev/sdb`, crear un volumen lógico de 10 GB y dejarlo montado en `/data`:

```bash
#!/bin/bash
# Preparar el disco físico y el grupo de volúmenes
sudo pvcreate /dev/sdb
sudo vgcreate vg_datos /dev/sdb

# Crear un volumen lógico de 10G y darle formato ext4
sudo lvcreate -L 10G -n lv_almacen vg_datos
sudo mkfs.ext4 /dev/vg_datos/lv_almacen

# Crear punto de montaje y montar
sudo mkdir -p /data
sudo mount /dev/vg_datos/lv_almacen /data

# Comprobar el espacio disponible
df -hT /data
```

---

## Enlaces de referencia

- Documentación externa: [Guía de LVM en kernel.org](https://www.kernel.org/doc/html/latest/admin-guide/LVM.html).
- Parámetros avanzados y políticas de snapshot: [docs/detalles.md](docs/detalles.md).

---

## Recursos gráficos

### Imagen local (Assets)
Esquema y logotipo del sistema operativo sobre el que se realizan las prácticas:

![Tux Linux](assets/mi-imagen.png)

### Centro educativo (Wikimedia Commons)
Fotografía del IES Clara del Rey donde se imparte el ciclo de ASIR:

![IES Clara del Rey](https://upload.wikimedia.org/wikipedia/commons/2/28/I.e.s._clara_del_rey_%28Prosperidad%2C_Madrid%29.jpg)

---

## Comparativa de comandos LVM por capa

| Capa LVM | Comando de creación | Comando de visualización | Comando de eliminación |
| :--- | :--- | :--- | :--- |
| **Physical Volume (PV)** | `pvcreate` | `pvs` / `pvdisplay` | `pvremove` |
| **Volume Group (VG)** | `vgcreate` | `vgs` / `vgdisplay` | `vgremove` |
| **Logical Volume (LV)** | `lvcreate` | `lvs` / `lvdisplay` | `lvremove` |
