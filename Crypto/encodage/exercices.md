# 📝 Exercices — Bases & encodages

[🏠 Index](../../index.md)

> **Cours :** [bases_encodage.md](bases_encodage.md) · Les corrigés sont dans les blocs repliables ▶

## Exercice 1 — Vers le décimal 🟢

Convertir en décimal, **à la main** :

1. `0b1011`
2. `0b11111111`
3. `0x2F`
4. `0xFF`

<details>
<summary>Corrigé</summary>

1. `1011` = 8 + 0 + 2 + 1 = **11**
2. `11111111` = 128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 = **255**
3. `0x2F` = 2 × 16 + 15 = **47**
4. `0xFF` = 15 × 16 + 15 = **255**

</details>

## Exercice 2 — Depuis le décimal 🟢

Convertir en binaire **et** en hexadécimal :

1. `42`
2. `200`

<details>
<summary>Corrigé</summary>

Méthode : divisions successives par 2 (ou par 16), on lit les restes de bas en haut.

1. `42` → **`0b101010`** → **`0x2A`**
   (42 = 32 + 8 + 2 ; et 42 = 2 × 16 + 10 → `2A`)
2. `200` → **`0b11001000`** → **`0xC8`**
   (200 = 128 + 64 + 8 ; et 200 = 12 × 16 + 8 → `C8`)

Astuce : binaire → hexa, on découpe par paquets de 4 bits : `1100 1000` → `C 8`.

</details>

## Exercice 3 — Combien de valeurs ? 🟢

Combien de valeurs différentes peut-on représenter avec :

1. 4 bits ?
2. 8 bits ?
3. 16 bits ?

<details>
<summary>Corrigé</summary>

Avec *n* bits : **2ⁿ** valeurs (de 0 à 2ⁿ − 1).

1. 2⁴ = **16** (0 à 15, soit un chiffre hexa)
2. 2⁸ = **256** (0 à 255, un octet)
3. 2¹⁶ = **65 536**

</details>

## Exercice 4 — ASCII 🟢

1. Décoder la suite hexadécimale : `42 4F 4E 4A 4F 55 52`
2. Donner le code hexa de `a`, sachant que `A` = `0x41`.

<details>
<summary>Corrigé</summary>

1. `42`=B, `4F`=O, `4E`=N, `4A`=J, `4F`=O, `55`=U, `52`=R → **`BONJOUR`**
2. Minuscule = majuscule + 32 = `0x41 + 0x20` = **`0x61`**

</details>

## Exercice 5 — Base64 🟡

1. Encoder `Hi` en Base64 **à la main**.
2. Décoder `Q291cnM=` (avec Python ou la commande `base64`).

<details>
<summary>Corrigé</summary>

1. `H` = `0x48` = `01001000`, `i` = `0x69` = `01101001`
   On découpe en paquets de **6 bits** : `010010` `000110` `1001`**`00`** (on complète avec des 0)
   → 18, 6, 36 → `S`, `G`, `k` dans la table Base64 (A=0…Z=25, a=26…z=51)
   → 3 caractères au lieu de 4 → on ajoute un `=` → **`SGk=`**
2. **`Cours`**

```bash
echo "Q291cnM=" | base64 -d
```

</details>

## Exercice 6 — Question de cours 🟢

Quelle est la différence entre un **encodage** et un **chiffrement** ? Base64 protège-t-il un mot de passe ?

<details>
<summary>Corrigé</summary>

- Un **encodage** change la représentation des données **sans clé** : tout le monde peut le décoder.
- Un **chiffrement** utilise une **clé** : sans elle, on ne peut pas retrouver le message.

➡️ Base64 **ne protège rien** : n'importe qui peut décoder un mot de passe encodé en Base64.

</details>
