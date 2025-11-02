---
layout: default
title: "Curs d'implantació de sistemes operatius "
---

Aquest repositori compte el contingut dels exercicis que se'ns va demanant a la classe d'implantació de sistemes operatius

# Llicencia

El contingut està baix la llicencia [Creative Commons BY-NC-SA 4.0 Internacional](LICENSE.md).

# Contingut del curs
**Unitat 1. Sprint1: Implantació de sistemes operatius**
   - [Màquina virtual dual Ubuntu - Windows](sp1/index.md).
      - [Configuració de Virtualbox](sp1/index.md#configuraci%C3%B3-de-virtualbox)
      - [Instal·lació del sistema operatiu Ubuntu](sp1/index.md#installaci%C3%B3-del-sistema-operatiu-ubuntu)
      - [Instal·lació del sistema operatiu Windows](sp1/index.md#installacio-del-sistema-operatiu-windows-a-la-m%C3%A0quina-virtual)
      - [Recuperació del GRUB d'Ubuntu](sp1/index.md#recuperaci%C3%B3-del-grub-dubuntu)
   - [Maquina virtual no dual Ubuntu - Windows](sp1/index.md#virtual-amb-dos-sistemes-operatius-amb-arrancada-independent)
      - [Configuració de VirtualBox](sp1/index.md#configuraci%C3%B3-de-virtualbox-1)
      - [Particionat del disc dur d'Ubuntu](sp1/index.md#particionat-del-disc-de-lubuntu)
      - [Particionat del disc dur Windows](sp1/index.md#particionat-del-disc-del-windows-10)
      - [Entrada a la bios per arrancar entre Windows u Ubuntu](sp1/index.md#entrada-a-la-bios-per-a-canviar-entre-sistemes-operatius)
   - [Punts de restauració](sp1/index.md#punts-de-restauraci%C3%B3)
       - [Creació i assignació del disc dur](sp1/index.md#creaci%C3%B3-i-assignaci%C3%B3-del-disc-dur)
       - [Particionat i formateig del disc dur](sp1/index.md#particionat-i-formateig-del-disc-dur)
       - [Instal·lació Timeshift i creació d'instantànies](sp1/index.md#installaci%C3%B3-timeshift-i-creaci%C3%B3-dinstant%C3%A0nies)
    - [Configuració de la xarxa](sp1/index.md#configuraci%C3%B3-de-la-xarxa)
    - [Comandes generals i instal·lacións](sp1/index.md#comandes-generals-i-installacions)
       - [Instal·lació d'aplicació manualment d'una versió concreta](sp1/index.md#installaci%C3%B3-daplicaci%C3%B3-manualment-duna-versi%C3%B3-concreta)
       - [Instal·lació aplicació prioritzant una versió i/o repositori concret](sp1/index.md#installaci%C3%B3-aplicaci%C3%B3-prioritzant-una-versi%C3%B3-io-repositori-concret-pinned-version))

**Unitat 1. Sprint2: instal·lació, configuració de programari de base i gestio de fitxers**
   - [Sistemes de fitxers i particions](/sp2/index.md#sistemes-de-fitxers-i-particions)
       - [Mida sector](/sp2/index.md#mida-sector)
       - [Mida block](/sp2/index.md#mida-block)
       - [Fragmentació interna](/sp2/index.md#fragmentaci%C3%B3-interna)
       - [Fragmentació externa](/sp2/index.md#fragmentaci%C3%B3-externa)
       - [Com mostra l'espai que ocupa un fitxer o directori al disc](/sp2/index.md#com-mostra-lespai-que-ocupa-un-fitxer-o-directori-al-disc)
       - [Tipus de formateig](/sp2/index.md#tipus-de-formateig)
           - [Baix nivell](/sp2/index.md#formateig-de-baix-nivell)
           - [Mig nivell](/sp2/index.md#formateig-de-mig-nivell)
           - [Alt nivell](/sp2/index.md#formateig-dalt-nivell)
       - [Gestió de particions](/sp2/index.md#gesti%C3%B3-de-particions)
            - [Creació del disc dur virtual i afegir-lo a la màquina virtual Ubuntu](/sp2/index.md#creaci%C3%B3-del-disc-dur-virtual-i-afegir-lo-a-la-m%C3%A0quina-virtual-ubuntu)
            - [Comprovació del disc dur al sistema](/sp2/index.md#comprovaci%C3%B3-del-disc-dur-al-sistema)
            - [Creació de les particions al nou disc dur](/sp2/index.md#creaci%C3%B3-de-les-particions-al-nou-disc-dur)
        - [El proces de formatació del disc dur](/sp2/index.md#el-proces-de-formataci%C3%B3-del-disc-dur)
        - [Observació dels valors existents a les particions creades](/sp2/index.md#observaci%C3%B3-dels-valors-existents-a-les-particions-creades)
        - [Muntatge de particions al sistema](/sp2/index.md#muntatge-de-particions-al-sistema)
            - [Muntatge i desmuntatge manual](/sp2/index.md#muntatge-i-desmuntatge-manual)
            - [Muntatge automàtic amb fstab](/sp2/index.md#muntatge-autom%C3%A0tic-amb-fstab)
        - [Fragmentació dels sistemes de fitxers (ext4 i NTFS)](/sp2/index.md#fragmentaci%C3%B3-dels-sistemes-de-fitxers-ext4-i-ntfs)
            - [Fragmentació en NTFS (Windows)](/sp2/index.md#fragmentaci%C3%B3-en-ntfs-windows)
            - [Fragmentació en ext4 (Linux)](/sp2/index.md#fragmentaci%C3%B3-en-ext4-linux)
            - [La comanda e4defrag](/sp2/index.md#la-comanda-e4defrag)
        - [Particions i volums](/sp2/index.md#particions-i-volums)
    - [Gestió d'usuaris, grups i permisos]
         - [Fitxers importants](/sp2/index.md#fitxers-importants)
            - [Els usuaris](/sp2/index.md#els-usuaris)
               - [Definició](/sp2/index.md#definici%C3%B3)
               - [Un usuari pot arribar a servir per:](/sp2/index.md#un-usuari-pot-arribar-a-servir-per)
               - [Perquè es creen els usuaris](/sp2/index.md#perqu%C3%A8-es-creen-els-usuaris)
               - [On trobar els usuaris al sistema](/sp2/index.md#on-trobar-els-usuaris-al-sistema)
               - [Com crear un usuari](/sp2/index.md#com-crear-un-usuari)
               - [Com eliminar un usuari](/sp2/index.md#com-eliminar-un-usuari)
               - [Modificar usuari](/sp2/index.md#modificar-usuari)
               - [Canviar el nom de l’usuari](/sp2/index.md#canviar-el-nom-de-lusuari)
               - [Creació d’un usuari complet amb una sola comanda](/sp2/index.md#creaci%C3%B3-dun-usuari-complet-amb-una-sola-comanda)
            - [Els grups](/sp2/index.md#els-grups)
               - [Definició](/sp2/index.md#definici%C3%B3-1)
               - [Tipus de grups](/sp2/index.md#tipus-de-grups)
               - [Gestió de permisos i seguretat i organització](/sp2/index.md#gesti%C3%B3-de-permisos-i-seguretat-i-organitzaci%C3%B3)
               - [On trobar els grups del sistema](/sp2/index.md#on-trobar-els-grups-del-sistema)
               - [Comandes habituals en els grups](/sp2/index.md#comandes-habituals-en-els-grups)
               - [El fitxer gshadow](/sp2/index.md#el-fitxer-gshadow)
               - [Els administradors de grup](/sp2/index.md#els-administradors-de-grup)
            - [Les contrasenyes](/sp2/index.md#les-contrasenyes)
               - [Definició](/sp2/index.md#definici%C3%B3-2)
               - [On es guarden les contrasenyes](/sp2/index.md#on-es-guarden-les-contrasenyes)
               - [Comandes per gestionar contrasenyes](/sp2/index.md#comandes-per-gestionar-contrasenyes)
            - [L’aplicació gnome-system-tools](/sp2/index.md#laplicaci%C3%B3-gnome-system-tools)
            - [Els permisos](/sp2/index.md#els-permisos)
               - [Definició](/sp2/index.md#definici%C3%B3-3)
               - [Propietat dels fitxers](/sp2/index.md#propietat-dels-fitxers)
               - [Tipus de permisos](/sp2/index.md#tipus-de-permisos)
               - [Com es representen](/sp2/index.md#com-es-representen)
               - [Representació numèrica](/sp2/index.md#representaci%C3%B3-num%C3%A8rica)

- [Còpies de seguretat i automatització de tasques]
- [Quotes d'usuaris]
