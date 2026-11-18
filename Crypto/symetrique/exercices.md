# 📝 Exercices — Chiffrement symétrique

[🏠 Index](../../index.md)

> **Cours :** [chiffrement_symetrique.md](chiffrement_symetrique.md) · Les corrigés sont dans les blocs repliables ▶

## Exercice 1 — Questions de cours 🟢

1. Quelle est la taille de bloc d'AES ? Quelles tailles de clé sont possibles ?
2. Pourquoi DES n'est-il plus utilisé ?
3. Citer un chiffrement par flot et un chiffrement par blocs.

<details>
<summary>Corrigé</summary>

1. Blocs de **128 bits** ; clés de **128, 192 ou 256 bits**.
2. Sa clé ne fait que **56 bits** : 2⁵⁶ clés, testables par force brute en quelques heures.
3. Flot : **ChaCha20** (ou RC4, cassé). Blocs : **AES** (ou DES).

</details>

## Exercice 2 — Nombre de clés 🟢

Une classe de 30 étudiants veut que chaque paire puisse communiquer secrètement en symétrique. Combien de clés faut-il ?

<details>
<summary>Corrigé</summary>

`n(n − 1)/2 = 30 × 29 / 2` = **435 clés**.

(En asymétrique, il suffirait d'**une paire de clés par personne**, soit 30 paires.)

</details>

## Exercice 3 — Force brute 🟡

Un ordinateur teste 10⁹ clés par seconde.

1. Combien de temps (au pire) pour une clé de 40 bits ?
2. Combien de fois plus de temps pour 41 bits ? pour 50 bits ?

<details>
<summary>Corrigé</summary>

1. 2⁴⁰ ≈ 1,1 × 10¹² clés → 1,1 × 10¹² / 10⁹ ≈ **1 100 secondes ≈ 18 minutes**
2. 41 bits → **2 fois** plus (≈ 37 min). 50 bits → 2¹⁰ = **1 024 fois** plus (≈ 13 jours).

</details>

## Exercice 4 — ECB 🟡

Un message de 4 blocs `M₁ M₂ M₁ M₃` (le 1ᵉʳ et le 3ᵉ blocs sont identiques) est chiffré en ECB.

1. Que remarque un attaquant dans le chiffré ?
2. Et en CBC ?

<details>
<summary>Corrigé</summary>

1. En ECB, `C₁ = E(K, M₁)` et `C₃ = E(K, M₁)` → **C₁ = C₃**. L'attaquant voit que le 1ᵉʳ et le 3ᵉ blocs sont identiques, sans connaître la clé : la **structure** du message fuit.
2. En CBC, `C₁ = E(K, M₁ ⊕ IV)` et `C₃ = E(K, M₁ ⊕ C₂)`. Comme `IV ≠ C₂`, on a **C₁ ≠ C₃** : la répétition est masquée.

</details>

## Exercice 5 — CBC à la main 🔴

On utilise un « chiffrement par blocs » jouet sur 4 bits : `E(K, X) = X ⊕ K` avec `K = 1010`, et `IV = 0110`.
Chiffrer en CBC le message de deux blocs `M₁ = 1100`, `M₂ = 1100`.

<details>
<summary>Corrigé</summary>

```
C₁ = E(K, M₁ ⊕ IV) = (1100 ⊕ 0110) ⊕ 1010 = 1010 ⊕ 1010 = 0000
C₂ = E(K, M₂ ⊕ C₁) = (1100 ⊕ 0000) ⊕ 1010 = 1100 ⊕ 1010 = 0110
```

→ **C₁ = 0000, C₂ = 0110** : deux blocs clairs identiques, deux blocs chiffrés différents ✅

(Évidemment, un vrai chiffrement par blocs n'est pas un simple XOR, sinon il serait trivial à casser.)

</details>

## Exercice 6 — Le nonce 🔴

En AES-GCM (ou CTR), pourquoi ne faut-il **jamais** réutiliser le même nonce avec la même clé ? (Indice : [exercice 6 du XOR](../logic_gate/XOR/exercices.md))

<details>
<summary>Corrigé</summary>

CTR/GCM produit un flot de clé `F` qui dépend de (clé, nonce), puis `C = M ⊕ F`.
Même clé + même nonce → **même flot F** pour deux messages :
`C₁ ⊕ C₂ = M₁ ⊕ F ⊕ M₂ ⊕ F = M₁ ⊕ M₂` → le flot disparaît, comme une clé XOR réutilisée. Si on connaît M₁, on retrouve M₂.

</details>
