# 🔀 XOR simple

> **Niveau :** débutant · **Prérequis :** [portes logiques](../README.md), [binaire & hexadécimal](../../encodage/bases_encodage.md)

## C'est quoi le XOR ?

Le **XOR** (*eXclusive OR*, « OU exclusif ») est une opération logique qui renvoie `1`
**si et seulement si les deux bits sont différents**.

| A | B | A ⊕ B |
|:-:|:-:|:-----:|
| 0 | 0 | **0** |
| 0 | 1 | **1** |
| 1 | 0 | **1** |
| 1 | 1 | **0** |

On le note `⊕` en maths et `^` dans la plupart des langages (Python, C, JS…).

## XOR sur des octets

On applique le XOR **bit à bit** :

```
  0100 1000   (0x48, 'H')
⊕ 0010 1010   (0x2A, la clé)
-----------
  0110 0010   (0x62, 'b')
```

## Les 4 propriétés à connaître par cœur

| Propriété | Formule | Ce que ça veut dire |
|---|---|---|
| Élément neutre | `A ⊕ 0 = A` | XOR avec 0 ne change rien |
| Auto-inverse | `A ⊕ A = 0` | XOR avec soi-même donne 0 |
| Commutativité | `A ⊕ B = B ⊕ A` | l'ordre ne compte pas |
| Associativité | `(A ⊕ B) ⊕ C = A ⊕ (B ⊕ C)` | on peut regrouper comme on veut |

👉 Conséquence magique :

```
chiffré = message ⊕ clé
chiffré ⊕ clé = message ⊕ clé ⊕ clé = message ⊕ 0 = message
```

**Chiffrer et déchiffrer, c'est la même opération.**

Et encore mieux pour un attaquant :

```
chiffré ⊕ message = clé
```

➡️ Si on connaît (ou devine) une partie du message clair, on retrouve la clé. C'est l'attaque à **clair connu** (*known plaintext*).

## Chiffrement XOR à clé d'un octet

La clé est un seul octet (256 possibilités : `0x00` → `0xFF`), répété sur tout le message.

```python
message = b"Hello 2600"
key = 0x2A

chiffre = bytes(b ^ key for b in message)
print(chiffre.hex())        # 624f4646450a181c1a1a

dechiffre = bytes(b ^ key for b in chiffre)
print(dechiffre)            # b'Hello 2600'
```

### Le casser par bruteforce

Seulement 256 clés → on les teste toutes et on garde ce qui ressemble le plus à du texte.

```python
chiffre = bytes.fromhex("624f4646450a181c1a1a")

def score(data: bytes) -> int:
    # +1 pour chaque lettre, chiffre ou espace : plus c'est haut, plus ça ressemble à du texte
    return sum(bytes([c]).isalnum() or c == 32 for c in data)

resultats = []
for key in range(256):
    candidat = bytes(b ^ key for b in chiffre)
    resultats.append((score(candidat), key, candidat))

for s, key, candidat in sorted(resultats, reverse=True)[:5]:
    print(s, hex(key), candidat)   # la bonne clé (0x2a) est en tête
```

## Chiffrement XOR à clé répétée

La clé fait plusieurs octets et on la répète en boucle :

```
message : H  e  l  l  o     2  6  0  0
clé     : K  E  Y  K  E  Y  K  E  Y  K
```

```python
from itertools import cycle

def xor(data: bytes, key: bytes) -> bytes:
    return bytes(d ^ k for d, k in zip(data, cycle(key)))

c = xor(b"Hello 2600", b"KEY")
print(xor(c, b"KEY"))       # b'Hello 2600'
```

💡 **Astuce CTF :** les flags commencent souvent par un format connu (`flag{`, `CTF{`, …).
`chiffré[:5] ⊕ b"flag{"` donne directement les 5 premiers octets de la clé !

## Pourquoi c'est important ?

- Le XOR est la brique de base de **presque tous** les chiffrements modernes (AES, ChaCha20, modes CTR/CBC…).
- Utilisé seul avec une clé courte ou réutilisée → **pas sûr du tout**.
- Utilisé avec une clé aléatoire, aussi longue que le message et **jamais réutilisée** → c'est le **One-Time Pad**, prouvé incassable.

## Outils pratiques

- [CyberChef](https://gchq.github.io/CyberChef/) — recette « XOR » et « XOR Brute Force »
- [xortool](https://github.com/hellman/xortool) — devine la longueur de la clé et la clé
- Python : l'opérateur `^`, `bytes.fromhex()`, `itertools.cycle`

## ✅ À retenir

- `A ⊕ B` = 1 si les bits sont différents
- `A ⊕ A = 0` et `A ⊕ 0 = A` → chiffrer = déchiffrer
- Clé d'1 octet → bruteforce (256 essais)
- Clair connu → `chiffré ⊕ clair = clé`
