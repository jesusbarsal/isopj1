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


