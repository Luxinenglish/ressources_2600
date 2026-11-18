# 🔌 Portes logiques

> **Niveau :** débutant · **Prérequis :** savoir ce qu'est un bit (`0` ou `1`)

Une **porte logique** prend un ou plusieurs bits en entrée et renvoie un bit en sortie.
C'est la base de l'électronique… et de la cryptographie.

## Les portes de base

### NOT (NON) — inverse le bit

| A | NOT A |
|:-:|:-----:|
| 0 | 1 |
| 1 | 0 |

Python : `~a` (attention, sur les entiers Python ça donne `-a-1`) → pour un bit utilisez `1 - a` ou `a ^ 1`.

### AND (ET) — 1 si **les deux** sont à 1

| A | B | A AND B |
|:-:|:-:|:-------:|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | **1** |

Python : `a & b` · Usage : **masquer** des bits (`x & 0x0F` garde les 4 bits de poids faible).

### OR (OU) — 1 si **au moins un** est à 1

| A | B | A OR B |
|:-:|:-:|:------:|
| 0 | 0 | 0 |
| 0 | 1 | **1** |
| 1 | 0 | **1** |
| 1 | 1 | **1** |

Python : `a | b` · Usage : **forcer** des bits à 1.

### XOR (OU exclusif) — 1 si les bits sont **différents**

| A | B | A XOR B |
|:-:|:-:|:-------:|
| 0 | 0 | 0 |
| 0 | 1 | **1** |
| 1 | 0 | **1** |
| 1 | 1 | 0 |

Python : `a ^ b` · Usage : **chiffrement**, inverser des bits. 👉 [Fiche complète sur le XOR](XOR/simple_xor.md)

## Les portes composées

| Porte | Définition | Sortie pour (00, 01, 10, 11) |
|---|---|---|
| **NAND** | NOT (A AND B) | 1, 1, 1, 0 |
| **NOR** | NOT (A OR B) | 1, 0, 0, 0 |
| **XNOR** | NOT (A XOR B) | 1, 0, 0, 1 |

💡 **NAND** et **NOR** sont dites *universelles* : on peut construire **toutes** les autres portes uniquement avec l'une d'elles.

## Récap des opérateurs bit à bit en Python

```python
a, b = 0b1100, 0b1010

print(bin(a & b))   # 0b1000   AND
print(bin(a | b))   # 0b1110   OR
print(bin(a ^ b))   # 0b110    XOR
print(bin(a << 1))  # 0b11000  décalage à gauche (×2)
print(bin(a >> 2))  # 0b11     décalage à droite (÷4)
```

## 📂 Dans ce dossier

- [exercices.md](exercices.md) — exercices corrigés sur les portes logiques
- [XOR/simple_xor.md](XOR/simple_xor.md) — le XOR et le chiffrement XOR
