# #️⃣ Fonctions de hachage

[🏠 Index](../../index.md)

> **Niveau :** débutant · **Prérequis :** [bases & encodages](../encodage/bases_encodage.md)

## Principe

Une fonction de hachage transforme une donnée **de taille quelconque** en une **empreinte** (*hash*, *condensat*) de **taille fixe**.

```
"bonjour"   ──SHA-256──►  2cb4b1431b84ec15d35ed83bb927e27e8967d75f4bcd9cc4b25c8d879ae23e18
un film 4 Go ──SHA-256──►  (toujours 64 caractères hexa = 256 bits)
```

⚠️ **Ce n'est pas un chiffrement** : il n'y a **pas de clé** et on ne peut **pas « déhacher »**.

## Les propriétés d'une bonne fonction de hachage

| Propriété | Signification |
|---|---|
| **Déterministe** | même entrée → toujours la même empreinte |
| **Rapide** à calculer | |
| **Résistance à la préimage** (sens unique) | à partir de `h`, impossible de trouver `m` tel que `H(m) = h` |
| **Résistance à la seconde préimage** | à partir de `m₁`, impossible de trouver `m₂ ≠ m₁` avec le même hash |
| **Résistance aux collisions** | impossible de trouver **deux** messages quelconques avec le même hash |
| **Effet avalanche** | changer 1 bit de l'entrée change **~50 %** des bits de la sortie |

### Effet avalanche

```
bonjour → 2cb4b1431b84ec15d35ed83bb927e27e8967d75f4bcd9cc4b25c8d879ae23e18
Bonjour → 9172e8eec99f144f72eca9a568759580edadb2cfd154857f07e657569493bc44
```

Une seule majuscule → une empreinte complètement différente.

### Pourquoi il existe forcément des collisions

Il y a une infinité d'entrées possibles mais seulement 2²⁵⁶ sorties (principe des tiroirs). Les collisions **existent**, mais une bonne fonction rend impossible d'en **trouver** une.

## Les algorithmes à connaître

| Algo | Taille de sortie | Hexa | Statut |
|---|:-:|:-:|---|
| **MD5** | 128 bits | 32 caractères | ❌ cassé (collisions faciles) |
| **SHA-1** | 160 bits | 40 caractères | ❌ cassé (collision publiée en 2017) |
| **SHA-256** (famille SHA-2) | 256 bits | 64 caractères | ✅ |
| **SHA-3** | 224 à 512 bits | | ✅ |

💡 1 caractère hexa = 4 bits → longueur hexa = taille en bits / 4.

## À quoi ça sert ?

### 1. Vérifier l'intégrité d'un fichier

Le site publie le SHA-256 du fichier ; après téléchargement on recalcule et on compare.

```bash
sha256sum ubuntu.iso
```

### 2. Stocker des mots de passe

On ne stocke **jamais** un mot de passe en clair : on stocke son hash. À la connexion, on hache le mot de passe saisi et on compare.

**Problème :** deux utilisateurs avec le même mot de passe ont le même hash, et un attaquant peut utiliser des **tables précalculées** (*rainbow tables*) de hash de mots de passe courants.

**Solution : le sel (*salt*)** — une valeur aléatoire **unique par utilisateur**, stockée avec le hash :

```
hash stocké = H(sel + mot_de_passe)
```

| Utilisateur | Sel | Hash stocké |
|---|---|---|
| alice | `x9Fq` | H(`x9Fq` + `azerty`) |
| bob | `Lm2p` | H(`Lm2p` + `azerty`) → **différent** d'alice |

⚠️ Pour les mots de passe, on n'utilise **pas** SHA-256 seul (trop rapide → force brute facile) mais des fonctions **volontairement lentes** : **bcrypt**, **scrypt**, **Argon2**.

### 3. Signatures numériques, blockchain, Git…

On signe le **hash** d'un document plutôt que le document entier ([RSA](../asymetrique/rsa/rsa.md)). Git identifie chaque commit par un hash.

## En pratique

```bash
echo -n "bonjour" | sha256sum      # -n : sans le retour à la ligne final !
echo -n "bonjour" | md5sum
```

```python
import hashlib
print(hashlib.sha256(b"bonjour").hexdigest())
print(hashlib.md5(b"bonjour").hexdigest())   # f02368945726d5fc2a14eb576f7276c0
```

## ✅ À retenir

- Hachage : taille fixe, **sans clé**, **sens unique** (pas de déchiffrement)
- Propriétés : préimage, seconde préimage, collisions, avalanche
- **MD5 et SHA-1 sont cassés** → SHA-256 / SHA-3
- Mots de passe : **sel** + fonction lente (**bcrypt, Argon2**)

📝 [Exercices corrigés](exercices.md)
