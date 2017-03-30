# Sistemes RAID

#### Resum de sistemes RAID fent servir una taula com la vista a classe.

|         | Nº min de discs | Nº max de discs fallats | Capacitat    | Read | Write |
| ------- | :-------------: | :---------------------: | :----------: | :--: | :---: |
| Raid 0  | 2               | 0                       | 100%         | Ex   | Ex    |
| Raid 1  | 2               | 1                       | 50%          | MB   | Be    |
| Raid 5  | 3               | 1                       | 67%-94%      | MB   | Be    |
| Raid 6  | 4               | 2                       | 50%-%88      | Be   | Be    |
| Raid 10 | 4               | 1                       | 50%          | MB   | Be    |



#### Descripció de la metodologia utilitzada a classe per a fer proves amb màquines virtuals.

Per poder practicar lo de les Raids hem tingut que crear una maquina virtual en el virt-manager amb 3 discs durs extres per poder fer raids entre ells.


#### Comandes i descripció de les mateixes per tal de crear un sistema RAID 1

Crear raid 1: __mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb /dev/sdc__ Aquesa comanda creara una raid a /dev/md0  de nivell 1 on agafara els discs /dev/sdb i /dev/sdc


#### Comandes i descripció de les mateixes per tal de crear un sistema RAID 5

Crear raid 5: __mdadm --create /dev/md0 --level=5 --raid-devices=3 /dev/sdb /dev/sdc /dev/sdd__ Aquesta comanda creara una raid a /dev/md0 de nivell 5  on agafarà els discs /dev/sdb, /dev/sdc i /dev/sdd


#### Comandes i descripció de les mateixes per tal de crear un sistema RAID 6

Crear raid 6: __mdadm --create /dev/md0 --level=6 --raid-devices=4 /dev/sdb /dev/sdc /dev/sdd /dev/sde__ Aquesta comanda creara una raid a /dev/md0 de nivell 6 on agafarà els discs /dev/sdb, /dev/sdc, /dev/sdd i /dev/sde 


#### Comandes i descripció de les mateixes per tal de crear un sistema RAID 10

Crear raid 10: __mdadm --create /dev/md0 --level=10 --raid-devices=4 /dev/sdb /dev/sdc /dev/sdd /dev/sde__ Aquesta comanda creara una raid a /dev/md0 de nivell 10 on agafarà els discs /dev/sdb, /dev/sdc, /dev/sdd i /dev/sde
