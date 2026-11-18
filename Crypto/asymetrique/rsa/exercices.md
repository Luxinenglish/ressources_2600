# 📝 Exercices — RSA

[🏠 Index](../../../index.md)

> **Cours :** [rsa.md](rsa.md) · Les corrigés sont dans les blocs repliables ▶

## Exercice 1 — Quelle clé ? 🟢

Alice veut envoyer un message confidentiel à Bob, puis signer un contrat. Quelle clé utilise-t-elle à chaque fois (publique/privée, de qui) ?

<details>
<summary>Corrigé</summary>

- Message confidentiel → elle chiffre avec la **clé publique de Bob** (seul Bob pourra déchiffrer avec sa clé privée).
- Signature → elle signe avec **sa propre clé privée** (tout le monde vérifie avec la clé publique d'Alice).

</details>

## Exercice 2 — Choix de e 🟢

Avec p = 5 et q = 11, peut-on choisir e = 4 ? e = 5 ? e = 7 ?

<details>
<summary>Corrigé</summary>

φ(n) = 4 × 10 = 40 = 2³ × 5. Il faut `pgcd(e, 40) = 1`.

- e = 4 → pgcd = 4 → **non**
- e = 5 → pgcd = 5 → **non**
- e = 7 → pgcd = 1 → **oui**

</details>

## Exercice 3 — Génération complète 🟡

Avec **p = 7, q = 13, e = 5** :

1. Calculer n et φ(n).
2. Vérifier que e est valide.
3. Calculer d (Euclide étendu).
4. Donner la clé publique et la clé privée.

<details>
<summary>Corrigé</summary>

1. n = 7 × 13 = **91** ; φ(n) = 6 × 12 = **72**
2. pgcd(5, 72) = 1 ✅
3. ```
   72 = 14 × 5 + 2
    5 = 2 × 2 + 1
   1 = 5 − 2 × 2 = 5 − 2 × (72 − 14 × 5) = 29 × 5 − 2 × 72
   ```
   → **d = 29** (vérif : 5 × 29 = 145 = 2 × 72 + 1 ✅)
4. Publique **(91, 5)** · Privée **(91, 29)**

</details>

## Exercice 4 — Chiffrer 🟡

Avec la clé publique (91, 5), chiffrer m = 10.

<details>
<summary>Corrigé</summary>

```
10² = 100 ≡ 9   (mod 91)
10⁴ ≡ 9² = 81
10⁵ = 10⁴ × 10 ≡ 81 × 10 = 810 = 8 × 91 + 82 ≡ 82
```

→ **c = 82**

Vérification en Python : `pow(82, 29, 91)` → `10` ✅

</details>

## Exercice 5 — Petit exemple complet 🟡

p = 5, q = 11, e = 3, d = 27. Chiffrer m = 2, puis vérifier le déchiffrement en Python.

<details>
<summary>Corrigé</summary>

c = 2³ mod 55 = **8**

```python
print(pow(8, 27, 55))   # 2 ✅
```

</details>

## Exercice 6 — Casser une clé trop petite 🔴

Vous interceptez le chiffré **c = 82** envoyé avec la clé publique **(n = 91, e = 5)**. Retrouver le message.

<details>
<summary>Corrigé</summary>

1. **Factoriser n** : 91 = **7 × 13** (on teste les petits premiers : 2, 3, 5, 7 ✅)
2. φ(n) = 6 × 12 = 72
3. d = 5⁻¹ mod 72 = **29**
4. m = 82²⁹ mod 91 = **10**

➡️ Toute la sécurité de RSA repose sur la difficulté de l'étape 1 : avec un n de 2048 bits, elle est impossible.

</details>

## Exercice 7 — Signature 🔴

Avec la clé (n = 55, e = 3, d = 27), signer le message m = 4, puis vérifier la signature.

<details>
<summary>Corrigé</summary>

- Signature : s = 4²⁷ mod 55. Par carrés : 4² = 16, 4⁴ = 256 ≡ 36, 4⁸ ≡ 36² = 1296 ≡ 31, 4¹⁶ ≡ 31² = 961 ≡ 26.
  27 = 16 + 8 + 2 + 1 → s ≡ 26 × 31 × 16 × 4 (mod 55). 26 × 31 = 806 ≡ 36 ; 36 × 16 = 576 ≡ 26 ; 26 × 4 = 104 ≡ **49**.
- Vérification : 49³ mod 55. 49² = 2401 ≡ 36 ; 36 × 49 = 1764 ≡ **4** = m ✅

</details>
