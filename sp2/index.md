---
layout: default
title: "Sprint2: Instal·lació, Configuració de Programari de Base i Gestió de Fitxers"
---

# Sistemes de fitxers i particions
En aquest apartat es comentarà en primer lloc tot el relacionat amb els Sistemes de fitxers i les particions. En primer lloc es podria dir que el **Sistema de fitxers** és el conjunt de regles i estructures que utilitza el sistema operatiu per emmagatzemar, organitzar i accedir als fitxers dins d’un dispositiu d’emmagatzematge (com un disc dur, SSD o memòria USB). **Exemples**: FAT32, NTFS, ext4, HFS+, APFS, exFAT.

I les **Particions** son les divisions lògiques d’un disc físic que permeten separar dades o instal·lar diversos sistemes operatius. Cada partició pot tenir el seu propi sistema de fitxers.

## Mida sector

El **sector** és la unitat mínima física d’una unitat d’emmagatzemament on es guarden les dades. Per defecte són  512 bytes. És la mida més petita que el maquinari pot llegir o escriure directament.

## Mida block

El **bloc**, anomenat en sistemes operatius com Linux, o també anomenat **clúster** en sistemes operatius Windows, és la unitat lògica mínima amb què el sistema operatiu i el sistema de fitxers gestionen les dades.

Quan un fitxer s’emmagatzema, ocupa almenys un bloc complet.
* **Mida habitual:** 1 KB, 2 KB, 4 KB o 8 KB.
* **Controlat pel sistema de fitxers** (NTFS, ext4, FAT32...).
* **Es pot definir o modificar** quan es formateja el disc.
* **Cada bloc** està format per un o més sectors físics.
* **Mides grans** més velocitat amb fitxers grans.
* **Mides petites** millor aprofitament amb fitxers petits.

## Fragmentació interna

La **fragmentació interna** succeeix quan un fitxer no omple completament el bloc assignat. L’espai no utilitzat dins del bloc es perd, ja que el bloc no es pot compartir entre dos fitxers.

```
Exemple: un fitxer de 3 KB en un bloc de 4 KB deixa 1 KB desaprofitat.
Si hi ha molts fitxers petits, la pèrdua d’espai pot ser considerable.
```
Aquesta fragmentació és inevitable, ja que els blocs són d’una mida fixa. Els sistemes moderns intenten minimitzar-ne l’impacte ajustant la mida de bloc.

## Fragmentació externa

La fragmentació externa apareix quan un fitxer no pot ser emmagatzemat en blocs contigus, i el sistema ha de dividir-lo en diverses parts disperses pel disc. Això fa que el capçal del disc dur hagi de moure’s més per llegir el fitxer complet, reduint el rendiment.

```
En discs SSD, aquest problema no afecta gaire, ja que no hi ha parts mòbils. En disc durs mecanics, és recomanable fer desfragmentació periòdica per reorganitzar els blocs contigus. Tanmateix en les ultimes versions dels sistemes operatius ja no es tant necessari com en versions anteriors.
```

## Com mostra l'espai que ocupa un fitxer o directori al disc

Amb la comanda **du** (disk usage) es pot visualitzar l’espai que ocupa un fitxer o directori al disc. Per a poder-ho visualitzar s'ha creat un fitxer amb la següent comanda **touch hola**. Això crear un fitxer sense contingut, únicament hi ha el nom.

Després de crear-lo, a continuació amb la comanda du amb els següents paràmetres es podrà veure la següent informació.

![Imatge amb els parametres de la comanda du](../imatges/sprint2_01.jpg)

* **du -b hola**
   * Mostra la mida real en bytes del fitxer.
   * Vol dir que el fitxer ocupa 8 bytes reals de dades.
     Aquesta és la mida del contingut del fitxer, no l’espai reservat al disc.

* **du -sh hola**
   * **-s:** mostra només el total resumit (sense detallar carpetes internes)
   * **-h:** mostra la mida en format humà (K, M, G...).
Indica que el fitxer ocupa un bloc de 4 KB al disc, tot i que només té 8 bytes de dades. Això passa per la fragmentació interna: el sistema de fitxers reserva un bloc sencer (4 KB) per al fitxer encara que no l’ompli.

* **du -sbh hola**
    * **-s:** resum total.
    * **-b:** mostra la mida en bytes.
    * **-h:** mostra la mida humana (en aquest cas no té efecte perquè -b té prioritat).
 Igual que **du -b**, mostra els 8 bytes reals de dades.

* **du -bh hola**
    * Equivalent pràcticament a l’anterior (du -sbh).
    * Mostra la mida real del fitxer en bytes, però no la mida que ocupa al disc.

* **du -sb hola**
    * **-s:** només el total.
    * **-b:** en bytes exactes.
De nou, indica la mida real de dades, no la de l’espai ocupat.

## Tipus de formateig

El formateig és el procés que prepara un dispositiu d’emmagatzematge per poder-hi desar dades. Hi ha diversos nivells segons la profunditat de l’operació:

### Formateig de baix nivell

* Escriu els sectors físics i defineix com es divideix el disc en pistes i sectors.
* El realitza el fabricant o programes de manteniment especials.
* Només s’utilitza per recuperar discs defectuosos o en diagnosi.
* En discs moderns ja no és recomanable fer-lo manualment.

### Formateig de mig nivell

* Reorganitza les àrees del disc i pot marcar sectors danyats per evitar-ne l’ús.
* Antigament s’usava com a pas intermedi entre el baix i l’alt nivell.
* Actualment, la majoria de sistemes no fan distinció i integren aquesta tasca en el formateig d’alt nivell.

### Formateig d'alt nivell

* Crea el sistema de fitxers (FAT, NTFS, ext4...) i les seves estructures de control (taules d’arxius, inodes, etc.).
* És el formateig habitual que fem des de Windows, macOS o Linux.
* Elimina les dades lògiques, però no sempre les físiques, de manera que poden ser recuperables amb programes especials.

## Gestió de particions

La gestió de particions consisteix a crear, eliminar, redimensionar o modificar les particions d’un disc dur.

Objectius principals:
* Separar sistemes operatius o dades.
* Millorar l’organització i la seguretat.
* Preparar nous discs o recuperar espai.
* Crear esquemes GPT/MBR segons la necessitat.

Els sistemes operatius moderns permeten fer-ho tant des de gràfics (com GParted o Gestor de discs de Windows) com des de la línia de comandes (fdisk, parted...).

### Creació del disc dur virtual i afegir-lo a la màquina virtual Ubuntu

Per a realitzar la part de les particions i formatacions, en primer lloc, es crearà una unitat de disc dur virtual de 25 GB, s’afegirà a la màquina virtual, i posteriorment es crearà el particionat i formatatge corresponent

![Imatge amb les dades de creació del disc dur virtual](../imatges/sprint2_02.jpg)

Imatge amb les dades de creació del disc dur virtual de 25 GB així com el nom i ruta d'accés del mateix

![Imatge inserció disc dur creat a la maquina virtual](../imatges/sprint2_03.jpg)

