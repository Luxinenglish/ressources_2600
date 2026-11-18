# 📝 Exercices — Chiffrement de César

> **Cours :** [cesar.md](cesar.md) · Les corrigés sont dans les blocs repliables ▶

## Exercice 1 — Chiffrer 🟢

Chiffrer `BONJOUR` avec `k = 3`, à la main.

<details>
<summary>Corrigé</summary>

B→E, O→R, N→Q, J→M, O→R, U→X, R→U → **`ERQMRXU`**

</details>

## Exercice 2 — Déchiffrer 🟢

Déchiffrer `KHOOR` sachant que `k = 3`.

<details>
<summary>Corrigé</summary>

On recule de 3 : K→H, H→E, O→L, O→L, R→O → **`HELLO`**

</details>

## Exercice 3 — Le modulo 🟢

Avec `k = 5`, que deviennent les lettres `W`, `Y` et `Z` ? Justifier avec la formule.

<details>
<summary>Corrigé</summary>

- W = 22 → (22 + 5) mod 26 = 27 mod 26 = **1 → B**
- Y = 24 → 29 mod 26 = **3 → D**
- Z = 25 → 30 mod 26 = **4 → E**

</details>

## Exercice 4 — ROT13 🟢

1. Chiffrer `RENDEZ VOUS A MIDI` en ROT13.
2. Que se passe-t-il si on applique ROT13 au résultat ? Pourquoi ?

<details>
<summary>Corrigé</summary>

1. **`ERAQRM IBHF N ZVQV`**
2. On retrouve le message d'origine, car 13 + 13 = 26 ≡ 0 (mod 26) : deux décalages de 13 font un tour complet.

</details>

## Exercice 5 — Force brute 🟡

Le message suivant a été chiffré avec César, clé inconnue. Le retrouver.

```
VO ZKBDSOV OCD VEXNS
```

<details>
<summary>Corrigé</summary>

Indice : un mot de 2 lettres en français → LE, LA, DE, UN, ET… Si `VO = LE`, alors V(21) → L(11) : k = 21 − 11 = **10**.
On vérifie avec `O → E` : 14 − 10 = 4 = E ✅

Message : **`LE PARTIEL EST LUNDI`**

```python
for k in range(1, 26):
    print(k, cesar("VO ZKBDSOV OCD VEXNS", -k))
```

</details>

## Exercice 6 — Analyse fréquentielle 🟡

Dans un long texte chiffré avec César, la lettre la plus fréquente est `X`. Quelle est probablement la clé ?

<details>
<summary>Corrigé</summary>

En français la lettre la plus fréquente est **E (4)**. On suppose donc `E → X (23)`.
k = 23 − 4 = **19**.

</details>

## Exercice 7 — Nombre de clés 🟡

1. Combien y a-t-il de clés possibles pour César ? Combien sont utiles ?
2. Une **substitution quelconque** (chaque lettre remplacée par n'importe quelle autre, sans répétition) a combien de clés ? Est-elle cassable par force brute ? Et par analyse fréquentielle ?

<details>
<summary>Corrigé</summary>

1. 26 clés (0 à 25), dont **25 utiles** (k = 0 ne chiffre rien).
2. **26! ≈ 4 × 10²⁶** clés → force brute impossible en pratique. Mais c'est toujours **monoalphabétique** (une lettre → toujours la même) donc l'**analyse fréquentielle** la casse quand même. Un grand nombre de clés ne suffit pas à rendre un chiffrement sûr.

</details>
