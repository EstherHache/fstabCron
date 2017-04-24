# fstabCron

## Ejercicio fstab

### A una máquina virtual de linux añadirle dos discos duros:

disco A

### Crear las siguientes particiones:

Linux --> usamos el comando (fdisk /dev/sdb) (siendo sdb el primer disco) imagen -->Por defecto al crear la partición le da formato linux.

~~~
partition type:
  p  primary (0primary, 0 extended , 4 free)
  e extended
Select (default p): p
Partition number (1-4, default 1) :1
First sector (2048-20971519, default 2048) :
Using default value 2048
Last sector, *

disco B

Crear las siguientes particiones:

Linux --> usamos el comando (fdisk /dev/sdc) (siendo sdc el segundo disco) imagen -->Por defecto al crear la partición le da formato linux.

NTFS imagen -->Damosel formato con el comando de la imagen(mkfs.ntfs /dev/sdc2)

Fat imagen -->Damosel formato con el comando de la imagen(mkfs.fat /dev/sdc3)

Para particionar un disco nuevo y formatearlos se utiliza fdisk. Modificar el fichero fstab, añadiendo todas las particiones. Las del disco A se montarán manualmente. Las del disco B se montarán automáticamente al arrancar.

imagen

Ejercicios cron.

Cada hora en punto ejecutamos la sincronización horaria y mandamos la salida a /dev/null/
 -->Instalamos ntp (apt-get install ntp)

--> 00 * * * * root ntpdate -u hora.rediris.es >> /dev/null/

Programar un trabajo (A) para ejecutarse en el minuto 30 de cada hora de cada día.

--> 30 * * * * root echo "A" && date +%H:%M >> /etc/trabajo

Programar un trabajo (B) para ejecutarse cada día a las 20:30h.

--> 30 20 * * * root echo "B" && date +%H:%M >> /etc/trabajo

Programar un trabajo (C) para ejecutarse de lunes a viernes a las 20:30h.

--> 30 20 * * 1,2,3,4,5 root echo "C" && date +%H:%M >> /etc/trabajo

Programar un trabajo (D) para ejecutarse los martes y los jueves a las 20:30h.

--> 30 20 * * 2,4 root echo "D" && date +%H:%M >> /etc/trabajo

Programar un trabajo (E) para ejecutarse los días 10 y 20 de todos los meses a las 20:30h.

--> 30 20 10,20 * * root echo "E" && date +%H:%M >> /etc/trabajo

Programar un trabajo (F) para ejecutarse cada 15 minutos.

--> 00,15,30,45 * * * * root echo "F" && date +%H:%M >> /etc/trabajo

Programar un trabajo (G) para ejecutarse cada día a las 00:00h.

--> 00 00 * * * root echo "G" && date +%H:%M >> /etc/trabajo

Programar un trabajo (H) para ejecutarse cada primer día de mes a las 00:00h.

--> 00 00 1 * * root echo "H" && date +%H:%M >> /etc/trabajo

El trabajo que se debe ejecutar es: Añadir al fichero /etc/trabajos (no existe hay que crearlo) el código del trabajo y la hora de ejecución.
