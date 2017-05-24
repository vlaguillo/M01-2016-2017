# Gestió de volums lògics
---
### Que es el LVM
Es una capa d'abstracción entre un dispositiu d'emmagatzematge i un sistema de fitxers.

---
### Què volen dir les sigles, definició, analogies i exemples de comandes (explicant què fan) vistes a classe de: PV, VG, LV
+ __PV (Phisical Volume)__: Es un dispositiu d'emmagatzematge, pot ser un disc dur, una tarjeta SD, un floppy o un dispositu RAID. Alguns exemples de comandes son:
    + __pvcreate__: Crea un volum fisic
    + __pvs__: Llista tots els volums fisics que hi hagin en el sistema
   

+ __VG (Volume Group)__: Els VG son grups de diferents PV, per exemple serien com discs durs virtuals. Algunes comandes per els VG son:
    + __vgccreate__: Crea volums de grup
    + __vgs__: Llista tots els volums de grup que hi hagi en el sistema

+ __LV (Logical Volume)__: Son com el producte final dels LVM. Son aquests dispositius els que utilitzarem per a crear sistemas de fitxers, swap, discs per a máquinas virtuals... Exemples de comades per els LV:
    + __lvcreate__: Crea volums lògics
    + __lvs__: Llista tots els colums lògics que hi han en el sistema

---
### Entorn de pràctiques: Explicar com farem la pràctica detalladament (màquina virtual i afegir tres discs de 200M)
Per fer aquesta practica hem utilitzat una maquina virtual i a aquesta li hem afegit 3 discs de 200M cada un

### Pràctica 1: Creació d'un volum lògic a partir d'un dels tres discs durs (vda per exemple). Aquest volum lògic ha de ser del total de capacitat del disc. El volum de grup s'ha de dir practica1 i el volum lògic dades.
Primer creem els 3 PV amb la comanda __pvcrate__

    [root@localhost ~]# pvcreate /dev/vdc
    Physical volume "/dev/vdc" successfully created
    [root@localhost ~]# pvcreate /dev/vdd
    Physical volume "/dev/vdd" successfully created
    [root@localhost ~]# pvcreate /dev/vde
    Physical volume "/dev/vde" successfully created
    
Per comprovar de que tot s'ha creat correctament es te que executar un __pvs__

    [root@localhost ~]# pvs
    PV         VG     Fmt  Attr PSize   PFree  
    /dev/vdc          lvm2 ---  204,80m 204,80m
    /dev/vdd          lvm2 ---  204,80m 204,80m
    /dev/vde          lvm2 ---  204,80m 204,80m
    
Ara creem els VG amb la comanda __vgcreate__

    [root@localhost ~]# vgcreate practica1 /dev/vdc /dev/vdd /dev/vde
    Volume group "practica1" successfully created
    
Per comprovar de que tot es correcte farem un __vgs__

    [root@localhost ~]# vgs
    VG        #PV #LV #SN Attr   VSize   VFree  
    fedora      1   2   0 wz--n-   9,51g      0 
    practica1   3   0   0 wz--n- 600,00m 600,00m
    
Ara tenim que crear un volum lògic que ocupi el 100% del volum de grup. Per fer això tenim que utilitzar la comanda __lvcreate__

    [root@localhost ~]# lvcreate -l 100%FREE -n dades practica1
    Logical volume "dades" created.
    
Al posar el __100%FREE__ indiques de que utilitzi tota la capacitat del VG per crear el LV

Per comprovar de que l'has creat correctament utilitzaras las comanda __lvs__

    [root@localhost ~]# lvs
    LV    VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
    root  fedora    -wi-ao----   8,51g                                                    
    swap  fedora    -wi-ao----   1,00g                                     
    dades practica1 -wi-a----- 600,00m

---    
### Pràctica 2: Creació d'un sistema de fitxers xfs al volum lògic creat i muntatge a /mnt. També s'ha de crear un fitxer amb dd de 180MB
    
A continuacó tenim que fer un __mkfs.ext4__ per poder visualitzar les dades

    [root@localhost ~]# mkfs.xfs /dev/practica1/dades
  
   
Ara tenim que montar-ho
    
    mount /dev/practica1/dades /mnt

    
A continuacó creem un fitxer de 180MB amb la comanda __dd__

    [root@localhost ~]# dd if=/dev/zero of=test.img bs=180M count=1
    1+0 registros leídos
    1+0 registros escritos
    188743680 bytes (189 MB) copiados, 0,96184 s, 196 MB/s

---
### Pràctica 3: Creació d'un RAID 1 als dos discos sobrants (vdb i vdc per exemple)

Per crear un raid de nivell 1 utilitzarem la seguent comanda:

    [root@localhost ~]# mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/vdf /dev/vdg

A level li indicarem de quin nivell serà la RAID. A raid-devices indicarem el numero de discs que formaran el RAID i per finalitzar posarem els discs

---
### Pràctica 4: Ampliació del volum lògic de dades al raid
Primer creem un PV amb el RAID

    [root@localhost ~]# pvcreate /dev/md0
    Physical volume "/dev/md0" successfully created

Ara afegirem el PV del raid a un VG amb un __vgextend__ i despres a un LV amb __lvextend__

    [root@localhost ~]# vgextend /dev/practica1 /dev/md0
    Volume group "practica1" successfully extended

    [root@localhost ~]# lvextend /dev/practica1/dades /dev/md0
    Logical volume dades successfully resized.

### Pràctica 5: Ampliació del sistema de fitxers xfs al tamany actual del volum lògic dades (s'ha de poder fer sense desmuntar-lo de /mnt ja que és xfs). Una vegada creat crearem un nou fitxer de 180M.

Per ampliar el sistema de fitxer xfs tenim que executar la seguent comanda

    [root@localhost ~]# xfs_growfs /dev/practica1/dades

I per crear el fitxer

    [root@localhost ~]# dd if=/dev/zero of=test2.img bs=180M count=1

On bs es el tamany del fitxer i el count es el numero de fitxers que vols crear