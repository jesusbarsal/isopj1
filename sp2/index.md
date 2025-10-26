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

![Imatge gparted amb el disc dur sense particionar](../imatges/sprint2_04.jpg)

Comprovat que el nou disc dur ja està disponible, i que aquest es troba com a /dev/sbd/, es procedeix a la creació de les particions. Tambe es podria averi

### Creació de les particions al nou disc dur

Per tal de crear les particions al disc dur, s'utilitzar la comanda **fdisk**. Per tal de crear les particions 

