# 📝 Exercices — Bases du réseau

> **Cours :** [reseau_bases.md](reseau_bases.md) · Les corrigés sont dans les blocs repliables ▶

## Exercice 1 — Couches OSI 🟢

Associer chaque élément à sa couche OSI (numéro + nom) : `HTTP`, `IP`, `TCP`, `adresse MAC`, `câble RJ45`, `UDP`, `DNS`.

<details>
<summary>Corrigé</summary>

| Élément | Couche |
|---|---|
| câble RJ45 | 1 — Physique |
| adresse MAC | 2 — Liaison |
| IP | 3 — Réseau |
| TCP, UDP | 4 — Transport |
| HTTP, DNS | 7 — Application |

</details>

## Exercice 2 — Adressage /24 🟢

Pour `192.168.10.37/24`, donner : le masque, l'adresse réseau, l'adresse de broadcast, la première et la dernière adresse utilisable, le nombre d'hôtes.

<details>
<summary>Corrigé</summary>

| | |
|---|---|
| Masque | `255.255.255.0` |
| Réseau | `192.168.10.0` |
| Broadcast | `192.168.10.255` |
| 1ʳᵉ adresse | `192.168.10.1` |
| Dernière adresse | `192.168.10.254` |
| Nombre d'hôtes | 2⁸ − 2 = **254** |

</details>

## Exercice 3 — Adressage /26 🟡

Même question pour `172.16.5.130/26`.

<details>
<summary>Corrigé</summary>

- /26 → 26 bits à 1 → dernier octet `1100 0000` = 192 → masque **`255.255.255.192`**
- Il reste 6 bits pour les hôtes → blocs de 2⁶ = **64** adresses : `.0`, `.64`, `.128`, `.192`
- 130 est dans le bloc **128 → 191**

| | |
|---|---|
| Réseau | `172.16.5.128` |
| Broadcast | `172.16.5.191` |
| 1ʳᵉ adresse | `172.16.5.129` |
| Dernière adresse | `172.16.5.190` |
| Nombre d'hôtes | 64 − 2 = **62** |

Vérification par le calcul : `130 AND 192` → `1000 0010 AND 1100 0000 = 1000 0000` = **128** ✅

</details>

## Exercice 4 — Nombre d'hôtes 🟢

Combien d'hôtes utilisables dans un réseau `/27` ? `/28` ? `/30` ?

<details>
<summary>Corrigé</summary>

Formule : **2^(32 − CIDR) − 2** (on retire l'adresse réseau et le broadcast)

- /27 → 2⁵ − 2 = **30**
- /28 → 2⁴ − 2 = **14**
- /30 → 2² − 2 = **2** (utilisé pour relier deux routeurs)

</details>

## Exercice 5 — Découpage 🟡

Découper `192.168.1.0/24` en **4 sous-réseaux** de même taille. Donner le CIDR et l'adresse de chaque sous-réseau.

<details>
<summary>Corrigé</summary>

4 sous-réseaux = 2² → on emprunte **2 bits** → /24 + 2 = **/26** (64 adresses chacun)

| Sous-réseau | Réseau | Broadcast |
|:-:|---|---|
| 1 | `192.168.1.0/26` | `192.168.1.63` |
| 2 | `192.168.1.64/26` | `192.168.1.127` |
| 3 | `192.168.1.128/26` | `192.168.1.191` |
| 4 | `192.168.1.192/26` | `192.168.1.255` |

</details>

## Exercice 6 — Privée ou publique ? 🟢

`10.12.0.5` · `8.8.8.8` · `172.20.1.1` · `172.32.0.1` · `192.168.0.254`

<details>
<summary>Corrigé</summary>

| Adresse | Réponse |
|---|---|
| `10.12.0.5` | privée (10.0.0.0/8) |
| `8.8.8.8` | **publique** |
| `172.20.1.1` | privée (172.16.0.0/12 = 172.16 → 172.31) |
| `172.32.0.1` | **publique** ⚠️ piège : 32 > 31 |
| `192.168.0.254` | privée (192.168.0.0/16) |

</details>

## Exercice 7 — Même réseau ? 🟡

Ces deux machines peuvent-elles communiquer directement (sans routeur) ?

1. `192.168.1.10/24` et `192.168.2.10/24`
2. `10.0.0.5/8` et `10.200.3.4/8`

<details>
<summary>Corrigé</summary>

1. **Non** : réseaux `192.168.1.0` et `192.168.2.0` → différents, il faut un routeur.
2. **Oui** : avec /8, seul le 1er octet compte → les deux sont dans `10.0.0.0`.

</details>

## Exercice 8 — TCP ou UDP ? 🟢

Pour chaque usage, choisir TCP ou UDP et justifier : téléchargement d'un fichier, requête DNS, appel vidéo, page web.

<details>
<summary>Corrigé</summary>

| Usage | Protocole | Pourquoi |
|---|---|---|
| Téléchargement | **TCP** | il ne faut perdre aucun octet |
| Requête DNS | **UDP** | petite question/réponse, rapide (TCP possible pour les grosses réponses) |
| Appel vidéo | **UDP** | mieux vaut perdre une image que prendre du retard |
| Page web | **TCP** | HTTP a besoin d'une transmission fiable |

</details>
