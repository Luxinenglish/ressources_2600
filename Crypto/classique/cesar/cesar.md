# 🏛️ Chiffrement de César

[🏠 Index](../../../index.md)

> **Niveau :** débutant · **Prérequis :** [arithmétique modulaire](../../arithmetique_modulaire/arithmetique_modulaire.md) (juste le modulo)

## Principe

Chaque lettre est **décalée** d'un nombre fixe de positions dans l'alphabet. Ce décalage est la **clé** `k`.
Jules César utilisait `k = 3`.

```
Clair  : A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
Chiffré: D E F G H I J K L M N O P Q R S T U V W X Y Z A B C
```

`BONJOUR` → `ERQMRXU`

## Formules

On numérote les lettres : `A = 0, B = 1, …, Z = 25`.

```
Chiffrement : C = (M + k) mod 26
Déchiffrement : M = (C − k) mod 26
```

Le `mod 26` permet de « boucler » : `X (23) + 3 = 26 mod 26 = 0 → A`.

### Exemple à la main (k = 3)

| Lettre | B | O | N | J | O | U | R |
|---|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| M | 1 | 14 | 13 | 9 | 14 | 20 | 17 |
| M + 3 mod 26 | 4 | 17 | 16 | 12 | 17 | 23 | 20 |
| Chiffré | E | R | Q | M | R | X | U |

## En Python

```python
def cesar(texte: str, k: int) -> str:
    resultat = ""
    for c in texte.upper():
        if c.isalpha():
            resultat += chr((ord(c) - ord("A") + k) % 26 + ord("A"))
        else:
            resultat += c          # espaces et ponctuation inchangés
    return resultat

print(cesar("BONJOUR", 3))   # ERQMRXU
print(cesar("ERQMRXU", -3))  # BONJOUR  (déchiffrer = décaler de -k)
```

## Cas particulier : ROT13

`k = 13` → chiffrer deux fois redonne le message (13 + 13 = 26 ≡ 0). Chiffrer et déchiffrer sont donc la même opération.

## Pourquoi c'est faible

### 1. Force brute

Il n'y a que **25 clés utiles** (k = 1 à 25). On les essaie toutes et on lit celle qui donne du français.

```python
for k in range(1, 26):
    print(k, cesar("ERQMRXU", -k))
```

### 2. Analyse fréquentielle

Le chiffrement de César est une **substitution monoalphabétique** : une lettre du clair donne toujours la même lettre chiffrée. Les fréquences sont donc conservées.

En français, la lettre la plus fréquente est **E** (~15 %), puis A, S, I, N, T.

➡️ Si la lettre la plus fréquente du chiffré est `H`, alors probablement `E → H`, donc `k = 7 − 4 = 3`.

## ✅ À retenir

- `C = (M + k) mod 26` et `M = (C − k) mod 26`
- Seulement **25 clés** → cassable par force brute
- Une lettre donne toujours la même lettre → cassable par **analyse fréquentielle**
- ROT13 = César avec k = 13 (involution)

📝 [Exercices corrigés](exercices.md) · ➡️ Suite : [Vigenère](../vigenere/vigenere.md)
