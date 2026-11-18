# 🔑 Chiffrement de Vigenère

[🏠 Index](../../../index.md)

> **Niveau :** débutant → intermédiaire · **Prérequis :** [César](../cesar/cesar.md)

## Principe

Vigenère = **plusieurs César** à la suite. La clé est un **mot** ; chaque lettre de la clé donne le décalage d'une lettre du message (A = 0, B = 1, …). La clé est répétée sur toute la longueur du message.

```
Clair : A T T A Q U E   D E M A I N
Clé   : C L E C L E C   L E C L E C
        ↓ (on additionne, mod 26)
Chiffré: C E X C B Y G   O I O L M P
```

(Les espaces ne consomment pas de lettre de clé.)

## Formules

Avec `Kᵢ` la lettre de clé utilisée pour la i-ème lettre :

```
Chiffrement   : Cᵢ = (Mᵢ + Kᵢ) mod 26
Déchiffrement : Mᵢ = (Cᵢ − Kᵢ) mod 26
```

### Exemple à la main : `BONJOUR` avec la clé `KEY`

| Clair | B (1) | O (14) | N (13) | J (9) | O (14) | U (20) | R (17) |
|---|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| Clé | K (10) | E (4) | Y (24) | K (10) | E (4) | Y (24) | K (10) |
| Somme mod 26 | 11 | 18 | 11 | 19 | 18 | 18 | 1 |
| Chiffré | **L** | **S** | **L** | **T** | **S** | **S** | **B** |

👉 Les deux `O` donnent `S` ici car ils tombent tous les deux sur la lettre de clé `E`. Mais à l'inverse, `B` et `N` donnent tous les deux `L` : **une même lettre chiffrée peut venir de lettres claires différentes**, et une même lettre claire peut donner des lettres chiffrées différentes (voir l'exercice 4).

## En Python

```python
def vigenere(texte: str, cle: str, sens: int = 1) -> str:
    """sens = 1 pour chiffrer, -1 pour déchiffrer."""
    resultat, i = "", 0
    for c in texte.upper():
        if c.isalpha():
            k = ord(cle[i % len(cle)].upper()) - ord("A")
            resultat += chr((ord(c) - ord("A") + sens * k) % 26 + ord("A"))
            i += 1
        else:
            resultat += c
    return resultat

print(vigenere("ATTAQUE DEMAIN", "CLE"))       # CEXCBYG OIOLMP
print(vigenere("CEXCBYG OIOLMP", "CLE", -1))   # ATTAQUE DEMAIN
```

## Pourquoi c'est mieux que César

C'est un chiffrement **polyalphabétique** : une même lettre du clair peut donner des lettres chiffrées différentes selon sa position.
➡️ L'analyse fréquentielle **directe** ne marche plus : les fréquences sont « lissées ».

Pour une clé de longueur `L`, il y a **26ᴸ** clés possibles (clé de 10 lettres : ~1,4 × 10¹⁴).

## Comment on le casse quand même

1. **Trouver la longueur `L` de la clé**
   - *Test de Kasiski* : on cherche des séquences répétées dans le chiffré. La distance entre deux répétitions est souvent un **multiple de L**.
   - *Indice de coïncidence* : on teste plusieurs L ; le bon donne un indice proche de celui du français (~0,078).
2. **Découper** le chiffré en `L` colonnes (lettres 1, L+1, 2L+1… ; lettres 2, L+2…).
3. Chaque colonne est un simple **César** → **analyse fréquentielle** colonne par colonne.

## Cas limite : le masque jetable

Si la clé est **aléatoire**, **aussi longue que le message** et **jamais réutilisée**, Vigenère devient le **One-Time Pad** (masque jetable) : incassable, même en théorie. (C'est la même idée que le [XOR](../../logic_gate/XOR/simple_xor.md) avec une clé aléatoire.)

## ✅ À retenir

- `Cᵢ = (Mᵢ + Kᵢ) mod 26`, la clé est répétée
- **Polyalphabétique** : résiste à l'analyse fréquentielle simple
- Cassable : trouver la longueur de clé (Kasiski) → L César à casser
- Clé aléatoire aussi longue que le message, jamais réutilisée = masque jetable

📝 [Exercices corrigés](exercices.md)
