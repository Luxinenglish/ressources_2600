# ➗ Arithmétique modulaire

> **Niveau :** débutant → intermédiaire · **Prérequis :** division euclidienne

C'est **la** boîte à outils mathématique de la crypto (César, Vigenère, RSA, Diffie-Hellman…).

## Le modulo

`a mod n` = le **reste** de la division euclidienne de `a` par `n`. Le résultat est toujours entre `0` et `n − 1`.

```
17 = 3 × 5 + 2   →   17 mod 5 = 2
```

| Calcul | Résultat |
|---|:-:|
| `17 mod 5` | 2 |
| `100 mod 7` | 2 |
| `26 mod 26` | 0 |
| `−3 mod 7` | **4** (on ajoute 7 jusqu'à être positif : −3 + 7 = 4) |

💡 Une horloge, c'est du modulo 12 : 10 h + 5 h = 15 mod 12 = **3 h**.

### Congruence

`a ≡ b (mod n)` signifie que `a` et `b` ont **le même reste** modulo `n` (autrement dit `n` divise `a − b`).
Exemple : `17 ≡ 2 (mod 5)` et `26 ≡ 0 (mod 26)`.

### Règles de calcul

On peut réduire **à chaque étape** :

```
(a + b) mod n = ((a mod n) + (b mod n)) mod n
(a × b) mod n = ((a mod n) × (b mod n)) mod n
```

Exemple : `(123 × 456) mod 10 = (3 × 6) mod 10 = 18 mod 10 = 8`

## PGCD et algorithme d'Euclide

Le **PGCD** est le plus grand diviseur commun. Euclide : `pgcd(a, b) = pgcd(b, a mod b)`, et on s'arrête quand le reste vaut 0.

```
pgcd(252, 105) :
252 = 2 × 105 + 42
105 = 2 × 42  + 21
 42 = 2 × 21  + 0    →  pgcd = 21  (dernier reste non nul)
```

Deux nombres sont **premiers entre eux** si leur PGCD vaut **1**.

## Inverse modulaire

L'inverse de `a` modulo `n` est le nombre `a⁻¹` tel que :

```
a × a⁻¹ ≡ 1 (mod n)
```

Exemple : `3 × 4 = 12 ≡ 1 (mod 11)` donc l'inverse de 3 modulo 11 est **4**.

⚠️ L'inverse **existe seulement si `pgcd(a, n) = 1`**. Exemple : 2 n'a pas d'inverse modulo 26.

### Le trouver : Euclide étendu

On cherche l'inverse de **7 modulo 26**.

**1. Euclide classique :**
```
26 = 3 × 7 + 5
 7 = 1 × 5 + 2
 5 = 2 × 2 + 1     → pgcd = 1, l'inverse existe
```

**2. On remonte** pour écrire 1 en fonction de 26 et 7 :
```
1 = 5 − 2 × 2
  = 5 − 2 × (7 − 5)          = 3 × 5 − 2 × 7
  = 3 × (26 − 3 × 7) − 2 × 7 = 3 × 26 − 11 × 7
```

Donc `−11 × 7 ≡ 1 (mod 26)` → inverse = `−11 mod 26` = **15**.
Vérification : `7 × 15 = 105 = 4 × 26 + 1` ✅

## Exponentiation modulaire rapide

Calculer `3¹³ mod 7` sans calculer 3¹³ en entier : **exponentiation par carrés successifs**.

1. On écrit l'exposant en binaire : `13 = 8 + 4 + 1`
2. On calcule les carrés successifs, en réduisant à chaque fois :
```
3¹ ≡ 3
3² ≡ 9  ≡ 2
3⁴ ≡ 2² = 4
3⁸ ≡ 4² = 16 ≡ 2      (mod 7)
```
3. On multiplie ceux dont on a besoin : `3¹³ = 3⁸ × 3⁴ × 3¹ ≡ 2 × 4 × 3 = 24 ≡ 3 (mod 7)`

### Petit théorème de Fermat

Si `p` est premier et `a` non multiple de `p` : **`a^(p−1) ≡ 1 (mod p)`**.
Exemple : `2⁶ = 64 = 9 × 7 + 1 ≡ 1 (mod 7)` ✅

## En Python

```python
print(17 % 5)            # 2
print(-3 % 7)            # 4  (Python donne toujours un résultat positif)

import math
print(math.gcd(252, 105))  # 21

print(pow(7, -1, 26))    # 15  inverse modulaire (Python ≥ 3.8)
print(pow(3, 13, 7))     # 3   exponentiation modulaire rapide
```

## ✅ À retenir

- `a mod n` = reste, toujours entre 0 et n − 1
- On peut réduire modulo n **à chaque étape** d'un calcul
- Inverse de `a` mod `n` : existe **ssi pgcd(a, n) = 1**, se calcule avec **Euclide étendu**
- Grandes puissances : **carrés successifs**

📝 [Exercices corrigés](exercices.md) · ➡️ Application : [RSA](../asymetrique/rsa/rsa.md)
