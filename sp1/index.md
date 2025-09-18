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

- **memoria Ram:** S'han assignat 8 Gb de ram, suficient per a poder fer funcionar correctament un Ubuntu Desktop i mes que de sobres en aquest cas donat que per a la instal·lació del sistema operatiu, i de sobres per a assignar-les donat que l'equip anfitrio disposa de 32 Gb de ram.

- **Processador**: En aquest cas s'han assignat 2 CPU suficient per a la instal·lació del sistema operatiu i posterior funcionament, amb 2 cpu, permet el funcionament del sistema operatiu virtual i de l'anfitrio, i d'aquesta manera permet el funcionament de mes d'una maquina virtual de forma simultanea sense haver-hi una perdua considerable de rendiment.

- **Ordre d'arrancada:** Quant a l'ordre d'arrancada es deixa l'opcio per defecte que dona l'aplicació i que es perfectament valida per a l'arrancada

- **EFI:** Aquesta opció en l'actualitat es una opcio que ja es recomendable activar-la en tot moment, basicament el que fa es que al instal·lar el sistema operatiu, aquest reconegui que "l'ordinador" sobre el que es realitza la instal·lacio ja disposa de UEFI i no de bios, per la qual cosa ja es l'opcio recomanada donat que en l'actualitat ja tots els equips moderns ja funcionen per UEFI i no per BIOS.

- **Acceleracio:** Aqui es on es pot configurar com s'utilitzen les funcionalitats de virtualització del processador del equip anfitrio Aquests parametres influeixen en el rendiment i la compatibilitat de la maquina virtual

#### Apartat 3 Pantalla

- **Memoria de video** Des d'aquesta opció es pot assignar quina sira la quantitat de memoria que virtualbox assignara a la maquina virtual, aquest apartat afecta a la qualitat d'imatge, el rendiment i les funcionalitats multimedia. En aquest cas, s'han assignat 16 Mb donat que nomes es realitzara la instal·lació, el normal seria aplicar-hi 128 Mb que es el maxim aplicable, si s'actives l'opcio de 3D llavors es podria arribar fins a 256 Mb, pero inicialment unicament s'ha assignat el minim funcional.

- **Controlador de grafics:** Aquesta opció ofereix diferents controladors de video virtuals. Depenent de la versio de sistema operatiu cal assignar un tipus o un altre de controlador. En el cas per a Ubuntu cal assignar el que es veu a la imatge, es a dir VMSVGA que es el mes adequat per a instal·lacions de Linux.

- **Servei d'escriptori remot:** Per defecte no ve activat, en cas d'activar-ho, aquesta opció permet accedir a la maquina virtual de manera remota com si s'estigues davant de la seva pantalla. Treballa amb el protocol VRDP que es una extensió del RDP de Microsoft

- **Enregistrament:** Amb aquesta opció desactiva per defecte permet realitzar una gravacio de la maquina virtual en un format multimedia util per a documentar processos, formacions o demostracions.

#### Apartat 4 Emmagatzematge

Aquest apartat es un dels mes importants de la creació de la maquina virtual, aqui es on es pot afegir, eliminar i configurar els dispositius d'emmagatzematge que tindrà la maquina virtual com ara discs durs, unitats optiques principalment.

- **Controlador** En aquest cas ens trobem amb dos apartats, el relacionat amb el lector de cd que per defecte ve amb una unitat IDE (sistema obsolet) per que encara funciona, i que si fos necessari es pot canviar per un de SATA mes adequat i actual, pero en aquest cas no es obligatori el seu canvi donat que encara continua funcionant. Aqui es on li assignarem la imatge ISO que tenim de l'Ubuntu per tal de que realitzi la instal·lació.
Per l'altre costat es troba el controlador SATA que aquest si que ja es el sistema mes actual i es on se li assigna el disc dur virtual que s'ha creat abans (80 Gb en aquest cas) i que es on es col·locaran totes les dades de la maquina virtual. De cara a l'Ubuntu es el que seria el disc dur. El sistema permet l'assignacio de multiples discs durs virtuals aixi com de varis lectors, etc. 

#### Apartat 5 Àudio

- Aquest apartat es un apartat que normalment no es modifica i com el seu nom indica, s'encarrega d'assignar la targeta de so per a la maquina virtual per tal de poder treballar amb sons. Normalment no es modifica i unicament s'activa o desactiva l'opció depenen del que es vulgue aconseguir.

#### Apartat 6 Xarxa

