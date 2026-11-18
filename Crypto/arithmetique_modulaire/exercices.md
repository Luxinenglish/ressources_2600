# 📝 Exercices — Arithmétique modulaire

> **Cours :** [arithmetique_modulaire.md](arithmetique_modulaire.md) · Les corrigés sont dans les blocs repliables ▶

## Exercice 1 — Modulo 🟢

Calculer : `23 mod 7` · `100 mod 7` · `−3 mod 7` · `−30 mod 26` · `52 mod 26`

<details>
<summary>Corrigé</summary>

| Calcul | Résultat | Détail |
|---|:-:|---|
| `23 mod 7` | **2** | 23 = 3 × 7 + 2 |
| `100 mod 7` | **2** | 100 = 14 × 7 + 2 |
| `−3 mod 7` | **4** | −3 + 7 = 4 |
| `−30 mod 26` | **22** | −30 + 2 × 26 = 22 |
| `52 mod 26` | **0** | 52 = 2 × 26 |

</details>

## Exercice 2 — Réduire avant de calculer 🟢

Calculer **sans calculatrice** :

1. `(1234 + 5678) mod 10`
2. `(97 × 98) mod 5`
3. `2¹⁰ mod 7`

<details>
<summary>Corrigé</summary>

1. `(4 + 8) mod 10 = 12 mod 10` = **2**
2. 97 ≡ 2 et 98 ≡ 3 (mod 5) → `2 × 3 = 6 mod 5` = **1**
3. `2³ = 8 ≡ 1 (mod 7)` → `2¹⁰ = (2³)³ × 2 ≡ 1 × 2` = **2**

</details>

## Exercice 3 — PGCD 🟢

Calculer avec l'algorithme d'Euclide :

1. `pgcd(120, 84)`
2. `pgcd(26, 15)` — sont-ils premiers entre eux ?

<details>
<summary>Corrigé</summary>

1.
```
120 = 1 × 84 + 36
 84 = 2 × 36 + 12
 36 = 3 × 12 + 0    → pgcd = 12
```

2.
```
26 = 1 × 15 + 11
15 = 1 × 11 + 4
11 = 2 × 4  + 3
 4 = 1 × 3  + 1
 3 = 3 × 1  + 0     → pgcd = 1
```
**Oui**, 26 et 15 sont premiers entre eux.

</details>

## Exercice 4 — Inverse « à tâtons » 🟢

Trouver l'inverse de 3 modulo 11 en testant les valeurs.

<details>
<summary>Corrigé</summary>

On cherche x tel que `3x ≡ 1 (mod 11)` :
3×1=3, 3×2=6, 3×3=9, 3×4=12 ≡ **1** ✅ → inverse = **4**

</details>

## Exercice 5 — Existence de l'inverse 🟡

Parmi `2, 3, 13, 15`, lesquels ont un inverse modulo 26 ?

<details>
<summary>Corrigé</summary>

26 = 2 × 13. Un nombre a un inverse mod 26 ssi il n'est divisible **ni par 2 ni par 13**.

- 2 → pgcd = 2 → **non**
- 3 → pgcd = 1 → **oui** (inverse 9, car 27 ≡ 1)
- 13 → pgcd = 13 → **non**
- 15 → pgcd = 1 → **oui** (inverse 7, car 105 ≡ 1)

</details>

## Exercice 6 — Euclide étendu 🟡

Calculer l'inverse de **5 modulo 72** avec l'algorithme d'Euclide étendu.

<details>
<summary>Corrigé</summary>

```
72 = 14 × 5 + 2
 5 = 2 × 2  + 1     → pgcd = 1

1 = 5 − 2 × 2
  = 5 − 2 × (72 − 14 × 5)
  = 29 × 5 − 2 × 72
```

Donc `29 × 5 ≡ 1 (mod 72)` → inverse = **29**.
Vérification : `5 × 29 = 145 = 2 × 72 + 1` ✅

</details>

## Exercice 7 — Exponentiation rapide 🟡

Calculer `3¹³ mod 7` puis `5²¹ mod 11` par carrés successifs.

<details>
<summary>Corrigé</summary>

**3¹³ mod 7** : 13 = 8 + 4 + 1
3¹ ≡ 3, 3² ≡ 2, 3⁴ ≡ 4, 3⁸ ≡ 2 → `2 × 4 × 3 = 24 ≡` **3**

**5²¹ mod 11** : 21 = 16 + 4 + 1
5¹ ≡ 5, 5² = 25 ≡ 3, 5⁴ ≡ 9, 5⁸ ≡ 81 ≡ 4, 5¹⁶ ≡ 16 ≡ 5
→ `5¹⁶ × 5⁴ × 5¹ ≡ 5 × 9 × 5 = 225 = 20 × 11 + 5 ≡` **5**

(Avec Fermat : 5¹⁰ ≡ 1 (mod 11) donc 5²¹ = (5¹⁰)² × 5 ≡ 5 ✅)

</details>

## Exercice 8 — Fermat 🔴

Sans calculatrice, calculer `7²²² mod 11`.

<details>
<summary>Corrigé</summary>

11 est premier et 7 n'est pas multiple de 11 → Fermat : `7¹⁰ ≡ 1 (mod 11)`.
222 = 22 × 10 + 2 → `7²²² = (7¹⁰)²² × 7² ≡ 1 × 49 = 4 × 11 + 5 ≡` **5**

</details>
