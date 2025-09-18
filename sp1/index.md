---
layout: default
title: "Sprint1 1: Instal·lació i configuracio inicial"
---

# Virtualització i instal·lació del SO Ubuntu
## Virtualització amb Virtualbox

Per tal de poder realitzar la instal·lació d'Ubuntu, i com que no podem realitzar-ho sobre una maquina fisica, hem d'utilitzar l'aplicació anomenada Virtualbox per tal de poder realitzar la instal·lació del sistema operatiu. L'elecció d'aquesta aplicació i no un altra com Vmware, es que aquesta es de codi lliure i gratuita, i per tant no es necessaria la compra de cap llicencia

### Creació de la maquina virtual

Com ja hem dit per a la maquina virtual s'ha utilitzat l'aplicacio Virtualbox, a continuació s'exposarà la configuració que s'ha realitzat per tal de crear la maquina virtual.

![Resum de les opcions aplicades a Virtualbox](../imatges/pantalla_virtualbox.jpg)

#### Apartat 1 General

En aquest primer apartat, unicament el que es fa es escriure el nom que se li vol donar a la maquina virtual i el propi Virtualbox si el nom esta relacionat amb el sistema operatiu a instal·lar la propia aplicacio ja li assigna el tipus de sistema operatiu a instalar.

#### Apartat 2 Sistema

**memoria Ram:** S'han assignat 8 Gb de ram, suficient per a poder fer funcionar correctament un Ubuntu Desktop i mes que de sobres en aquest cas donat que per a la instal·lació del sistema operatiu, i de sobres per a assignar-les donat que l'equip anfitrio disposa de 32 Gb de ram.

**Processador**: En aquest cas s'han assignat 2 CPU suficient per a la instal·lació del sistema operatiu i posterior funcionament, amb 2 cpu, permet el funcionament del sistema operatiu virtual i de l'anfitrio, i d'aquesta manera permet el funcionament de mes d'una maquina virtual de forma simultanea sense haver-hi una perdua considerable de rendiment.

**Ordre d'arrancada:** Quant a l'ordre d'arrancada es deixa l'opcio per defecte que dona l'aplicació i que es perfectament valida per a l'arrancada

**EFI:** Aquesta opció en l'actualitat es una opcio que ja es recomendable activar-la en tot moment, basicament el que fa es que al instal·lar el sistema operatiu, aquest reconegui que "l'ordinador" sobre el que es realitza la instal·lacio ja disposa de UEFI i no de bios, per la qual cosa ja es l'opcio recomanada donat que en l'actualitat ja tots els equips moderns ja funcionen per UEFI i no per BIOS.

**Acceleracio:** Aqui es on es pot configurar com s'utilitzen les funcionalitats de virtualització del processador del equip anfitrio Aquests parametres influeixen en el rendiment i la compatibilitat de la maquina virtual

#### Apartat 3 Pantalla

**Memoria de video** Des d'aquesta opció es pot assignar quina sira la quantitat de memoria que virtualbox assignara a la maquina virtual, aquest apartat afecta a la qualitat d'imatge, el rendiment i les funcionalitats multimedia. En aquest cas, s'han assignat 16 Mb donat que nomes es realitzara la instal·lació, el normal seria aplicar-hi 128 Mb que es el maxim aplicable, si s'actives l'opcio de 3D llavors es podria arribar fins a 256 Mb, pero inicialment unicament s'ha assignat el minim funcional.

**Controlador de grafics:** Aquesta opció ofereix diferents controladors de video virtuals. Depenent de la versio de sistema operatiu cal assignar un tipus o un altre de controlador. En el cas per a Ubuntu cal assignar el que es veu a la imatge, es a dir VMSVGA que es el mes adequat per a instal·lacions de Linux.

**Servei d'escriptori remot:** Per defecte no ve activat, en cas d'activar-ho, aquesta opció permet accedir a la maquina virtual de manera remota com si s'estigues davant de la seva pantalla. Treballa amb el protocol VRDP que es una extensió del RDP de Microsoft

**Enregistrament:** Amb aquesta opció desactiva per defecte permet realitzar una gravacio de la maquina virtual en un format multimedia util per a documentar processos, formacions o demostracions.

#### Apartat 4 Emmagatzematge


# Llicenciament
# Gestors d'arrencada per a instal·lacions DUALS
# Punts de restauració
# Configuració de la xarxa
# Comandes generals i instal·lacions