Imatge com queda la configuració de la màquina virtual després d'afegir el segon disc dur per a poder fer la pràctica. A continuació, s'arranca la màquina virtual i es procedeix a la comprovació de què el disc dur afegit apareix com a afegit al sistema.

### Comprovació del disc dur al sistema

Per tal de comprovar que el disc dur esta disponible al sistema, en primer lloc s'obrira el terminal de l'Ubuntu i es posara la comanda **fdisk -l** per tal de poder comprovar que aquest apareix i en quina ubicació del sistema es troba.

![Imatge terminal comprovació ubicació del disc dur afegit](../imatges/sprint2_05.jpg)

Des del terminal s'ha pogut comprovar com el disc dur creat apareix correctament al sistema, però com és normal cal preparar-lo per a treballar amb ell. Com es pot apreciar a la imatge, el disc dur apareix a la ruta **/dev/sdb**. Amb aquesta dada, ja es pot començar amb el particionat del disc i posterior formatatge.

També en aquest cas, com que es disposa de l'aplicació Gparted, també s'ha realitzat la mateixa comprovació però en aquest cas en format gràfic, i també ens mostra la mateixa informació que el terminal.

![Imatge gparted amb el disc dur sense particionar](../imatges/sprint2_04.jpg)

Comprovat que el nou disc dur ja està disponible, i que aquest es troba com a **/dev/sbd/**, es procedeix a la creació de les particions.

### Creació de les particions al nou disc dur

Comprovada la ubicació del disc dur es procedeix a la creació de les particions utilitzant la comanda **fdisk**.

![Imatge amb la creació de les particions al disc dur](../imatges/sprint2_06.jpg)

Les comandes utilitzades han estat les següents:
* **n:** Per a crear una partició nova
* **p:** Per a crear una partició primària
* **Número partició:** 1 per defecte en aquest cas, ja que és la primera que es realitza.
* **Primer sector:** per defecte, 2048 que es on comença el disc
* **Últim sector:** 26000000 al particionar el disc en dos, inicialment posem la meitat del disc aproximadament
I amb això ja tindríem la primera partició creada.

A continuació es crea la segona partició continuant des de dintre de la comanda fdisk ja que no cal sortir-ne.

![Imatge de la creació de la segona particio del disc dur](../imatges/sprint2_07.jpg)

En aquest cas comencem de nou amb els mateixos passos que en el pas anterior.
* **n:** crear nova partició
* **p:** per a crear novament una partició primària
* **Número de partició:** 2 per defecte, ja que ja l'aplicació ja detecta que tenim la primera creada.
* **Primer sector:** en aquest cas ens mostra 260001408 que és on ha acabat la primera partició. 
* **Last sector:** en aquest cas ja és el final del disc dur i es polsa intro, ja que és el valor predeterminat i el correcte a inserir en aquest cas.

![Imatge aplicacio comanda per sortir de fdisk](../imatges/sprint2_08.jpg)

Després d’això ja tindríem les dues particions creades, únicament ens quedaria aplicar la comanda **w** per tal d’aplicar els canvis i sortir de la comanda fdisk

Després de realitzar aquests canvis es torna a posar la comanda fdisk -l per a comprovar com s’han realitzat els canvis al disc dur i on han d’aparèixer les dues particions creades si tot ha anat correctament.

![imatge amb la comprovacio de la creació de les particions del disc dur](../imatges/sprint2_09.jpg)

A la imatge es pot apreciar com al disc dur de 25 GB i que es troba a **/dev/sdb** ja apareixen les dues particions creades tal com s’ha realitzat amb la comanda **fdisk**. Però també una informació que ens mostra la comanda és la mida dels **sectors** del disc el qual ja ens mostra que els sectors o clústers són de **512 bytes**.

![Imatge amb la comprovació de la creació de les particions des de Gparted](../imatges/sprint2_10.jpg)

Si es volgués comprovar l’estat del disc dur per l’entorn gràfic, es tornaria a entrar a l’aplicació **Gparted** i després d’escollir el segon disc dur, aquest ja ens mostra correctament també la creació de les dues particions.

**Amb el particionat de discs** com es pot apreciar, tant es pot fer per **entorn gràfic** mitjançant amb aplicacions com **Gparted com pel terminal**, però s’ha de saber una cosa important que és per exemple que amb **Gparted no es pot modificar la mida del bloc**. Això vol dir que les aplicacions d’entorn gràfic no tenen les mateixes funcionalitats que les de línia d'ordres com fdisk.

## El proces de formatació del disc dur

Un cop s’ha dividit el disc dur en particions, és necessari formatejar-les abans de poder-les utilitzar. El formateig és el procés que **crea l’estructura lògica** (sistema de fitxers) que permet al sistema operatiu organitzar i desar dades dins de la partició.

Per tant, l’ordre correcte és:
* **Particionar el disc:** definir les àrees on s’emmagatzemaran dades o sistemes operatius.
* **Formatejar cada partició:** crear-hi el sistema de fitxers (com ext4, NTFS, FAT32...).
Sense aquest segon pas, el sistema operatiu no pot reconèixer ni utilitzar l’espai del disc.

![Imatge del formateig de la primera particio del disc dur](../imatges/sprint2_11.jpg)

Per al formatatge de la primera partició i tal com s’aprecia a la imatge s’ha creat un sistema de fitxers **ext4** propi dels sistemes Linux. En aquest cas s’ha utilitzat el paràmetre -b 2048 que defineix la mida de bloc del sistema de fitxers a 2048 bytes en lloc del valor predeterminat de 4096 habitual en ext4. 

D’aquesta manera, cada bloc del sistema de fitxers pot emmagatzemar fins a 2 KB de dades, fet que pot millorar l’aprofitament de l’espai en fitxers petits, pero empitjorar-lo en algunes altres.

La comanda utilitzada ha estat: 
* sudo mkfs.ext4 -b 2048 /dev/sdb1

Formatada la primera partició amb un sistema de fitxers **ext4** de sistemes Linux, a continuació es procedirà al formatatge de la segona partició, que en aquest cas es realitzarà amb un sistema de fitxers **NTFS** propietari dels sistemes operatius Windows

![Imatge del formateig de la segona partició del disc amb el sistema NTFS](../imatges/sprint2_12.jpg)

En aquest cas el formatatge s’ha realitzat amb els paràmetres per defecte. Com es pot apreciar a la imatge la mida del bloc o clúster és de **4096 bytes**, que és la mida per defecte que s’apliquen als sistemes de fitxers NTFS.

En aquest cas la comanda utilitzada per al formateig a estat:

* sudo mkfs.ntfs /dev/sdb2

Si es volgués comprovar que el formatatge ha estat correcte i no hem realitzat cap error, es podria utilitzar la comanda **lsblk -f** la qual mostra totes les unitats del sistema aixi com la informació del sistema de fitxers.

![Imatge de la comanda lsblk -f amb el resultat per al disc dur](../imatges/sprint2_13.jpg)

A la imatge es pot apreciar com si ens centrem en el disc dur /dev/sdb, ens apareixen les dues particions existents així com el seu sistema de fitxers de cadascuna. Però, per als que els agrada l’entorn gràfic, també es pot comprovar el resultat del formatge així com de les particions des de l’aplicació Gparted.

