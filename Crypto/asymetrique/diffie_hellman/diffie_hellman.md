# 🤝 Échange de clés Diffie-Hellman

> **Niveau :** intermédiaire · **Prérequis :** [arithmétique modulaire](../../arithmetique_modulaire/arithmetique_modulaire.md) (exponentiation)

## Le problème

Alice et Bob veulent utiliser un [chiffrement symétrique](../../symetrique/chiffrement_symetrique.md) (AES), mais ils doivent d'abord se mettre d'accord sur une **clé secrète commune**… en communiquant sur un canal **que tout le monde écoute**.

Diffie-Hellman (1976) permet de le faire **sans jamais envoyer la clé**.

## Le protocole

| | Alice | Canal public 👀 | Bob |
|---|---|---|---|
| 1 | | se mettent d'accord sur `p` (premier) et `g` (générateur) | |
| 2 | choisit un secret `a` | | choisit un secret `b` |
| 3 | calcule `A = gᵃ mod p` | ── `A` ──► / ◄── `B` ── | calcule `B = gᵇ mod p` |
| 4 | calcule `s = Bᵃ mod p` | | calcule `s = Aᵇ mod p` |

Les deux obtiennent **le même secret** :

```
Bᵃ = (gᵇ)ᵃ = gᵃᵇ = (gᵃ)ᵇ = Aᵇ   (mod p)
```

## Exemple

p = 23, g = 5, Alice choisit a = 6, Bob choisit b = 15.

```
A = 5⁶  mod 23 = 8
B = 5¹⁵ mod 23 = 19

Alice : s = 19⁶ mod 23 = 2
Bob   : s = 8¹⁵ mod 23 = 2     ✅ secret commun : 2
```

L'espion voit **p = 23, g = 5, A = 8, B = 19**, mais pas `a` ni `b`.

## Pourquoi c'est sûr

Pour trouver le secret, l'espion doit retrouver `a` à partir de `A = gᵃ mod p` : c'est le **problème du logarithme discret**.

- Avec p = 23, on teste tous les `a` à la main.
- Avec un `p` de **2048 bits**, c'est impossible en pratique.

## La faiblesse : l'homme du milieu (MITM)

Diffie-Hellman seul **n'authentifie pas** les participants. Si Mallory peut **modifier** les messages (pas seulement écouter) :

```
Alice ──A──► Mallory ──M──► Bob
Alice ◄──M── Mallory ◄──B── Bob
```

- Alice partage un secret avec Mallory (en croyant parler à Bob)
- Bob partage un autre secret avec Mallory (en croyant parler à Alice)
- Mallory déchiffre, lit, re-chiffre tout 😈

➡️ Solution : **authentifier** les valeurs échangées, par exemple avec des **signatures** ([RSA](../rsa/rsa.md)) et des **certificats** (c'est ce que fait TLS/HTTPS).

## En Python

```python
p, g = 23, 5
a, b = 6, 15                 # secrets (en vrai : aléatoires et très grands)

A = pow(g, a, p)             # 8  envoyé à Bob
B = pow(g, b, p)             # 19 envoyé à Alice

print(pow(B, a, p), pow(A, b, p))   # 2 2
```

## ✅ À retenir

- Public : `p`, `g`, `A = gᵃ mod p`, `B = gᵇ mod p` · Secret : `a`, `b`
- Secret partagé : `s = gᵃᵇ mod p = Bᵃ = Aᵇ`
- Sécurité : **logarithme discret**
- Sans authentification → vulnérable à l'**homme du milieu**
- Sert à **établir une clé**, pas à chiffrer des messages

📝 [Exercices corrigés](exercices.md)
