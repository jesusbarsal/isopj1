---
layout: default
title: "És necessari crear una partició swap a Ubuntu?"
---

# És necessari crear una partició swap a Ubuntu?

Avui en dia, en les versions modernes d’Ubuntu (des de 17.04 fins a 24.04…), **ja no és necessari crear manualment una partició swap**.  
El sistema, per defecte, utilitza un **fitxer swap** en lloc d’una partició dedicada, que ofereix la mateixa funcionalitat i és més flexible de gestionar.  
Per tant, només caldria una partició swap en casos concrets, com ara quan es vol utilitzar la **hibernació** o en entorns molt específics.

---

## Objectius

- Entendre la diferència entre **partició swap** i **fitxer swap**.  
- Conèixer en quins casos és recomanable encara fer servir una partició.  
- Aprendre què fa servir Ubuntu de manera predeterminada.  

---

## Diferències entre fitxer swap i partició swap

Tot i que ambdós tenen la mateixa funció (actuar com a memòria virtual addicional quan la RAM s’esgota), hi ha algunes diferències:

| Característica     | Partició swap                          | Fitxer swap                                  |
|--------------------|----------------------------------------|----------------------------------------------|
| **Ubicació**       | Espai reservat en una partició del disc | Fitxer normal dins de la partició arrel (`/`) |
| **Ús per defecte** | Antigament (fins Ubuntu 18.04)          | Actualment (Ubuntu 20.04+)                    |
| **Flexibilitat**   | Difícil de modificar (cal redimensionar particions) | Es pot ampliar o reduir fàcilment   |
| **Hibernació**     | Recomanada si es vol hibernar           | També possible, però requereix configuració   |
| **Ús recomanat**   | Equips antics o amb poca RAM            | Equips moderns i ús general                   |

---

## Exemple pràctic

Per veure si el teu Ubuntu està fent servir *swapfile* o partició swap:

```bash
swapon --show
``` 

### Resum
- **Avui en dia no cal crear partició swap**: Ubuntu ja gestiona automàticament la memòria virtual amb un **fitxer swap**.  
- **Partició swap** només és necessària en situacions específiques (hibernació o equips antics).  
- El **fitxer swap** és suficient en la majoria de casos i és l’opció per defecte.
