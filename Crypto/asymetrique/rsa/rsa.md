# 🗝️ RSA

[🏠 Index](../../../index.md)

> **Niveau :** intermédiaire · **Prérequis :** [arithmétique modulaire](../../arithmetique_modulaire/arithmetique_modulaire.md) (inverse, exponentiation)

## Principe de l'asymétrique

Chaque personne a **deux clés** :

- une **clé publique** : tout le monde peut la connaître → sert à **chiffrer** (ou vérifier une signature)
- une **clé privée** : gardée secrète → sert à **déchiffrer** (ou signer)

💡 Image : un **cadenas ouvert** (clé publique) que tout le monde peut fermer, mais que seul le propriétaire de la clé (privée) peut ouvrir.

RSA (Rivest, Shamir, Adleman, 1977) repose sur le fait qu'il est **facile de multiplier** deux grands nombres premiers, mais **très difficile de factoriser** le résultat.

## Génération des clés

| Étape | Exemple |
|---|---|
| 1. Choisir deux nombres premiers `p` et `q` | p = 5, q = 11 |
| 2. Calculer `n = p × q` (le **module**) | n = 55 |
| 3. Calculer `φ(n) = (p − 1)(q − 1)` (indicatrice d'Euler) | φ = 4 × 10 = 40 |
| 4. Choisir `e` tel que `1 < e < φ(n)` et `pgcd(e, φ(n)) = 1` | e = 3 |
| 5. Calculer `d = e⁻¹ mod φ(n)` (**inverse modulaire**) | d = 27 car 3 × 27 = 81 = 2 × 40 + 1 |

- 🔓 **Clé publique : `(n, e)`** = (55, 3)
- 🔐 **Clé privée : `(n, d)`** = (55, 27) — et on garde aussi `p`, `q`, `φ(n)` secrets

## Chiffrer et déchiffrer

Le message est un nombre `m` avec `0 ≤ m < n`.

```
Chiffrement (clé publique)  : c = mᵉ mod n
Déchiffrement (clé privée)  : m = cᵈ mod n
```

**Exemple** avec m = 7 :

```
c = 7³ mod 55 = 343 mod 55 = 343 − 6 × 55 = 13
m = 13²⁷ mod 55 = 7   ✅  (calcul par carrés successifs)
```

## Signer

On inverse le rôle des clés :

```
Signature (clé privée)        : s = mᵈ mod n
Vérification (clé publique)   : on vérifie que sᵉ mod n = m
```

Seul le détenteur de `d` peut produire `s`, mais **tout le monde** peut vérifier avec `e`.
En pratique, on signe le **[hash](../../hachage/hachage.md)** du message, pas le message entier.

## Pourquoi c'est sûr (et quand ça ne l'est pas)

Pour trouver `d`, il faut `φ(n)`, donc `p` et `q`, donc **factoriser `n`**.

- Avec n = 55, c'est immédiat (5 × 11).
- Avec un `n` de **2048 bits** (~617 chiffres), aucun ordinateur actuel n'y arrive.

⚠️ Les erreurs classiques :

| Erreur | Conséquence |
|---|---|
| `n` trop petit | factorisation → clé privée retrouvée |
| `p` et `q` trop proches | factorisation facile (méthode de Fermat) |
| RSA « textbook » sans *padding* | même message → même chiffré, et d'autres attaques → on utilise **OAEP** |
| Révéler `φ(n)`, `p` ou `q` | clé privée retrouvée immédiatement |

## En Python

```python
p, q = 5, 11
n = p * q
phi = (p - 1) * (q - 1)
e = 3
d = pow(e, -1, phi)       # 27

m = 7
c = pow(m, e, n)          # 13
print(pow(c, d, n))       # 7
```

## ✅ À retenir

- `n = p × q`, `φ(n) = (p − 1)(q − 1)`, `pgcd(e, φ) = 1`, `d = e⁻¹ mod φ(n)`
- Publique `(n, e)` · Privée `(n, d)`
- Chiffrer : `c = mᵉ mod n` · Déchiffrer : `m = cᵈ mod n`
- Signer = utiliser la clé **privée** ; vérifier = clé **publique**
- Sécurité = difficulté de **factoriser n** (≥ 2048 bits aujourd'hui)

📝 [Exercices corrigés](exercices.md) · ➡️ Voir aussi : [Diffie-Hellman](../diffie_hellman/diffie_hellman.md)
