# 🔒 Chiffrement symétrique

[🏠 Index](../../index.md)

> **Niveau :** débutant → intermédiaire · **Prérequis :** [introduction](../introduction/notions_de_base.md), [XOR](../logic_gate/XOR/simple_xor.md)

## Principe

**La même clé** sert à chiffrer et à déchiffrer. Alice et Bob doivent donc partager cette clé secrète **à l'avance**.

```
          clé K                     clé K
Alice : M ──[chiffrer]──► C ──────► [déchiffrer]──► M : Bob
```

## Chiffrement par flot vs par blocs

| | Par flot (*stream*) | Par blocs (*block*) |
|---|---|---|
| Fonctionnement | génère une suite de clé pseudo-aléatoire et fait **message ⊕ flot** | découpe le message en **blocs de taille fixe** et chiffre chaque bloc |
| Exemples | RC4 (cassé), **ChaCha20** | DES (obsolète), **AES** |

## Les algorithmes à connaître

| Algo | Année | Taille de bloc | Taille de clé | Statut |
|---|:-:|:-:|:-:|---|
| **DES** | 1977 | 64 bits | 56 bits | ❌ cassé (clé trop courte) |
| **3DES** | 1998 | 64 bits | 112 / 168 bits | ⚠️ obsolète |
| **AES** | 2001 | **128 bits** | **128, 192 ou 256 bits** | ✅ standard actuel |
| **ChaCha20** | 2008 | (flot) | 256 bits | ✅ utilisé dans TLS, WireGuard |

### Pourquoi la taille de clé compte

Une clé de *n* bits → **2ⁿ** clés possibles à tester en force brute.

| Clé | Nombre de clés | Force brute |
|---|---|---|
| 56 bits (DES) | 2⁵⁶ ≈ 7,2 × 10¹⁶ | quelques heures avec du matériel dédié |
| 128 bits (AES) | 2¹²⁸ ≈ 3,4 × 10³⁸ | impossible (plus que l'âge de l'univers) |

➡️ Chaque bit de clé en plus **double** le travail.

## Les modes d'opération (chiffrement par blocs)

Un message fait plusieurs blocs : le **mode** dit comment les enchaîner.

### ECB (*Electronic Code Book*) — ❌ à ne pas utiliser

Chaque bloc est chiffré **indépendamment** avec la même clé.

```
C₁ = E(K, M₁)    C₂ = E(K, M₂)    ...
```

⚠️ Deux blocs clairs identiques donnent **deux blocs chiffrés identiques** → on voit la structure du message (célèbre exemple : l'image du pingouin Linux chiffrée en ECB reste reconnaissable).

### CBC (*Cipher Block Chaining*)

Chaque bloc clair est XORé avec le **bloc chiffré précédent** avant d'être chiffré. Le premier bloc utilise un **IV** (vecteur d'initialisation) aléatoire.

```
C₁ = E(K, M₁ ⊕ IV)
C₂ = E(K, M₂ ⊕ C₁)
Cᵢ = E(K, Mᵢ ⊕ Cᵢ₋₁)
```

✅ Deux blocs identiques donnent des chiffrés différents. L'IV n'est pas secret mais doit être **imprévisible** et **différent à chaque message**.

### CTR et GCM

- **CTR** : transforme un chiffrement par blocs en chiffrement par flot (on chiffre un compteur, puis XOR avec le message).
- **GCM** : CTR + **authentification** (vérifie aussi l'intégrité). C'est le mode recommandé aujourd'hui (AES-GCM).

## Le problème de l'échange de clés

Pour *n* personnes qui veulent toutes communiquer deux à deux en secret, il faut une clé par paire :

```
nombre de clés = n × (n − 1) / 2
```

100 personnes → **4 950 clés** à échanger de façon sûre ! ➡️ C'est ce que résout la [cryptographie asymétrique](../asymetrique/rsa/rsa.md) ([Diffie-Hellman](../asymetrique/diffie_hellman/diffie_hellman.md)).

## En Python (pour voir, avec la lib `cryptography`)

```python
# pip install cryptography
from cryptography.hazmat.primitives.ciphers.aead import AESGCM
import os

cle = AESGCM.generate_key(bit_length=128)
nonce = os.urandom(12)                    # jamais deux fois le même avec la même clé !
aes = AESGCM(cle)

chiffre = aes.encrypt(nonce, b"Rendez-vous a midi", None)
print(aes.decrypt(nonce, chiffre, None))  # b'Rendez-vous a midi'
```

## ✅ À retenir

- Symétrique = **une seule clé partagée** ; rapide
- **AES** : blocs de 128 bits, clés de 128/192/256 bits. DES (56 bits) est cassé
- **ECB = fuite de structure** ; utiliser CBC (avec IV aléatoire) ou mieux **GCM**
- n personnes → **n(n−1)/2** clés : d'où le besoin de l'asymétrique

📝 [Exercices corrigés](exercices.md)
