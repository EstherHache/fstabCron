# fstabCron

## Ejercicio fstab

### A una máquina virtual de linux añadirle dos discos duros:

### Disco A

### Crear las siguientes particiones:

Linux --> usamos el comando (fdisk /dev/sdb) (siendo sdb el primer disco) 

~~~
partition type:
  p  primary (0 primary, 0 extended , 4 free)
  e extended
Select (default p): p
Partition number (1-4, default 1) :1
First sector (2048-20971519, default 2048) :
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-20971519, default 20971519):1000000
0

command (m for help): n 

partition type:
  p  primary (1 primary, 0 extended , 3 free)
  e extended
Select (default p): e
Partition number (1-4, default 2) :2
First sector (1000001-20971519, default 1000001) :
Using default value 1000001
Last sector, +sectors or +size{K,M,G} (10000001-20971519, default 20971519):
Using default value 20971519

command (m for help): w
The partition table has been altered!

Called ioctl() to re-read partition table.
Syncing disks.


~~~
Por defecto al crear la partición le da formato linux.

## Fat

~~~
root@ubuntu-sv:~# mkfs
mkfs        mkfs.ext2     mkfs.ext4dev    mkfs.msdos
mkfs.bef    mkfs.ext3     mkfs.fat        mkfs.ntfs
mkfs.cramfs mkfs.ext4     mkfs.minix      mkfs.vfat
root@ubuntu-sv:~# mkfs.fat /dev/
Display all 211 possibilities? (y or n)
root@ubuntu-sv:~# mkfs.fat /dev/sdb2
mkfs.fat 3.0.26 (2014-03-07)
mkfs.fa : Attempting to create a too large filesystem
root@ubuntu-sv:~#
~~~

### Disco B

Crear las siguientes particiones:

Linux --> usamos el comando (fdisk /dev/sdc) (siendo sdc el segundo disco) 

~~~
partition type:
  p  primary (0 primary, 0 extended , 4 free)
  e extended
Select (default p): p
Partition number (1-4, default 1) :1
First sector (2048-20971519, default 2048) :
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-20971519, default 20971519):7000000
0

command (m for help): n 

partition type:
  p  primary (1 primary, 0 extended , 3 free)
  e extended
Select (default p): e
Partition number (1-4, default 2): 2
First sector (7000001-20971519, default 7000001):
Using default value 7000001
Last sector, +sectors or +size{K,M,G} (70000001-20971519, default 20971519):
Using default value 20971519

command (m for help): n
partition type:
  p  primary (2 primary, 0 extended , 2 free)
  e extended
Select (default p): e
Partition number (1-4, default 3):
Using default value 3
First sector (14000001-20971519, default 14000001):
~~~


Por defecto al crear la partición le da formato linux.


## NTFS 
Damos el formato con este comando
~~~
root@ubuntu-sv:~# mkfs.fat /dev/sdc2
Cluster size has been automatically set to 4096 bytes.
Initializing device with zeroes: 100% - Done.
Creating NTFS volume structures.
mkntfs completed successfully. 
~~~

## Fat 
Damos el formato con este comando
~~~
root@ubuntu-sv:~# mkfs.fat /dev/sdc3
mkfs.fat 3.0.26(2014-03-07)
mkfs.fat: Attempting to create a too large filesystem
~~~

-Si queremos particionar un disco nuevo y formatear sus particiones se utiliza fdisk. 

-Modificamos el fichero fstab, añadiendo todas las particiones. 

-Las del disco A se montarán manualmente. Las del disco B se montarán automáticamente al arrancar.

### Editamos el fichero /etc/fstab

Añadiendo esto:

~~~
/dev/mapper/ubuntu--sv--vg-root /   ext4 errors=remount-ro 0            $

UUID=9b7bba1b-80fe-4b5c-a656-93aeefb08935 / boot      rxt 2 defaults    $  
/dev/mapper/ubuntu--sv--vg- swap_1 none        swap   sw            0   $

83c6a5e0-ce4b-4b27-9533-7db44bbe9f26  /media/discB1  ext4  noauto  0 0

a8331766-49cc-4b80-a787-789bc43e702f  /media/discB2  fat   noauto  0 0

/dev/sdc1   /media/discC1   ext4    auto    0     0

/dev/sdc2   /media/discC2   ntfs    auto    0     0

/dev/sdc3   /media/discC3   fat     auto    0     0

~~~



## Ejercicios cron.

Cada hora en punto ejecutamos la sincronización horaria y mandamos la salida a /dev/null/

Instalamos ntp 
~~~
(apt-get install ntp)
~~~

~~~
00 * * * * root ntpdate -u hora.rediris.es >> /dev/null/
~~~

Programar un trabajo (A) para ejecutarse en el minuto 30 de cada hora de cada día.

~~~
30 * * * * root echo "A" && date +%H:%M >> /etc/trabajo
~~~

Programar un trabajo (B) para ejecutarse cada día a las 20:30h.

~~~
30 20 * * * root echo "B" && date +%H:%M >> /etc/trabajo
~~~

Programar un trabajo (C) para ejecutarse de lunes a viernes a las 20:30h.

~~~
30 20 * * 1,2,3,4,5 root echo "C" && date +%H:%M >> /etc/trabajo
~~~

Programar un trabajo (D) para ejecutarse los martes y los jueves a las 20:30h.

~~~
30 20 * * 2,4 root echo "D" && date +%H:%M >> /etc/trabajo
~~~

Programar un trabajo (E) para ejecutarse los días 10 y 20 de todos los meses a las 20:30h.

~~~
30 20 10,20 * * root echo "E" && date +%H:%M >> /etc/trabajo
~~~

Programar un trabajo (F) para ejecutarse cada 15 minutos.

~~~
00,15,30,45 * * * * root echo "F" && date +%H:%M >> /etc/trabajo
~~~

Programar un trabajo (G) para ejecutarse cada día a las 00:00h.

~~~
00 00 * * * root echo "G" && date +%H:%M >> /etc/trabajo
~~~

Programar un trabajo (H) para ejecutarse cada primer día de mes a las 00:00h.

~~~
00 00 1 * * root echo "H" && date +%H:%M >> /etc/trabajo
~~~