![Imatge final de les particions i formatatges amb Gparted](../imatges/sprint2_14.jpg)

A la imatge, es pot apreciar com Gparted mostra les particions existents així com el sistema de fitxers de cadascuna d’elles.

## Observació dels valors existents a les particions creades

Arribats aquí, ja estan les dues particions amb els seus sistemes de fitxers creats, per la qual cosa ja tenim el disc dur apunt per a ser utilitzat i afegir les dades necessàries. Per acabar i per a comprovar tot el que s’ha vist fins aquí, ens queda visualitzar com han quedat els valors al final de tot el procés.

Per exemple per a poder veure els valors que hi ha a una partició amb format **ext4** com es el cas, es pot utilitzar la comanda **tune2fs**, que permet mostrar tots els valors com ara la mida dels blocs. Per a veure el resultat, la comanda seria:
* sudo tune2fs -l /dev/sdb1 | grep Block

![Imatge amb els valors de la comanda tune2fs](../imatges/sprint2_15.jpg)

Amb aquesta comanda es pot apreciar el seguent:
* **Block count: 6499488**
Indica el nombre total de blocs que té el sistema de fitxers dins d’aquesta partició que en aquest cas es de 6499488
* **Block size: 2048**
Mostra la mida de cada bloc lògic del sistema de fitxers (definit en el moment del formateig), en aquest cas 2048. Per defecte, en ext4 la mida és 4.096 bytes (4 KB), però aquí s’ha canviat manualment amb el paràmetre -b 2048 al realitzar el formateig
* **Blocks per group: 16384**
Indica quants blocs formen cada grup de blocs dins del sistema de fitxers ext4. En ext4, els blocs s’organitzen en grups per millorar l’eficiència de la gestió i reduir la fragmentació. Aquí, cada grup conté 16.384 blocs (és a dir, 16.384 × 2.048 = 33.554.432 bytes ≈ 32 MB per grup).

Si el que es vol veure és la informació sobre el **sistema de fitxers NTFS** és necessària una altra comanda, ja que la primera com ja s’ha dit només es valida per a sistemes de fitxers **ext4**. La comanda a utilitzar finalment ha estat:
* sudo ntfsinfo -m /dev/sdb2 | grep -A 15 "Volume Information"

![imatge per a visualitzar les dades del sistema de fitxers NTFS](../imatges/sprint2_16.jpg)

Tal com s’aprecia a la imatge es pot apreciar entre altres que la mida del **sector físic és de 512 bytes** que és el que ha agafat al crear la partició, mentre que la mida del **sector lògic ha quedat en 4096 bytes**. Això indica que un clúster (logic) agrupa diversos sectors físics per formar la unitat mínima que utilitza el sistema operatiu per desar un fitxer.

## Muntatge de particions al sistema

Quan es crea una nova unitat de disc a Linux, aquesta no és accessible directament pel sistema operatiu. Per poder accedir-hi i treballar amb els seus fitxers, cal muntar-la en un punt concret del sistema de fitxers.

Aquesta tasca es realitza mitjançant la comanda **mount**, que permet associar una partició o dispositiu amb un punt de muntatge (directori) dins de l’estructura del sistema. Un cop muntada, la unitat esdevé accessible com si fos una carpeta més del sistema.

A Linux, totes les unitats de disc formen part d’una única jerarquia de directoris.  Per aquest motiu, quan es crea una nova partició o s’afegeix un dispositiu d’emmagatzematge, aquest no és accessible automàticament fins que s’hi realitza el muntatge.

El muntatge consisteix a enllaçar el sistema de fitxers de la unitat amb un punt de muntatge dins de l’arbre principal (/). Això es pot fer manualment amb la comanda:

* sudo mount /dev/sdb1 /mnt

on /dev/sdb1 és la partició i /mnt és el directori on quedarà accessible. A partir d’aquest moment, el contingut de la unitat pot ser llegit i modificat com qualsevol altra carpeta del sistema.

Quan s’ha acabat de treballar amb una unitat o dispositiu muntat, és recomanable desmuntar-lo correctament per assegurar que totes les dades s’hagin escrit al disc i evitar possibles errors o corrupcions. La comanda a utilitzar seria:
* sudo umount /dev/sdb1

Quan una unitat està desmuntada, ja no és accessible pel sistema operatiu fins que es torni a muntar. Si la unitat està en ús (per exemple, si hi ha un fitxer obert dins d’ella), la comanda umount mostrarà un error del tipus "target is busy". En aquest cas, cal tancar els fitxers o processos que l’estiguin utilitzant abans de desmuntar-la.

### Muntatge i desmuntatge manual

El muntatge manual es realitza mitjançant el terminal, utilitzant la comanda mount. En aquest cas la comanda seria:
* sudo mkdir /mnt/sdb1
* sudo mount /dev/sdb1 /mnt/sdb1

![Imatge de la comanda de muntatge manual](../imatges/sprint2_17.jpg)

Amb aquesta comanda s’indica al sistema que munti la partició **/dev/sdb1** al directori **/mnt/sdb1**, fent que el seu contingut sigui accessible des d’aquest punt del sistema de fitxers. És recomanable crear un subdirectori dins de **/mnt** amb el nom de la partició o un nom descriptiu, per tal de mantenir una estructura més clara i organitzada.

Així, la partició queda muntada en un directori específic, facilitant-ne la identificació i l’accés. En el cas del desmuntatge quan s’ha acabat de treballar amb la unitat muntada, és important desmuntar-la correctament per assegurar que totes les dades s’hagin escrit al disc i evitar possibles errors o corrupcions. La comanda a utilitzar seria.

* sudo umount /dev/sdb1

Quan es treballa amb muntatges manuals, cal tenir en compte que el **muntatge realitzat d’aquesta manera és temporal**, no queda registrat al sistema i, per tant, **desapareix automàticament en reiniciar l’equip**. Si es vol que una unitat es munti automàticament en cada inici, cal afegir-ne la configuració al fitxer fstab, on es defineixen els muntatges permanents.

