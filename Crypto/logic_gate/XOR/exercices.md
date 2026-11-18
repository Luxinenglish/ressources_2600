# 📝 Exercices — XOR

[🏠 Index](../../../index.md)

> **Cours :** [simple_xor.md](simple_xor.md) · Les corrigés sont dans les blocs repliables ▶

## Exercice 1 — Calculs 🟢

1. `1010 ⊕ 0110`
2. `0xF0 ⊕ 0x3C`

<details>
<summary>Corrigé</summary>

1. `1010 ⊕ 0110` = **`1100`**
2. `1111 0000 ⊕ 0011 1100` = `1100 1100` = **`0xCC`**

</details>

## Exercice 2 — Simplifier 🟢

Simplifier (A et B sont des bits) :

1. `A ⊕ B ⊕ A`
2. `A ⊕ 1`
3. `A ⊕ A ⊕ A`

<details>
<summary>Corrigé</summary>

1. `A ⊕ A ⊕ B = 0 ⊕ B` = **`B`** (commutativité puis auto-inverse)
2. **`NOT A`** (si A = 0 → 1, si A = 1 → 0)
3. `(A ⊕ A) ⊕ A = 0 ⊕ A` = **`A`**

</details>

## Exercice 3 — Chiffrer / déchiffrer 🟢

1. Chiffrer la lettre `A` (`0x41`) avec la clé `0x20`.
2. Déchiffrer le résultat avec la même clé.

<details>
<summary>Corrigé</summary>

1. `0100 0001 ⊕ 0010 0000 = 0110 0001` = **`0x61`** (c'est la lettre `a` !)
2. `0x61 ⊕ 0x20 = 0x41` = **`A`** → on retrouve le message : chiffrer et déchiffrer, c'est la même opération.

</details>

## Exercice 4 — Retrouver la clé 🟡

Un message de 5 lettres a été chiffré avec une clé d'**un seul octet**. Le chiffré est :

```
51 41 52 45 5c
```

On sait que le message commence par la lettre `B` (`0x42`). Retrouver la clé, puis le message.

<details>
<summary>Corrigé</summary>

`clé = chiffré ⊕ clair = 0x51 ⊕ 0x42` → `0101 0001 ⊕ 0100 0010 = 0001 0011` = **`0x13`**

On déchiffre tout avec `0x13` :

```python
chiffre = bytes.fromhex("51 41 52 45 5c")
print(bytes(c ^ 0x13 for c in chiffre))   # b'BRAVO'
```

Message : **`BRAVO`**

</details>

## Exercice 5 — Échanger deux variables 🟡

Que contiennent `a` et `b` à la fin ? Justifier.

```python
a, b = 12, 7
a = a ^ b
b = a ^ b
a = a ^ b
```

<details>
<summary>Corrigé</summary>

- ligne 2 : `a = 12 ⊕ 7`
- ligne 3 : `b = (12 ⊕ 7) ⊕ 7 = 12`
- ligne 4 : `a = (12 ⊕ 7) ⊕ 12 = 7`

➡️ **`a = 7`, `b = 12`** : les deux variables ont été échangées sans variable temporaire.

</details>

## Exercice 6 — Réutiliser la clé 🔴

Deux messages `M1` et `M2` sont chiffrés avec **la même clé** `K` : `C1 = M1 ⊕ K` et `C2 = M2 ⊕ K`.
Que vaut `C1 ⊕ C2` ? Pourquoi est-ce un problème ?

<details>
<summary>Corrigé</summary>

`C1 ⊕ C2 = M1 ⊕ K ⊕ M2 ⊕ K = M1 ⊕ M2 ⊕ (K ⊕ K) = M1 ⊕ M2`

➡️ **La clé disparaît.** Avec les deux chiffrés seulement, on obtient le XOR des deux messages clairs. Si on connaît (ou devine) `M1`, on retrouve directement `M2`.
C'est pour ça que la clé du One-Time Pad ne doit **jamais** être réutilisée.

</details>