- Aquest apartat permet configurar com la maquina virtual es connectara a la xarxa i a internet. En aquest cas s'ha escollit l'opcio de NAT donat que aixo la maquina rep una ip privada de dintre d'una xarxa virtual interna el que permet que la maquina virtual no ocupi ips de la xarxa existent, i depenent de les configuracions a aplicar a la maquina virtual aquestes no afecten a la xarxa i equips aliens de la maquina virtual.
Virtualbox permet assignar diferents modalitats de configuració de xarxa. Les opcions son NAT, Bridged o adaptador pont, Internal Network, Host-only i Nat Network, cadascuna amb les seves caracteristiques que les defineixen i diferencien.

#### Apartat 7 USB

- En aquest apartat hi trobem la configuració per als ports USB que disposara la maquina virtual, podent assignar-hi ports USB 2.0, 3.0, etc. Amb aquesta opció es pot gestionar els dispositius USB fisics permetent que el sistema Ubuntu en aquest cas, els vegui com si estiguessin els dispositius USB conectats a ell mateix i no a l'amfitrio.

#### Apartat 8 Carpetes compartides

- Les carpetes compartides permeten que una màquina virtual accedeixi a carpetes o directoris de l’ordinador amfitrió com si fossin unitats locals dins del sistema convidat.
Això facilita enormement l’intercanvi de dades sense haver de copiar-les amb memòries USB ni utilitzar xarxa.

## Instal·lació del sistema operatiu.

Revisades les opcions de la maquina virtual es comença amb la instal·lació de l'Ubuntu, per la qual cosa es polsa sobre el boto de inicialitzar i comença la instal·lació. Dintre de les parts de la instal·lacio es mencionaran les parts mes importants.
En primer lloc apareix la pantalla per a escullir si volem instal·lar-lo o nomes provar-lo

![Pantalla de benvinguda](../imatges/pantalla_inici_ubuntu.jpg)

Arribats a aquesta pantalla gairebe inicial, aqui es on es pot escollir l'idioma del sistema operatiu i despres si el que es vol fer es la instal·lació o nomes probar-lo, que seria el mateix que dir que ens genera un sistema operatiu portable i que en parar-ho desapareix completament. En aquest cas polsarem sobre el boto Instalar Ubuntu i començara la instal·lació del sistema operatiu.

Continuant amb la instal·lació finalment s'arriba a la pantalla possiblement mes important de la instal·lació que es la creació de les particions. Les particions finalment han quedat de la seguent manera.

![Pantalla de particions](../imatges/pantalla_particions_ubuntu.jpg)

### Esquema de particions per a la instal·lació d’Ubuntu

Durant la instal·lació d’Ubuntu, s’ha optat per la **creació manual de particions**, definint un esquema adaptat a un disc dur virtual de 80 GB. Aquest esquema permet al sistema funcionar correctament i tenir una bona organització dels espais de memòria.

#### Particions creades

- **/dev/sda1 → Partició EFI (799 MB, tipus ext4)**
  - Aquesta partició és necessària quan s’utilitza el sistema d’arrencada **UEFI** que es la que s'ha activat a l'hora de crear la maquina virtual.  
  - Conté els fitxers essencials perquè l’ordinador pugui iniciar el carregador d’arrencada (GRUB en el cas d’Ubuntu).  
  - Encara que sembli petita, es suficient i és imprescindible per a l’arrencada del sistema.

- **/dev/sda2 → Partició arrel “/” (38 GB, ext4)**
  - Aquesta és la partició principal on s’instal·la el sistema operatiu.  
  - Conté tots els directoris del sistema (`/home`, `/bin`, `/etc`, etc.) i les aplicacions.  
  - S’ha escollit el sistema de fitxers **ext4**, el més habitual en Linux, ja que és robust, eficient i amb bona gestió de journaling.

- **/dev/sda3 → Partició swap (4 GB)**
  - Espai reservat per al **swap**, que actua com a memòria virtual addicional quan la memòria RAM física no és suficient.  
  - També és útil per permetre la funció d’**hibernació** (guardar l’estat de la sessió al disc).  
  - En aquest cas s’han assignat 4 GB, una mida adequada per a un sistema amb 8 Gb de RAM com el de la maquina virtual.

- **Espai lliure (43.098 MB)**
  - Encara hi ha espai disponible al disc dur virtual per crear noves particions si cal, per exemple:
    - Una partició **/home** separada per a les dades dels usuaris. En aquest cas no s'ha creat aquesta particio per la qual cosa quedara inclosa a la particio arrel.
    - Una partició addicional per a proves o altres sistemes.  