![imatge amb el proces i muntatge comprovacio i desmuntatge d'una particio](../imatges/sprint2_18.jpg)

A la imatge es pot apreciar tot el procés de muntatge i desmuntatge de la partició **/sdb1** dintre de **/mnt**. Abans s’ha creat ja la carpeta sdb1. El procés es pot apreciar com un cop muntada la partició, aquesta si s’accedeix mostra el seu contingut (carpeta lost+found).

A continuació es procedeix al desmuntatge amb la comanda **umount**, però aquesta no ha estat permesa donat que estem a l'interior, no és possible desmuntar-la, per la qual cosa ja ens mostra l’error corresponent. Després de sortir-ne es torna a utilitzar la comanda umount aquesta vegada de forma correcta. En tornar a entrar a la carpeta **/mnt/sdb1**, ja es pot apreciar com ja no apareix la carpeta de la unitat i mostra el contingut de la carpeta **/mnt/sdb1** que en aquest cas no hi ha contingut.

Tot i que el muntatge manual es pot fer mitjançant la comanda mount des del terminal, els entorns d’escriptori moderns com GNOME, KDE Plasma o XFCE permeten muntar particions i dispositius externs gràficament, sense necessitat d’utilitzar ordres.

Quan es connecta un dispositiu (com una memòria USB o un disc dur extern), el sistema detecta automàticament la unitat i ofereix l’opció de muntar-la amb un sol clic des del gestor d’arxius (per exemple, Nautilus, Dolphin o Thunar). Un cop muntada, la unitat apareix en la barra lateral del gestor de fitxers i és accessible com qualsevol altra carpeta.

Internament, el sistema realitza el mateix procés que la comanda mount, però de manera automàtica i temporal. Aquest tipus de muntatge no és permanent i desapareix quan s’expulsa el dispositiu o s’apaga l’equip.

Quan es munta una unitat des del gestor d’arxius (com Nautilus a GNOME o Dolphin a KDE), el sistema utilitza un servei intern anomenat udisks2, que realitza la comanda mount automàticament amb permisos d’usuari, no de root.
Per defecte, les unitats muntades gràficament es col·loquen a:

* /media/jesus/sdb1/

Per a desmuntar només cal fer un clic amb el botó de la dreta al damunt de la unitat, i ja apareix la comanda per a desmuntar.

### Muntatge automàtic amb fstab

Per tal d’evitar haver de muntar manualment les unitats cada vegada que s’inicia el sistema, Linux utilitza un fitxer especial anomenat **fstab (File System Table)**. Aquest fitxer conté la informació necessària perquè el sistema operatiu munti automàticament les particions o dispositius en iniciar-se. Cada línia del fitxer fstab defineix una unitat, el seu punt de muntatge i les opcions associades. 

Tanmateix, el muntatge automàtic només té realment sentit en aquells casos en què la partició o unitat s’utilitza de manera continuada o permanent dins del sistema.  Per exemple, en particions que contenen directoris importants com /home, /var, /srv o carpetes de dades que el sistema o els serveis necessiten des del moment de l’arrencada.

En canvi, per a dispositius externs o d’ús esporàdic (com discs USB, discos durs externs o unitats de còpia de seguretat), no és recomanable afegir-los a fstab. En aquests casos, és preferible realitzar un muntatge manual quan sigui necessari, o deixar que l’entorn gràfic del sistema (GNOME, KDE, etc.) gestioni automàticament el muntatge quan es connecti el dispositiu.

![imatge de configuració del fitxer fstab](../imatges/sprint2_19.jpg)

A l'última línia del fitxer fstab es pot apreciar com s’ha afegit una línia amb els paràmetres mínims necessaris perquè el muntatge de la partició es realitzi de forma automàtica en iniciar el sistema. En aquest cas la línia inserida ha estat la següent.

* /dev/sdb1   /mnt/sdb1   ext4    rw,nofail 0   0

Els paràmetres utilitzats són els següents.
* **/dev/sdb1**	Indica quin és el dispositiu físic a muntar
* **/mnt/sdb1**	Indica el punt on es muntarà el disc a muntar
* **ext4** Indica el sistema de fitxers de la partició a muntar
* **rw,nofail**	Indica que es muntarà amb permisos de lectura i escriptura i que permet evitar els errors en cas que el disc no hi sigui
* **0 0**	indica Dump i fsck que no cal fer comprovacions d’arrancada.

Quan es treballa amb el fitxer /etc/fstab (File System Table) s’ha de tindre molta cura, ja que és el responsable d’indicar al sistema quines particions, dispositius o unitats de xarxa s’han de muntar automàticament en iniciar Linux, i en quin punt del sistema de fitxers s’han de connectar.

Cada línia del fitxer defineix una entrada de muntatge amb diversos paràmetres: el dispositiu o UUID, el punt de muntatge, el tipus de sistema de fitxers i les opcions de muntatge. Tot i ser molt útil, editar el fitxer fstab pot comportar certs riscos si no es fa correctament.

Si el directori especificat com a punt de muntatge no existeix, el sistema no podrà muntar la partició i mostrarà un error. Crea el directori abans de muntar. Si la unitat és externa o no sempre està present, cal afegir l’opció nofail a la línia del fstab. Això evita que l’arrencada s’aturi si el dispositiu no es troba. Un sol espai de més o un camp mal escrit pot fer que el sistema no pugui llegir correctament fstab i no arrenqui

Algunes opcions poden restringir l’accés o fer que el sistema no pugui escriure al dispositiu (ex: ro = read-only, noexec, etc.). El fitxer /etc/fstab és una eina molt potent que permet automatitzar el muntatge de particions, però també pot ser una font de problemes si s’edita sense precaució.

## Fragmentació dels sistemes de fitxers (ext4 i NTFS)

La fragmentació és un fenomen que es produeix quan les dades d’un fitxer no s’emmagatzemen de manera contigua al disc, sinó disperses en diferents blocs o clústers. Això pot afectar el rendiment d’accés als fitxers, especialment en discs durs mecànics (HDD).

Tot i que la fragmentació pot aparèixer en qualsevol sistema de fitxers, el seu impacte i gestió varien segons el tipus: NTFS (Windows) i ext4 (Linux).

Com ja s’ha comentat al principi del document existeix la fragmentació interna es la que es produeix dins dels blocs o clústers. Succeeix quan un fitxer no omple completament el bloc assignat, deixant espai desaprofitat dins d’ell.
I per l’altre costat està la fragmentació externa que apareix quan els fitxers es divideixen en fragments que es guarden en blocs no contigus al disc. Això passa quan s’esborren o creen molts fitxers i l’espai lliure es dispersa, etc.

### Fragmentació en NTFS (Windows)

NTFS tendeix a fragmentar-se amb el temps perquè:
* No sempre pot col·locar els fitxers grans en blocs contigus.
* L’espai lliure es fragmenta amb les operacions d’escriptura i esborrat.

Windows inclou una eina de desfragmentació automàtica (“Desfragmentar i optimitzar unitats”). En discs SSD, aquesta eina no desfragmenta sinó que executa l’ordre TRIM, que optimitza l’ús dels blocs.

### Fragmentació en ext4 (Linux)

El sistema de fitxers ext4 està molt optimitzat per evitar la fragmentació externa pel següent:
* Reserva espai addicional entre fitxers per permetre que puguin créixer sense trencar la contigüitat.
* Utilitza un sistema anomenat extents, que guarda trams contigus de blocs junts.
* Distribueix els fitxers en diferents grups de blocs per minimitzar la fragmentació.
En ús normal, ext4 manté una fragmentació inferior al 2%, fins i tot després de molt temps. Amb ext4, no cal desfragmentar manualment, tot i que existeixen eines com e4defrag per optimitzar un sistema molt ple o molt antic.

### La comanda e4defrag

Com ja s’acaba de dir, per a desfragmentar una unitat amb **ext4** hi ha la comanda **e4defrag**. Aquesta comanda funciona de manera que si detecta que la unitat no necessita desfragmentació, no realitza cap moviment, i si aquesta detecta una fragmentació excessiva, aquesta realitza una desfragmentació de la partició. La comanda per aplicar-la seria la següent:

* sudo e4defrag -c /mnt/sdb1

![Imatge amb el resultat de la comanda e4defrag](../imatges/sprint2_20.jpg)

El sistema de fitxers està completament optimitzat, e4defrag ha analitzat tots els fitxers dins de **/mnt/sdb1** i ha trobat que cap d’ells no està dividit en blocs separats.

## Particions i volums

Quan es parla de particions i volums cal, en primer lloc, tindre clar el concepte de cada cosa. Per un costat hi ha la partició, aquesta és una divisió lògica dins d’un dispositiu d’emmagatzematge físic (com un disc dur, SSD o memòria externa). Mitjançant el particionat, es pot organitzar millor l’espai del disc, separant dades o sistemes diferents dins del mateix dispositiu. 

Cada partició es comporta com si fos un disc independent i pot tenir el seu propi sistema de fitxers (NTFS, ext4, FAT32, etc.). Per exemple, un mateix disc físic pot tenir una partició per al sistema operatiu i una altra per a les dades de l’usuari.

I per l’altre costat es troben els volums, un volum és una unitat lògica d’emmagatzematge que el sistema operatiu pot muntar i utilitzar per llegir o escriure dades. És el que l’usuari veu com una unitat accessible (com ara C:, D: o /home). Cada volum correspon, generalment, a una partició, però també pot estar format per diverses particions o diversos discs combinats.

Per tant, per a entendre les diferències entre una relació i una partició i un volum es pot dir el següent:
* Una partició és una divisió del disc físic.
* Un volum és la unitat lògica creada a partir d’una o més particions.
* Normalment, hi ha una relació d’1 a 1 (una partició = un volum), però en sistemes més avançats (com LVM o RAID) diverses particions poden formar un únic volum, o un volum pot estar repartit en diversos discs físics.

# Gestió d’usuaris, grups i permisos
## Fitxers importants
### Els usuaris
#### Definició

Un usuari en Linux és una identitat individual que pot iniciar sessió i utilitzar el sistema. Cada usuari té un nom, un identificador únic (UID), un directori personal i uns permisos que determinen què pot fer dins del sistema.

#### Un usuari pot arribar a servir per:
* Identificar qui utilitza el sistema.
* Controlar l’accés als fitxers i recursos.
* Separar els entorns de treball de cada persona o procés.
* Garantir la seguretat, ja que cada usuari només pot fer allò per al que té permisos.

#### Perquè es creen els usuaris
* Es creen els usuaris per organitzar i protegir el sistema:
* Cada persona té el seu directori personal i la seva contrasenya.
* Es pot limitar què pot fer cadascú (per exemple, alguns poden instal·lar programes i altres no).
* També hi ha usuaris del sistema (com root, daemon, www-data, etc.) que s’utilitzen perquè els serveis del sistema funcionin de manera segura i separada.

#### Tots els usuaris tenen els mateixos permisos?

No. Hi ha diferents nivells de permisos:

* **Usuari normal:** pot treballar només dins del seu espai i amb els seus fitxers.
* **Usuari administrador (root):** té tots els privilegis del sistema i pot fer qualsevol canvi.
* **Usuaris de sistema:** no inicien sessió, serveixen per executar serveis o processos.

#### On trobar els usuaris al sistema.

En Linux, la gestió dels usuaris es realitza des del fitxer passwd. Aquest fitxer és un dels fitxers més importants del sistema operatiu i es pot localitzar dintre de la carpeta /etc/. Per a accedir-hi cal posar la següent comanda.
* sudo nano /etc/passwd

![Imatge del fitxer passwd](../imatges/sprint2_25.jpg)

La funció d’aquest fitxer és la de guardar la informació bàsica de tots els usuaris del sistema. Cada línia d’aquest fitxer representa un usuari i conté diversos camps separats per dos punts (:)

Permet associar-los amb els seus UID, grups, directoris personals i shells, a més permet que el sistema sàpiga qui és cada usuari i que pot fer.

#### L’estructura d’una línia és la següent.

* nom_usuari:x:UID:GID:comentari:directori_personal:shell
* jesus:x:1000:1000:jesus:/home/jesus: /bin/bash (Exemple real)

#### El significat de cada camp és el següent:
* **nom_usuari:** És el nom amb què l’usuari inicia sessió
* **x:** Indica que la contrasenya està xifrada al fitxer /etc/shadow
* **UID:** Identificador numèric únic de l’usuari
* **GID:** Identificador numèric del grup principal de l’usuari
* **Comentari:** Camp opcional per descriure l’usuari (nom complet, funcio, etc)
* **Directori_personal:** Ruta on l’usuari te els seus fitxers
* **shell:** Programa que s’executa quan l’usuari inicia sessio.

Altres detalls del fitxer és que és un fitxer llegible per tothom, però només l’usuari root pot modificar-lo. Conte tant usuaris humans com usuaris del sistema com ara.

* root:x:0:0:root:/root:/bin/bash
* daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
* www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin

Els usuaris del sistema es poden distingir perquè normalment tenen un identificador numèric (UID) inferior a 1000, mentre que els usuaris creats per persones tenen UIDs a partir de 1000.

A més, els usuaris del sistema sovint no tenen directori personal a /home ni una shell activa (apareix com /usr/sbin/nologin o, ja que no estan pensats per iniciar sessió, sinó per fer funcionar serveis del sistema. A la imatge anterior es pot veure el que s’explica aquí aplicat a la pràctica.

#### Com crear un usuari

En Linux, per a crear un usuari principalment es pot fer bé per la part gràfica entrant a la configuració del sistema, o bé pel terminal amb comandes. Per l’entorn gràfic si es va a paràmetres, opció Sistema.

![Imatge configuració d'usuaris per entorn grafic](../imatges/sprint2_26.jpg)

Ja es pot veure l’opció d’usuaris, un cop dins ja podríem afegir els usuaris que facin falta. Tanmateix, aquesta opció no es profunditzarà, ja que únicament permet la creació d’usuaris de forma bàsica, mentre que pel terminal es poden definir moltes més opcions avançades.

Per a crear un usuari des del Terminal es pot utilitzar dues comandes, la comanda **adduser** o la comanda **useradd**.

La comanda **useradd** és una comanda molt més tècnica i directa i que està pensada inicialment per a administradors o scripts automatitzats. Aquesta comanda conté una quantitat considerable d’opcions que per la seva longitud no es posaran aquí, però convé saber de la seva existència.

La comanda **adduser**, per exemple, és una comanda més amigable que l’anterior. Per a crear un usuari cal posar la comanda **sudo adduser (nom_usuari)**. Al posar-la demana una contrasenya, el nom complet i altres dades opcionals pas a pas de forma més automatitzada i sense necessitat d’afegir paràmetres.

![Imatge on es crea un usuari des del terminal](../imatges/sprint2_27.jpg)

Un cop ja creat l’usuari, es pot fer una consulta per tal de comprovar que l’usuari s’ha creat correctament i veure les seves dades.

![Imatge de comprovació de com s'ha creat un usuari](../imatges/sprint2_28.jpg)

Si s’utilitza la comanda com s’aprecia a la imatge ens mostra l’usuari creat amb totes les seves dades que s’han generat dintre del sistema.

#### Com eliminar un usuari

Per a esborrar un usuari del sistema també es pot esborrar des de la part gràfica, però en aquest cas ens centrarem en l’apartat del Terminal, ja que com ja hem dit, les opcions són molt més completes que en l’entorn gràfic. Per a esborrar un usuari s’utilitzarà la comanda **sudo userdel nom_usuari**. Només els usuaris amb permisos de **root** poden eliminar comptes. Comandes a utilitzar per a esborrar un usuari.

* **sudo deluser nom_usuari:** Elimina l’usuari pero conserva el seu directori personal
* **sudo deluser –remove-home nom_usuari:** Elimina l’usuari i tambe el seu directori personal i fitxers associats
* **sudo userdel nom_usuari:** Fa la mateixa funció pero es mes tecnica
* **sudo userdel -r nom_usuari:** Elimina tambe el directori personal i el correu intern

Quan s’esborra un usuari, és borr*a també la seva entrada dels fitxers del sistema (/etc/passwd, /etc/shadow i /etc/group).

#### Modificar usuari
La principal comanda per a modificar un usuari és la comanda usermod, la sintaxi de la comanda és: 
* sudo usermod (opcions) nom_usuari
Algunes de les opcions més habituals de la comanda són les següents:
* **-l nou_nom:** Canvia el nom de l’usuari
* **-d /nova/ruta:** Canvia el directori personal
* **-m:** mou els fitxers al nou directori personal
* **-s /bin/bash:** canvia el shell per defecte
* **-g grup:** Canvia el grup principal
* **-aG grup1, grup2:** afegeix l’usuari a grups secundaris
* **-e AAAA-MM_DD:** Defineix una nova data de caducitat
* **-L / -U:** Bloca (-L) o desbloqueja (-U) el compte.

Alguns exemples de les comandes utilitzades per a modificar usuaris.

![Imatge de la comanda usermod -s](../imatges/sprint2_29.jpg)
![Imatge de la comanda usermod -L](../imatges/sprint2_30.jpg)
![Imatge de la comanda usermod -U](../imatges/sprint2_31.jpg)

#### Canviar el nom de l’usuari
Quan es parla de canviar el nom d’usuari, aquest es pot realitzar de diferents maneres, una que seria canviar el nom de forma visible, però una altra cosa diferent i que no és el mateix és canviar-lo completament dins del sistema, incloent-hi la carpeta personal /home, permisos i referències internes.

Abans de realitzar un compte complet d’usuari, és convenient realitzar una còpia de seguretat per si hi ha errors. És una feina que s’ha d’executar com a usuari root o amb sudo i cal tenir en compte que no es pot realitzar mentre es tingui la sessió oberta, per la qual cosa caldria disposar d’un altre usuari amb permisos d’administrador al sistema.

Per a realitzar aquest canvi s’ha de realitzar en tres passos, ja que s’està modificant tres coses diferents. Per tant, les comandes a utilitzar serien les següents:
* **sudo usermod -l nou_nom antic_nom** (canvia el nom de l’usuari)
* **sudo mv /home/antic_nom /home/nou_nom** (canvia de nom la carpeta del perfil)
* **sudo usermod -d /home/nou_nom -m nou_nom** (canvi la ruta del directori personal associada al compte)

El perquè no es pot fer tot de cop és degut al fet que cada element pertany a un subsistema diferent (gestió d’usuaris, sistema de fitxers i configuració del compte). Si es fes de cop, podrien quedar referències trencades o fitxers sense propietari.

Aquí s’ha vist fer-ho des del terminal, però és possible fer això des de l’entorn gràfic? La resposta seria que des de l’entorn gràfic només permet canviar el nom visible i algunes dades bàsiques, per canviar completament un usuari (nom intern, carpeta /home, permisos i rutes), només es pot fer des del terminal i amb les comandes abans comentades.

#### Creació d’un usuari complet amb una sola comanda.
La comanda **useradd** s’utilitza per crear usuaris de manera manual al sistema Linux. Per defecte, si s’executa sense opcions, només afegeix l’entrada de l’usuari als fitxers del sistema (/etc/passwd, /etc/shadow, /etc/group), però no crea el directori personal ni la resta d’elements necessaris.

Si s’utilitza per exemple la comanda **sudo useradd nom_usuari**, això crea l’usuari, però no genera automàticament la carpeta /home/nom_usuari, no assigna cap shell d’inici, no posa cap contrasenya i no crea cap grup amb el mateix nom. És a dir, l’usuari existeix al sistema, però no pot iniciar sessió fins que es completen els altres passos manualment.

Però hi ha la possibilitat de poder tots els passos d’un sol cop sense haver d’editar res després. Per a que això sigui possible caldria implementar la comanda de la següent manera.
* sudo useradd -m -d /home/pere -s /bin/bash -c "Pere Martí" pere
on cada apartat té el seu significat
* **sudo:** Per a donar permisos d’administrador a la comanda
* **useradd:** comanda per a inserir l’usuari
* **-m:** Crea automàticament la carpeta personal /home/pere
* **-d /home/pere:** Defineix la ruta del directori personal
* **-s /bin/bash:** Assigna la Shell per defecte
* **-c “Pere Marti”:** Afegeix un comentari o nom complet
* **pere:** És el nom del nou usuari

Únicament quedaria afegir la contrasenya. La contrasenya no es posa directament dintre de la comanda useradd per motius de seguretat no permet posar la contrasenya en text pla directament dins de la mateixa ordre. Això evita que la contrasenya quedi visible a la línia de comandes o registrada en l’historial del terminal (.bash_history) cosa que seria un risc. Per aquesta raó, un cop creat l’usuari es posaria la comanda sudo passwd pere per a afegir la contrasenya de forma segura.

Avantatge de fer-ho tot d’una vegada és el de fer-ho tot en una sola comanda amb **useradd** estalvia temps i evita errors, ja que el sistema crea tots els elements necessaris de manera coherent: usuari, directori personal, shell i descripció. Això és especialment útil en entorns administratius o scripts automàtics on cal crear diversos usuaris de forma ràpida i controlada.

Però si es volgués fer tot complet també es podria fer amb les comandes 
* sudo useradd -m -d /home/pere -s /bin/bash -c "Pere Martí" pere 
* echo "pere:1234" | sudo chpasswd (assigna password 1234 a l’usuari pere per defecte sense mostrar-la a la pantalla ni guardar-la a fitxers visibles)
* sudo usermod -aG sudo pere (afegeix a pere al grup sudo sense eliminar els altres si cal)

Tot aquest procés també es pot realitzar des d’un script, la qual cosa permetria crear diversos usuaris automàticament. Per a fer-ho només caldria crear un fitxer .sh amb una forma com la de l’exemple.

```
#!/bin/bash
sudo useradd -m -s /bin/bash -c "Anna Torres" anna
echo "anna:contrasenyaSegura" | sudo chpasswd
sudo useradd -m -s /bin/bash -c "Joan Vidal" joan
echo "joan:1234" | sudo chpasswd
```

En aquest cas es crearien l’usuari Anna Torres i Joan Vidal, però es podrien afegir tants d’usuaris com sigui necessari. Un cop guardat només caldria executar-lo amb una comanda com aquesta.
* sudo bash crear_usuaris.sh

### Els grups
#### Definició
Un grup en Linux és un conjunt d’usuaris que comparteixen uns mateixos permisos sobre fitxers o recursos. Els grups serveixen per gestionar de manera col·lectiva els accessos i privilegis dins del sistema.

Per a què serveixen els grups
* Els grups faciliten la gestió de permisos:
* Permeten donar accés compartit a un conjunt d’usuaris (per exemple, tots els membres del grup professors poden editar una mateixa carpeta).
* Eviten haver de configurar els permisos usuari per usuari.
* S’utilitzen molt en entorns amb molts usuaris, com servidors o xarxes corporatives.

#### Tipus de grups

* **Grup principal (primari):** Cada usuari té un grup principal assignat per defecte. Normalment, té el mateix nom que l’usuari i s’utilitza per determinar el propietari de fitxers i processos creats per aquell usuari.
* **Grup secundari (addicional):** Un usuari pot pertànyer a diversos grups alhora. Els grups secundaris permeten donar permisos addicionals o accés a recursos compartits.

#### Gestió de permisos i seguretat i organització

Els grups s’utilitzen per gestionar permisos de lectura, escriptura i execució sobre fitxers i carpetes. Això permet que, per exemple, tots els usuaris del grup projecte puguin modificar fitxers dins d’una mateixa carpeta, però els altres usuaris del sistema no.

Els grups ajuden a **mantenir la seguretat i l’ordre** dins d’un sistema amb molts usuaris. En lloc de donar permisos individualment, es poden donar al grup complet, fent el sistema més fàcil d’administrar.

#### On trobar els grups del sistema.

Si el que es necessita és saber la informació sobre els grups que hi han creats al sistema cal buscar el fitxer **group**. Aquest es troba a la carpeta **/etc** igual que el fitxer d’usuaris. Igual que el fitxer **passwd**, aquest també es pot considerar com un dels principals fitxers del sistema, conte la informació de tots els grups del sistema i els usuaris que en formen part. La comanda per a entrar al fitxer és la següent:

* sudo nano /etc/group

![Imatge del fitxer group](../imatges/sprint2_32.jpg)

Observant el fitxer es pot observar la seva estructura.

* nom_grup:x:GID:llista_usuaris

On cada camp significa el següent.
* **Nom_grup:** nom del grup
* **x:** indica que la contrasenya del grup (si n’hi ha està guardada a /etc/gshadow)
* **GID (group ID):** Identificador numeric unic del grup
* **llista_usuaris:** Usuaris membres del grup, separats per comes.

Cal recordar que només l’usuari **root** o un administrador pot modificar aquest fitxer. També és important tenir en compte que no és recomanable realitzar canvis dintre del fitxer.

Dintre del fitxer **group** també es troben els grups del sistema, aquestos són conjunts especials creats automàticament per gestionar serveis, processos i permisos interns de Linux. Tenen GIDs baixos (menys de 1000), no estan destinats a usuaris humans, i són essencials per mantenir la seguretat i el bon funcionament del sistema operatiu.

#### Comandes habituals en els grups.
Quan es treballa amb grups hi ha diverses comandes que permeten crear, eliminar, canviar noms, afegir usuaris, etc. Entre algunes de les comandes i paràmetres existents es poden trobar aquests:

* **groupadd nom:** Crea un nou grup
* **groupdel nom:** Elimina un grup
* **groupmod -n nou_nom antic_nom: Canvia el nom d’un grup
* **gpasswd -a usuari grup:** Afegeix un usuari a un grup
* **gpasswd -d usuari grup:** Elimina un usuari d’un grup
* **groups usuari:** Mostra els grups als quals pertany un usuari
* **id usuari:** Mostra el UID, GID i grups associats.
* **adduser usuari grup:** afegeix un usuari dintre d’un grup
* **deluser usuari nom_grup:** Elimina un usuari d’un grup

Alguns exemples de com treballar amb grups.

![Imatge de la comanda sudo addgroup](../imatges/sprint2_33.jpg)

![Imatge de la comanda sudo adduser](../imatges/sprint2_34.jpg)

Quan es treballa amb grups hi ha una cosa a ressaltar, l’usuari que ha instal·lat el sistema operatiu, aquest es troba dintre de molts més grups que un usuari afegit posteriorment. 

Això és degut al fet que aquest rep privilegis especials d’administració, per la qual cosa és afegit automàticament a diversos grups del sistema per tal que pugui instal·lar i actualitzar programes, configurar dispositius, administrar altres usuaris i altres coses relacionades amb l’administració del sistema.

![Imatge de la comanda cat](../imatges/sprint2_35.jpg)

Si es vol veure informació sobre els grups, una comanda que s’utilitza bastant és la comanda **groups**, aquesta és una ordre del terminal que mostra a quins grups pertany un usuari, llegeix la informació que hi ha a **/etc/group** i la presenta d’una manera senzilla.

Únicament posant la comanda **groups nom_usuari** ja mostra els grups que pertany un usuari. Si no es posa cap nom d’usuari, mostra els grups de l’usuari actual

#### El fitxer gshadow

El fitxer **gshadow** és on Linux guarda la informació de seguretat dels grups del sistema. Conté les **contrasenyes encriptades dels grups** (si n’hi ha), així com la llista d’administradors i membres de cada grup. Només pot ser llegit o modificat per l’usuari root, ja que emmagatzema dades sensibles.

El fitxer **gshadow** es troba localitzat dintre de la carpeta **/etc/**. i per a poder accedir-hi cal posar la comanda **sudo nano /etc/gshadow.**

![Imatge del fitxer gshadow](../imatges/sprint2_36.jpg)

Cada línia del fitxer representa un grup i segueix aquest format:

* nom_grup:contrasenya:administradors:membres

El significat dels camps és el següent:
* **nom_grup:** Nom del grup (ha de coincidir amb el del fitxer /etc/group)
* **contrasenya:** Contrasenya del grup, si existeix (normalment ! o x perquè no s’utilitza)
* **administradors:** Usuaris que poden afegir o eliminar membres del grup
* **membres:** Usuaris que pertanyen al grup

Com a resum, el fitxer **/etc/gshadow** desa la informació de seguretat dels grups: contrasenyes, administradors i membres. Només **root** hi pot accedir, i treballa conjuntament amb /etc/group per gestionar correctament els permisos i la seguretat dels grups del sistema.

#### Els administradors de grup

Els **administradors de grup** són usuaris amb permisos especials per gestionar un grup concret sense necessitat de ser l’usuari **root**. Això permet delegar part de la gestió del sistema i facilitar l’administració en entorns amb molts usuaris.

Entre les funcions d’un administrador de grup es poden trobar permetre Afegir o eliminar membres d’aquell grup, Canviar la contrasenya del grup (si se’n fa servir una), Consultar la llista de membres del grup, etc. Aquests permisos s’apliquen només sobre el grup que administra, no sobre la resta del sistema.

Aquests administradors de grup s’especifiquen dintre del fitxer **gshadow** en el tercer camp de cada línia. Els administradors de grup són usuaris amb privilegis per gestionar un grup concret: poden afegir o eliminar membres i canviar-ne la contrasenya.

Aquesta informació es troba al fitxer **/etc/gshadow**, i permet distribuir tasques d’administració sense donar accés complet al sistema.

### Les contrasenyes
#### Definició

Les contrasenyes serveixen per protegir l’accés als comptes d’usuari i garantir que només les persones autoritzades puguin utilitzar el sistema. Cada usuari en té una d’associada, que s’introdueix en iniciar sessió o en executar accions que requereixen permisos especials.

#### On es guarden les contrasenyes
Igual que els usuaris i els grups, també es troba l’arxiu on es guarden les contrasenyes. Aquest arxiu s’anomena **shadow**, inicialment les contrasenyes es trobaven dintre del fitxer **passwd** conjuntament amb els usuaris, però com que representava un risc de seguretat en ser un fitxer llegible per tots els usuaris, actualment les contrasenyes es guarden xifrades en el fitxer **shadow**.

El fitxer **shadow** es troba a la carpeta **/etc/** i només l’usuari root o el sistema pot llegir o modificar aquest fitxer. Per a poder accedir al fitxer es posarà la comanda.
* sudo nano /etc/shadow

![Imatge del fitxer shadow](../imatges/sprint2_37.jpg)

Cada línia del fitxer representa un usuari del sistema i segueix el format:

* nom_usuari:contrasenya_encriptada:data_últim_canvi:min:max:avís:inactiu:caducitat

El significat dels camps és el següent:
* **Nom_usuari:** Nom de l’usuari
* **contrasenya_encriptada:** Contrasenya xifrada amb un olgaritme (el prefix $6$ indica que s’ha usat SHA-512)
* **data_ultim_canvi:** Nombre de dies des del 1/1/1970 fins a l’últim canvi de contrasenya
* min:** Dies mínims que es pugui canviar la contrasenya
* **max:** Dies màxims abans que caduqui la contrasenya
* **avis:** Dies d’avis abans que la contrasenya caduqui.
* **inactiu:** Dies després de la caducitat en què el compte queda inactiu.
* **caducitat:** Data exacta en què el compte deixa d’estar actiu.

Com a observació al fitxer cal afegir que la majoria d’usuaris com systemd-oom, sssd, dnsmasq, avahi, etc. no tenen contrasenya d’inici de sessió. Això es veu pels símbols ! o * al segon camp. Són usuaris del sistema utilitzats per serveis interns i no poden iniciar sessió

Cal tornar a remarca que el fitxer **/etc/shadow** no pot ser llegit per altres usuaris, només per root. Si algú aconsegueix accedir-hi, podria intentar trencar les contrasenyes mitjançant tècniques de força bruta. Per això, les contrasenyes es guarden en format hash i amb un salt aleatori que fa molt difícil revertir-les.

#### Comandes per gestionar contrasenyes

Hi ha diverses comandes que permeten gestionar les contrasenyes, moltes d’aquestes comandes requereixen tenir permisos de **root**. Algunes de les comandes són les següents.
* **sudo passwd usuari:** canvia la contrasenya de l’usuari usuari
* **passwd:** canvia la pròpia contrasenya
* **passwd -d:** Elimina la contrasenya d’un compte
* **sudo chpasswd:** Canvia contrasenyes de diversos usuaris a la vegada d’es d’un fitxer o entrada

Alguns exemples de canvis de contrasenya

![Imatge comanda sudo passwd](../imatges/sprint2_38.jpg)

### L’aplicació gnome-system-tools
Quan **gnome-system-tools** va aparèixer, Linux no tenia eines gràfiques modernes integrades com les que coneixem avui (p. ex. Configuració o Settings de GNOME). Aleshores, gnome-system-tools actuava com un “centre de control” independent per a afegir o eliminar usuaris i grups, configurar la xarxa (IP, DNS, passarel·les...), canviar la data, hora o zona horària, activar o desactivar serveis del sistema, compartir carpetes localment (Samba/NFS) entre altres

Era molt útil perquè permetia fer des de l’entorn gràfic coses que fins llavors només es podien fer amb ordres del terminal. Avui dia, totes aquestes funcions ja estan **integrades nativament** dins del mateix GNOME o altres escriptoris:

Això fa que gnome-system-tools sigui redundant, ja que fa el mateix però amb una interfície antiga i menys compatible. L’aplicació no s’ha actualitzat durant anys (el seu desenvolupament pràcticament es va aturar cap al 2015).

GNOME i altres entorns moderns ja porten eines pròpies més integrades i segures. Algunes funcionalitats de gnome-system-tools no funcionen bé en versions modernes de Linux, perquè els mètodes de gestió del sistema (com systemd o NetworkManager) han canviat. Per això, moltes distribucions ja no la instal·len per defecte.

Podríem dir que **gnome-system-tools** està obsoleta o en desús, però encara es pot instal·lar i funcionar parcialment en alguns sistemes. No està “trencada”, però ja no rep manteniment ni millores. Pot anar bé per a entorns educatius o per mostrar com era la gestió gràfica antiga de Linux, però no s’aconsella utilitzar-la en sistemes moderns o de producció.

Si es volgués instal·lar caldria posar la comanda
* sudo apt install gnome-system-tools

![Pantalla de l'aplicació gnome-system-tools](../imatges/sprint2_39.jpg)

Un cop instal·lat ja apareix una icona a l’apartat de les aplicacions i si es polsa apareix la pantalla que es veu a la imatge on des d’alli es poden realitzar els canvis.

### Els permisos
#### Definició

Els permisos tenen la funció de controlar l’accés als fitxers, carpetes i recursos del sistema. Gràcies a ells es pot garantir la seguretat, l’ordre i la privadesa dels usuaris evitant que un usuari modifiqui o esborri fitxers d’un altre. S’apliquen a tres nivells (usuari, grup i altres) i es poden gestionar amb comandes com chmod, chown i chgrp.

#### Propietat dels fitxers
Cada fitxer o carpeta a Linux té tres nivells de propietat:

* **Usuari (owner):** és el propietari del fitxer (normalment qui el crea).
* **Grup (group):** és el grup al qual pertany el fitxer; tots els membres del grup comparteixen uns mateixos permisos.
* **Altres (others):** Tots els altres usuaris del sistema.

#### Tipus de permisos

* **Lectura	    r (read)**	Permet llegir el contingut del fitxer o llistar una carpeta
* **Escriptura	    w (write)**	Permet modificar o eliminar el fitxer o dintre d’una carpeta
* **Execució	   x (execute)**	Permet executar un fitxer com a programa o entrar en una carpeta.
#### Com es representen

La forma de veure els permisos és fent un ls -l on es mostra una línia com aquesta
