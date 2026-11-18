# 📝 Exercices — Introduction à la cryptographie

> **Cours :** [notions_de_base.md](notions_de_base.md) · Les corrigés sont dans les blocs repliables ▶

## Exercice 1 — Vocabulaire 🟢

Compléter avec : *chiffrer*, *déchiffrer*, *décrypter*.

1. Alice utilise la clé pour ______ son message avant de l'envoyer.
2. Bob, qui possède la clé, ______ le message reçu.
3. Eve n'a pas la clé, mais elle réussit à ______ le message en analysant les fréquences des lettres.

<details>
<summary>Corrigé</summary>

1. **chiffrer**
2. **déchiffre**
3. **décrypter**

</details>

## Exercice 2 — Kerckhoffs 🟢

Une entreprise affirme : « Notre algorithme est ultra-sûr car personne ne sait comment il fonctionne. » Qu'en pensez-vous ?

<details>
<summary>Corrigé</summary>

C'est contraire au **principe de Kerckhoffs** : c'est de la « sécurité par l'obscurité ». Un algorithme finit toujours par être découvert (rétro-ingénierie, fuite…). Un bon système reste sûr **même si l'algorithme est connu** : seule la clé doit être secrète. Les algorithmes publics (AES, RSA) ont en plus été analysés par des milliers de chercheurs.

</details>

## Exercice 3 — Objectifs de sécurité 🟢

Pour chaque situation, donner l'objectif de sécurité concerné :

1. Un fichier téléchargé doit être identique à l'original.
2. Personne ne doit pouvoir lire un e-mail sauf son destinataire.
3. Un client ne doit pas pouvoir nier avoir signé un contrat en ligne.
4. Un serveur veut être sûr que la requête vient bien de son client.

<details>
<summary>Corrigé</summary>

1. **Intégrité** (hachage)
2. **Confidentialité** (chiffrement)
3. **Non-répudiation** (signature numérique)
4. **Authentification** (MAC ou signature)

</details>

## Exercice 4 — Symétrique ou asymétrique ? 🟡

1. Quel est le principal problème du chiffrement symétrique ?
2. Pourquoi ne chiffre-t-on pas tout en asymétrique ?
3. Comment HTTPS combine-t-il les deux ?

<details>
<summary>Corrigé</summary>

1. **L'échange de la clé** : les deux parties doivent partager la même clé secrète, sans qu'un tiers l'intercepte.
2. L'asymétrique est **beaucoup plus lent** (des centaines à des milliers de fois).
3. L'asymétrique (RSA, Diffie-Hellman) sert à **établir une clé de session**, puis toutes les données sont chiffrées en **symétrique** (AES) avec cette clé.

</details>

## Exercice 5 — Type d'attaque 🟡

Identifier le type d'attaque :

1. Eve a intercepté 50 messages chiffrés et rien d'autre.
2. Eve sait que chaque message commence par « Bonjour ».
3. Eve teste les 26 décalages possibles d'un chiffrement de César.

<details>
<summary>Corrigé</summary>

1. **Chiffré seul**
2. **Clair connu** (elle connaît une partie du clair correspondant à chaque chiffré)
3. **Force brute**

</details>