#### El sistema de particions en Linux

En Linux, a diferència de Windows, no s’utilitzen lletres de unitat (com `C:` o `D:`).  
Tot el sistema s’organitza sota un únic **arbre de directoris**, que comença a la **arrel “/”**.  

- **/** → Punt de muntatge principal (arrel).  
- **/boot o EFI** → Fitxers d’arrencada del sistema.  
- **/home** → Carpeta dels usuaris (opcions de configuració i fitxers personals).  
- **swap** → Espai de memòria virtual.  

Aquest model flexible permet dividir el disc en diferents particions segons les necessitats, millorant el rendiment, la seguretat i la gestió del sistema.

---

#### Resum

En aquest cas s’ha creat un esquema simple però funcional:
- **EFI** per a l’arrencada.  
- **/** com a partició principal del sistema i carpeta **home** (38 GB).  
- **swap** per a memòria virtual (4 GB).  
- **Espai lliure** per a futures ampliacions.  

Aquesta organització garanteix que Ubuntu s’instal·li correctament i que el sistema pugui arrencar i funcionar amb estabilitat.

Despres de la creació de les particions ja s'inicia la instal·lació del sistema operatiu i es configuren la resta d'opcions de instal·lació del sistema operatiu. Ja gairebe al final de la instal·lació nomes queda la creació de l'usuari aixi com el nom que se li donara al equip.

![Imatge de la creació de l'usuari i nom de l'equip](../imatges/imatge_creacio_usuari.jpg)

### Creació de l’usuari principal a Ubuntu

Aquesta pantalla estableix tant la informació d’identitat com les credencials que s’utilitzaran per iniciar sessió i administrar el sistema.

#### Camps configurables

- **El seu nom** Es tracta del nom complet de la persona usuària (en aquest cas, *Jesus*).  
  Aquest nom es mostra en l’entorn gràfic i a les pantalles de benvinguda.

- **El nom de l’equip** Identifica l’ordinador dins de la xarxa.  
  En aquest cas, s’ha assignat *jesus-VirtualBox*, de manera que altres dispositius poden reconèixer aquest equip quan es connecta a una xarxa.

- **Nom d’usuari** És l’identificador que s’utilitza per iniciar sessió i a la terminal.  
  Sol ser en minúscules i sense espais (per exemple, *jesus*).  
  Aquest usuari tindrà permisos d’administració mitjançant l’ordre `sudo`.

- **Contrasenya** Clau d’accés que protegeix l’usuari.  
  Ha de ser prou robusta (combinació de lletres, números i símbols) per garantir la seguretat del sistema.  
  També es demana repetir-la per evitar errors de tecleig.

#### Opcions d’inici de sessió

- **Iniciar sessió automàticament** L’usuari accedeix al sistema sense introduir la contrasenya cada vegada que arrenca l’ordinador.  
  Pot ser còmode, però menys segur.

- **Sol·licitar contrasenya per iniciar sessió** El sistema demana sempre la contrasenya en arrencar.  
  És la opció **més recomanada** per protegir l’equip i les dades.

- **Utilitzar Active Directory** Permet connectar l’ordinador a un **domini corporatiu de Microsoft Active Directory**.  
  Aquesta opció no és necessària en entorns domèstics o d’ús personal, però sí en xarxes d’empresa on els usuaris i permisos es gestionen centralitzadament.

#### Importància d’aquest pas

Aquest és un dels punts més importants de la instal·lació:
- Es defineix **l’usuari principal** del sistema, que serà l’administrador inicial.  
- Es configura la **seguretat d’accés** amb una contrasenya robusta.  
- Es determina com es **presentarà l’equip a la xarxa** (nom de l’ordinador).  

Una configuració correcta aquí garanteix que el sistema estigui protegit i preparat per treballar tant en entorns personals com en xarxes més grans.

Despres d'aixo ja tindriem configurat l'Ubuntu i nomes quedaria la personalització de l'usuari per a que aparegui la pantalla de l'escritori i puguem donar per acabada la instal·lació del sistema operatiu. Despres d'acabar la instal·lació seria necessaria la instal·lacio de les Guest Additions i les actualitzacions corresponents.

# Llicenciament

Per tal de poder veure el llicenciament d'Ubuntu es pot lleguir el fitxer [license.md](license.md)

# Gestors d'arrencada per a instal·lacions DUALS
# Punts de restauració
# Configuració de la xarxa
# Comandes generals i instal·lacions
