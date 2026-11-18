# 🗂️ Index

> Toutes les fiches du dépôt sur une seule page. 📘 = cours · 📝 = exercices corrigés
> Chaque fiche a un lien **🏠 Index** en haut pour revenir ici.

**Aller à :** [🔐 Crypto](#-crypto) · [🐍 Python](#-python) · [🖧 ASR](#-asr--systèmes--réseaux) · [🔎 Par mot-clé](#-par-mot-clé) · [📖 README](README.md)

---

## 🔐 Crypto

[Vue d'ensemble, ordre conseillé et formules à connaître](Crypto/README.md)

### Les bases

| # | Notion | 📘 Cours | 📝 Exercices | Mots-clés |
|:-:|---|---|---|---|
| 1 | Introduction | [notions_de_base](Crypto/introduction/notions_de_base.md) | [exercices](Crypto/introduction/exercices.md) | vocabulaire, Kerckhoffs, confidentialité, intégrité, types d'attaques |
| 2 | Encodages | [bases_encodage](Crypto/encodage/bases_encodage.md) | [exercices](Crypto/encodage/exercices.md) | binaire, hexa, ASCII, Base64 |
| 3 | Portes logiques | [README](Crypto/logic_gate/README.md) | [exercices](Crypto/logic_gate/exercices.md) | AND, OR, NOT, NAND, NOR, opérateurs bit à bit |
| 4 | XOR | [simple_xor](Crypto/logic_gate/XOR/simple_xor.md) | [exercices](Crypto/logic_gate/XOR/exercices.md) | propriétés, clé répétée, clair connu, One-Time Pad |
| 5 | Arithmétique modulaire | [arithmetique_modulaire](Crypto/arithmetique_modulaire/arithmetique_modulaire.md) | [exercices](Crypto/arithmetique_modulaire/exercices.md) | modulo, PGCD, Euclide étendu, inverse, Fermat |

### Chiffrements classiques

| # | Notion | 📘 Cours | 📝 Exercices | Mots-clés |
|:-:|---|---|---|---|
| 6 | César | [cesar](Crypto/classique/cesar/cesar.md) | [exercices](Crypto/classique/cesar/exercices.md) | décalage, ROT13, force brute, analyse fréquentielle |
| 7 | Vigenère | [vigenere](Crypto/classique/vigenere/vigenere.md) | [exercices](Crypto/classique/vigenere/exercices.md) | polyalphabétique, Kasiski, masque jetable |

### Cryptographie moderne

| # | Notion | 📘 Cours | 📝 Exercices | Mots-clés |
|:-:|---|---|---|---|
| 8 | Symétrique | [chiffrement_symetrique](Crypto/symetrique/chiffrement_symetrique.md) | [exercices](Crypto/symetrique/exercices.md) | AES, DES, ECB, CBC, GCM, IV |
| 9 | Hachage | [hachage](Crypto/hachage/hachage.md) | [exercices](Crypto/hachage/exercices.md) | SHA-256, MD5, collisions, sel, bcrypt |
| 10 | RSA | [rsa](Crypto/asymetrique/rsa/rsa.md) | [exercices](Crypto/asymetrique/rsa/exercices.md) | clé publique/privée, φ(n), signature, factorisation |
| 11 | Diffie-Hellman | [diffie_hellman](Crypto/asymetrique/diffie_hellman/diffie_hellman.md) | [exercices](Crypto/asymetrique/diffie_hellman/exercices.md) | échange de clés, logarithme discret, homme du milieu |

---

## 🐍 Python

[Vue d'ensemble et installation](python/README.md)

| # | Notion | 📘 Cours | 📝 Exercices | Mots-clés |
|:-:|---|---|---|---|
| 1 | Les bases | [bases_python](python/bases/bases_python.md) | [exercices](python/bases/exercices.md) | variables, conditions, boucles, fonctions, listes, dictionnaires, fichiers |
| 2 | Bytes & encodage | [bytes_encodage](python/bytes/bytes_encodage.md) | [exercices](python/bytes/exercices.md) | `str` / `bytes`, hex, base64, `int.from_bytes`, endianness |

---

## 🖧 ASR — Systèmes & Réseaux

[Vue d'ensemble](ASR/README.md)

| # | Notion | 📘 Cours | 📝 Exercices | Mots-clés |
|:-:|---|---|---|---|
| 1 | Commandes Linux | [commandes_base](ASR/linux/commandes_base.md) | [exercices](ASR/linux/exercices.md) | `ls`, `cd`, `find`, `grep`, pipes, redirections, `chmod` |
| 2 | Bases du réseau | [reseau_bases](ASR/reseau/reseau_bases.md) | [exercices](ASR/reseau/exercices.md) | OSI, IPv4, CIDR, sous-réseaux, TCP/UDP, ports |

---

## 🔎 Par mot-clé

| Je cherche… | Où ? |
|---|---|
| AES, DES | [Symétrique](Crypto/symetrique/chiffrement_symetrique.md) |
| Analyse fréquentielle | [César](Crypto/classique/cesar/cesar.md) · [Vigenère](Crypto/classique/vigenere/vigenere.md) |
| Base64 | [Encodages](Crypto/encodage/bases_encodage.md) · [Python bytes](python/bytes/bytes_encodage.md) |
| Binaire / hexadécimal | [Encodages](Crypto/encodage/bases_encodage.md) |
| CBC, ECB, GCM | [Symétrique](Crypto/symetrique/chiffrement_symetrique.md) |
| CIDR, masque, sous-réseau | [Réseau](ASR/reseau/reseau_bases.md) |
| Droits (`chmod`, 755…) | [Linux](ASR/linux/commandes_base.md) |
| Euclide étendu, inverse modulaire | [Arithmétique modulaire](Crypto/arithmetique_modulaire/arithmetique_modulaire.md) |
| Exponentiation modulaire | [Arithmétique modulaire](Crypto/arithmetique_modulaire/arithmetique_modulaire.md) |
| Homme du milieu (MITM) | [Diffie-Hellman](Crypto/asymetrique/diffie_hellman/diffie_hellman.md) |
| Kerckhoffs | [Introduction](Crypto/introduction/notions_de_base.md) |
| Modèle OSI | [Réseau](ASR/reseau/reseau_bases.md) |
| Mot de passe, sel | [Hachage](Crypto/hachage/hachage.md) |
| One-Time Pad / masque jetable | [XOR](Crypto/logic_gate/XOR/simple_xor.md) · [Vigenère](Crypto/classique/vigenere/vigenere.md) |
| Opérateurs bit à bit (`&`, `\|`, `^`) | [Portes logiques](Crypto/logic_gate/README.md) |
| Ports (22, 80, 443…) | [Réseau](ASR/reseau/reseau_bases.md) |
| Signature numérique | [RSA](Crypto/asymetrique/rsa/rsa.md) |
| SHA-256, MD5 | [Hachage](Crypto/hachage/hachage.md) |
| TCP / UDP | [Réseau](ASR/reseau/reseau_bases.md) |
