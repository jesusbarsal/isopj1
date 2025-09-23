layout: default
title: "Modes de xarxa a VirtualBox"

VirtualBox ofereix diferents opcions per configurar la xarxa d’una màquina virtual. Cada mode té avantatges i inconvenients segons l’ús que es vulgui donar a la màquina virtual. A continuació es descriuen les principals opcions.

---

## 1. NAT (Network Address Translation)

El mode **NAT** és l’opció configurada per defecte a VirtualBox i també la més senzilla d’utilitzar.

### Característiques:
- La màquina virtual rep una **IP privada** dins d’una xarxa virtual creada pel mateix VirtualBox.  
- Les connexions a Internet es fan a través de la IP de l’amfitrió, que actua com a “router”.  
- El convidat pot accedir a Internet sense necessitat de cap configuració addicional.  
- Els equips de la xarxa física **no poden veure ni connectar-se** directament a la màquina virtual.  

### Avantatges:
- Configuració automàtica i molt senzilla.  
- Funciona en qualsevol entorn (Wi-Fi, xarxes d’empresa, etc.).  
- Aporta una capa de seguretat: la màquina virtual queda amagada darrere de l’amfitrió.  

### Inconvenients:
- La màquina virtual **no és accessible des de la xarxa física**.  
- Per permetre connexions entrants cal configurar regles de “port forwarding” manualment.

---

## 2. Adaptador pont (Bridged Adapter)

El mode **Adaptador pont** connecta la màquina virtual directament a la xarxa física, com si fos un ordinador més.

### Característiques:
- La màquina virtual rep una **IP de la mateixa xarxa que l’amfitrió**, normalment assignada pel router físic via DHCP.  
- Els equips de la xarxa física poden veure i connectar-se a la màquina virtual.  
- El trànsit passa directament per la targeta de xarxa de l’amfitrió.  

### Avantatges:
- La màquina virtual funciona com un equip més de la xarxa.  
- Permet compartir fitxers i serveis directament amb altres dispositius de la LAN.  
- Ideal per a servidors, proves de serveis de xarxa i laboratoris realistes.  

### Inconvenients:
- Pot no funcionar correctament en algunes xarxes Wi-Fi que bloquegen el mode pont.  
- La màquina virtual queda exposada a la xarxa i pot ser més vulnerable.  
- Requereix que hi hagi IPs disponibles al mateix rang que l’amfitrió.

---

## 3. Xarxa interna (Internal Network)

El mode **Xarxa interna** crea una xarxa completament aïllada entre màquines virtuals dins del mateix amfitrió.

### Característiques:
- Les màquines virtuals connectades a la mateixa “Internal Network” poden comunicar-se entre elles.  
- No hi ha connexió a Internet ni a la xarxa de l’amfitrió.  
- És com si fos una LAN virtual independent.  

### Avantatges:
- Total aïllament respecte a l’amfitrió i la xarxa externa.  
- Ideal per a **laboratoris de proves de xarxa** o entorns on es vol garantir que no hi hagi connexió amb l’exterior.  
- Permet simular xarxes complexes sense riscos.  

### Inconvenients:
- Sense connexió a Internet per defecte.  
- Per sortir a Internet caldria configurar un router virtual dins de la mateixa xarxa interna.

---

## 4. NAT Network

El mode **NAT Network** és una combinació entre NAT i xarxa interna.

### Característiques:
- Diverses màquines virtuals poden compartir una mateixa xarxa interna creada per VirtualBox.  
- Cada màquina rep una IP pròpia dins d’aquesta xarxa virtual.  
- Poden comunicar-se entre elles **i** també accedir a Internet a través de l’amfitrió.  

### Avantatges:
- Més flexible que el NAT tradicional: permet comunicació entre màquines convidades.  
- Les màquines convidades tenen sortida a Internet sense configuració complicada.  
- És ideal per a simular una xarxa local amb diversos equips connectats.  

### Inconvenients:
- Encara queden amagades respecte a la xarxa física.  
- Per fer-les accessibles des de fora cal configurar port forwarding.

---

# Resum comparatiu

| Mode             | Connexió a Internet | Accessible des de la LAN física | Comunicació entre màquines virtuals | Ús recomanat |
|------------------|---------------------|---------------------------------|------------------------------------|--------------|
| **NAT**          | Sí                  | No                              | No (només amb port forwarding)     | Ús bàsic, seguretat i simplicitat |
| **Adaptador pont** | Sí                  | Sí                              | Sí                                 | Servidors, proves reals en xarxa |
| **Xarxa interna** | No                  | No                              | Sí                                 | Laboratoris aïllats, proves de xarxa |
| **NAT Network**  | Sí                  | No                              | Sí                                 | Simular LAN amb accés a Internet |

---

En conclusió, l’opció més recomanada per defecte és **NAT**, per simplicitat i seguretat.  
Si es necessita que la màquina virtual sigui visible a la xarxa física, s'ha d’utilitzar **Adaptador pont**.  
Per a laboratoris aïllats, la millor opció és **Xarxa interna**, i si es vol una LAN virtual amb Internet entre diverses màquines, la millor és **NAT Network**.
