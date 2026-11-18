# 📝 Exercices — Chiffrement de Vigenère

[🏠 Index](../../../index.md)

> **Cours :** [vigenere.md](vigenere.md) · Les corrigés sont dans les blocs repliables ▶

## Exercice 1 — Chiffrer 🟢

Chiffrer `SECRET` avec la clé `ABC`.

<details>
<summary>Corrigé</summary>

| Clair | S (18) | E (4) | C (2) | R (17) | E (4) | T (19) |
|---|:-:|:-:|:-:|:-:|:-:|:-:|
| Clé | A (0) | B (1) | C (2) | A (0) | B (1) | C (2) |
| Chiffré | S | F | E | R | F | V |

→ **`SFERFV`**

</details>

## Exercice 2 — Déchiffrer 🟢

Déchiffrer `LSLTSSB` avec la clé `KEY`.

<details>
<summary>Corrigé</summary>

On **soustrait** la clé : L(11)−K(10)=1→B, S(18)−E(4)=14→O, L(11)−Y(24)=−13 mod 26=13→N, T(19)−K(10)=9→J, S−E→O, S(18)−Y(24)=−6 mod 26=20→U, B(1)−K(10)=−9 mod 26=17→R

→ **`BONJOUR`**

</details>

## Exercice 3 — Clé d'une lettre 🟢

Que devient Vigenère si la clé ne fait qu'**une lettre** ? Et si la clé est `A` ?

<details>
<summary>Corrigé</summary>

- Clé d'une lettre → le décalage est le même partout : c'est un **chiffrement de César**.
- Clé `A` → décalage de 0 : le message **n'est pas chiffré**.

</details>

## Exercice 4 — Mono ou poly ? 🟡

1. Dans l'exemple du cours (`ATTAQUE DEMAIN` / clé `CLE` → `CEXCBYG OIOLMP`), relever deux lettres identiques du clair chiffrées différemment.
2. Pourquoi est-ce important ?

<details>
<summary>Corrigé</summary>

1. Les `T` (positions 2 et 3) donnent `E` puis `X`. Les `A` donnent `C`, `C` puis `L`.
2. Une même lettre ne donne pas toujours la même lettre chiffrée → les fréquences du français sont **cachées** : l'analyse fréquentielle directe ne fonctionne plus (contrairement à César).

</details>

## Exercice 5 — Kasiski 🟡

Dans un chiffré, la séquence `XKV` apparaît aux positions 4, 28 et 52. Quelles longueurs de clé sont plausibles ?

<details>
<summary>Corrigé</summary>

Distances : 28 − 4 = **24** et 52 − 28 = **24**.
La longueur de clé divise probablement 24 : **2, 3, 4, 6, 8, 12 ou 24**. On teste ensuite ces valeurs (en commençant par les plus probables, ex : 4, 6, 8) avec l'analyse fréquentielle par colonnes.

</details>

## Exercice 6 — Nombre de clés 🟡

Combien de clés possibles pour une clé de 5 lettres ? Comparer avec César.

<details>
<summary>Corrigé</summary>

26⁵ = **11 881 376** clés (contre 26 pour César). Force brute faisable pour un ordinateur, mais la vraie attaque reste Kasiski + fréquences.

</details>

## Exercice 7 — Programmation 🔴

Modifier la fonction `vigenere` du cours pour qu'elle conserve les **minuscules** (au lieu de tout passer en majuscules).

<details>
<summary>Corrigé</summary>

```python
def vigenere(texte, cle, sens=1):
    resultat, i = "", 0
    for c in texte:
        if c.isalpha():
            base = ord("A") if c.isupper() else ord("a")
            k = ord(cle[i % len(cle)].upper()) - ord("A")
            resultat += chr((ord(c) - base + sens * k) % 26 + base)
            i += 1
        else:
            resultat += c
    return resultat

print(vigenere("Bonjour", "KEY"))   # Lsltssb
```

</details>
