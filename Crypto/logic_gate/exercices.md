# 📝 Exercices — Portes logiques

[🏠 Index](../../index.md)

> **Cours :** [README.md](README.md) · Les corrigés sont dans les blocs repliables ▶

## Exercice 1 — Table de vérité 🟢

Dresser la table de vérité de : `S = (A AND B) OR (NOT A)`

<details>
<summary>Corrigé</summary>

| A | B | A AND B | NOT A | S |
|:-:|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 1 | **1** |
| 0 | 1 | 0 | 1 | **1** |
| 1 | 0 | 0 | 0 | **0** |
| 1 | 1 | 1 | 0 | **1** |

Remarque : S vaut 0 uniquement quand A = 1 et B = 0 (c'est « A implique B »).

</details>

## Exercice 2 — Calcul bit à bit sur 8 bits 🟢

Avec `x = 1100 1010` (`0xCA`), calculer :

1. `x AND 0000 1111`
2. `x OR 0000 1111`
3. `x XOR 1111 1111`

<details>
<summary>Corrigé</summary>

```
  1100 1010        1100 1010        1100 1010
& 0000 1111      | 0000 1111      ^ 1111 1111
-----------      -----------      -----------
  0000 1010        1100 1111        0011 0101
```

1. **`0000 1010`** (`0x0A`) → le AND a gardé les 4 bits de droite
2. **`1100 1111`** (`0xCF`) → le OR a forcé les 4 bits de droite à 1
3. **`0011 0101`** (`0x35`) → le XOR avec que des 1 inverse tous les bits (= NOT)

</details>

## Exercice 3 — En décimal 🟢

Calculer (passer par le binaire) :

1. `13 & 6`
2. `13 | 6`
3. `13 ^ 6`
4. `5 << 3`
5. `40 >> 2`

<details>
<summary>Corrigé</summary>

`13 = 1101` et `6 = 0110`

1. `1101 & 0110 = 0100` → **4**
2. `1101 | 0110 = 1111` → **15**
3. `1101 ^ 0110 = 1011` → **11**
4. décaler de 3 à gauche = × 2³ → 5 × 8 = **40**
5. décaler de 2 à droite = ÷ 2² → 40 / 4 = **10**

</details>

## Exercice 4 — Porte universelle 🟡

En n'utilisant **que des portes NAND**, construire :

1. NOT A
2. A AND B

<details>
<summary>Corrigé</summary>

Rappel : `A NAND B = NOT (A AND B)`

1. **`NOT A = A NAND A`** (car `A AND A = A`)
2. **`A AND B = (A NAND B) NAND (A NAND B)`** (on applique le NOT de la question 1 au résultat de `A NAND B`)

</details>

## Exercice 5 — Pair ou impair ? 🟡

Écrire une fonction Python `est_pair(n)` **sans utiliser `%`**, uniquement avec un opérateur bit à bit.

<details>
<summary>Corrigé</summary>

Un nombre est pair si son bit de poids faible vaut 0.

```python
def est_pair(n: int) -> bool:
    return n & 1 == 0

print(est_pair(10))  # True
print(est_pair(7))   # False
```

</details>
