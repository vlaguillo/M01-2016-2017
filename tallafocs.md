# Tallafocs

## Tallafocs

### Què es un sistema tallafocs? Quina és la seva finalitat?
És un element de maquinari o programari utilitzat en una xarxa d'equips informàtics per controlar les comunicacions.

### Quines generacions de tallafocs hi ha hagut i què millorava cadascun?

__Primera generació: tallafocs de xarxa__
Millorava el filtratge per paquets

__Segona generació: tallafocs d'estat__
Implemena la colocació de cada paquet individual dintre d'una serie de paquets

__Tercera generació: tallafocs d'aplicació
Aquesta generació pot entendre certes aplicacions i protocols

### Quines capes té el model OSI?
1. Aplicació
2. Presentació
3. Sesió
4. Transport
5. Xarxa
6. Enllaç de dades
7. Fisica

### Quines capes té el model TCP/IP? En aquest cas feu una breu descripció de les funcionalitats de cada capa.
__Nivell d'aplicació__
Es el nivell que els programes mes habituals utilitzen per comunicar-se amb la xarxa

__Nivell de transport__
Pot solucionar problemes com la fiabilitat i seguretat de que les dades arribin al destí i ho fagin en l'ordre correcte

__Nivell d'interxarxa__
Soluciona els problemes de transportar paquets a una xarxa

__Nivell d'enllaç__
S'utilitza per passar paquets de la capa d'internet d'un dispositiu a la capa internet d'un altre

### A quina capa/capes sol treballar tradicionalment un tallafocs?
A la capa d'aplicació

## Tallafocs Linux

### Busqueu quins són els tradicionals sistemes de tallafocs incorporats en linux i anomeneu-los

En el Linux antic son les iptables i en el actual es diu firewall d

### Quins dels anteriors tallafocs estan instal.lats al fedora de classe? Com ho comproveu?
El firewalld esta instalat

### Algun dels anteriors tallafocs es troba activat?

### Instal.leu el servidor web httpd o nginx i activeu-ne el servei (dnf installl ...  ; systemctl ....). Indiqueu les comandes i comproveu que des d'una altra màquina podeu accedir via web a la vostra IP (digueu-li a un company). Hauria de sortir la plana per defecte.

### Activeu el servei firewalld. Indiqueu com ho feu.

### Comproveu si ara es pot seguir accedint.

## Win7

### Porta aquest SO algun tallafocs incorporat?
Si, el que ja ve per defecte 

### Arrenqueu una màquina win7 a isard.escoladeltreball.org

### Indiqueu com arribar al tallafocs (passos i pantalles)
1. Inicill
2. Panel de control
3. Sistema i seguretat
4. Firewall de Windows

### Es troba activat en aquest windows?
Si que es troba activat

### Busqueu un altre tallafocs per windows. Indiqueu la plana web i les prestacions que ens dona. Intenteu que NOMÉS sigui tallafocs.
__Tinywall__: Es un talla focs per a Windows i només necesita 1MB del teu disc dur. Funciona en segon pla per no molestar al usuari
