# 📝 Exercices — Fonctions de hachage

> **Cours :** [hachage.md](hachage.md) · Les corrigés sont dans les blocs repliables ▶

## Exercice 1 — Vrai ou faux ? 🟢

1. On peut déchiffrer un hash SHA-256 si on a la bonne clé.
2. Le hash d'un fichier de 1 Go est plus long que celui d'un fichier de 1 Ko.
3. Deux fichiers différents peuvent avoir le même hash.
4. Hacher deux fois le même mot donne le même résultat.

<details>
<summary>Corrigé</summary>

1. **Faux** : il n'y a pas de clé, et le hachage est à sens unique.
2. **Faux** : la taille de sortie est **fixe** (256 bits pour SHA-256).
3. **Vrai** : les collisions existent forcément (infinité d'entrées, nombre fini de sorties), mais doivent être impossibles à **trouver**.
4. **Vrai** : une fonction de hachage est **déterministe**.

</details>

## Exercice 2 — Tailles 🟢

Combien de caractères hexadécimaux contient une empreinte :

1. MD5 (128 bits) ?
2. SHA-1 (160 bits) ?
3. SHA-512 (512 bits) ?

<details>
<summary>Corrigé</summary>

1 caractère hexa = 4 bits.

1. 128 / 4 = **32**
2. 160 / 4 = **40**
3. 512 / 4 = **128**

</details>

## Exercice 3 — Identifier 🟢

Quel algorithme a probablement produit chacune de ces empreintes ?

1. `f02368945726d5fc2a14eb576f7276c0`
2. `2cb4b1431b84ec15d35ed83bb927e27e8967d75f4bcd9cc4b25c8d879ae23e18`

<details>
<summary>Corrigé</summary>

1. 32 caractères → 128 bits → **MD5**
2. 64 caractères → 256 bits → **SHA-256**

(Ce sont les hash de `bonjour`.)

</details>

## Exercice 4 — Le piège du echo 🟡

Pourquoi ces deux commandes donnent-elles des résultats différents ?

```bash
echo "bonjour" | sha256sum
echo -n "bonjour" | sha256sum
```

<details>
<summary>Corrigé</summary>

Sans `-n`, `echo` ajoute un **retour à la ligne** (`\n`) à la fin. On hache donc `bonjour\n` au lieu de `bonjour`. Un seul octet de différence → empreinte totalement différente (**effet avalanche**).

</details>

## Exercice 5 — Mots de passe 🟡

Une base de données stocke `utilisateur : SHA-256(mot_de_passe)`.

1. Un attaquant vole la base. Comment repère-t-il les utilisateurs ayant le même mot de passe ?
2. Comment peut-il retrouver les mots de passe faibles rapidement ?
3. Quelles sont les deux corrections à apporter ?

<details>
<summary>Corrigé</summary>

1. Ils ont **le même hash**.
2. Avec une **table précalculée** (ou un dictionnaire) : il hache des millions de mots de passe courants et compare. SHA-256 est très rapide, donc c'est efficace.
3. - Ajouter un **sel** aléatoire unique par utilisateur → mêmes mots de passe = hash différents, tables précalculées inutiles.
   - Utiliser une fonction **lente** conçue pour ça : **bcrypt, scrypt ou Argon2**.

</details>

## Exercice 6 — Intégrité 🟡

Vous téléchargez un logiciel et son SHA-256 **depuis le même site**. Le site a été piraté. La vérification du hash vous protège-t-elle ?

<details>
<summary>Corrigé</summary>

**Non** : l'attaquant peut remplacer le fichier **et** le hash affiché. Le hash protège contre les erreurs de transfert, pas contre un attaquant qui contrôle la source. Il faut une **signature numérique** (le hash est signé avec la clé privée de l'éditeur) ou récupérer le hash via un canal de confiance différent.

</details>

## Exercice 7 — Programmation 🔴

Écrire une fonction `verifier(fichier, hash_attendu)` qui renvoie `True` si le SHA-256 du fichier correspond.

<details>
<summary>Corrigé</summary>

```python
import hashlib

def verifier(fichier, hash_attendu):
    h = hashlib.sha256()
    with open(fichier, "rb") as f:          # "rb" : lecture en bytes
        for bloc in iter(lambda: f.read(4096), b""):
            h.update(bloc)                  # lecture par blocs : marche pour les gros fichiers
    return h.hexdigest() == hash_attendu.lower()
```

</details>
