# 📝 Exercices — Diffie-Hellman

[🏠 Index](../../../index.md)

> **Cours :** [diffie_hellman.md](diffie_hellman.md) · Les corrigés sont dans les blocs repliables ▶

## Exercice 1 — Public ou secret ? 🟢

Classer en **public** ou **secret** : `p`, `g`, `a`, `b`, `A`, `B`, `s`.

<details>
<summary>Corrigé</summary>

- **Public** : `p`, `g`, `A`, `B`
- **Secret** : `a` (Alice seule), `b` (Bob seul), `s` (Alice et Bob)

</details>

## Exercice 2 — Échange complet 🟢

p = 11, g = 2. Alice choisit a = 3, Bob choisit b = 7. Calculer A, B et le secret commun (des deux côtés).

<details>
<summary>Corrigé</summary>

```
A = 2³ mod 11 = 8
B = 2⁷ mod 11 = 128 mod 11 = 128 − 11 × 11 = 7

Alice : s = 7³ mod 11 = 343 mod 11 = 343 − 31 × 11 = 2
Bob   : s = 8⁷ mod 11 = 2²¹ mod 11
        (Fermat : 2¹⁰ ≡ 1, donc 2²¹ = (2¹⁰)² × 2 ≡ 2)   ✅
```

→ **A = 8, B = 7, s = 2**

</details>

## Exercice 3 — Vérifier l'exemple du cours 🟡

p = 23, g = 5, a = 6. Calculer `A = 5⁶ mod 23` à la main.

<details>
<summary>Corrigé</summary>

```
5² = 25 ≡ 2
5⁴ ≡ 2² = 4
5⁶ = 5⁴ × 5² ≡ 4 × 2 = 8
```

→ **A = 8**

</details>

## Exercice 4 — Jouer l'espion 🟡

Vous écoutez un échange : p = 11, g = 2, A = 8, B = 7. Retrouver le secret commun.

<details>
<summary>Corrigé</summary>

On cherche `a` tel que `2ᵃ ≡ 8 (mod 11)` (logarithme discret) en testant :
2¹ = 2, 2² = 4, 2³ = 8 ✅ → **a = 3**

Puis `s = Bᵃ mod p = 7³ mod 11` = **2**.

➡️ Faisable ici car p est minuscule. Avec p de 2048 bits, il faudrait tester ~2²⁰⁴⁸ valeurs.

</details>

## Exercice 5 — Homme du milieu 🟡

1. Pourquoi Diffie-Hellman « seul » est-il vulnérable à l'homme du milieu ?
2. Un espion **passif** (qui ne fait qu'écouter) peut-il mener cette attaque ?
3. Comment s'en protéger ?

<details>
<summary>Corrigé</summary>

1. Rien ne prouve à Alice que `B` vient vraiment de Bob : il n'y a **pas d'authentification**. Mallory peut remplacer A et B par ses propres valeurs.
2. **Non** : il faut pouvoir **intercepter et modifier** les messages (attaquant actif).
3. **Authentifier** les échanges : signer A et B (signature RSA/ECDSA) avec des clés publiques garanties par des **certificats**.

</details>

## Exercice 6 — Programmation 🔴

Écrire une fonction `logarithme_discret(g, A, p)` qui retrouve `a` par force brute. La tester sur p = 23, g = 5, A = 8.

<details>
<summary>Corrigé</summary>

```python
def logarithme_discret(g, A, p):
    valeur = 1
    for a in range(p):
        if valeur == A:
            return a
        valeur = (valeur * g) % p
    return None

print(logarithme_discret(5, 8, 23))   # 6
```

Complexité : jusqu'à p essais → **exponentielle** en la taille de p (en bits).

</details>
