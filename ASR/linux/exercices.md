# 📝 Exercices — Commandes Linux

> **Cours :** [commandes_base.md](commandes_base.md) · Les corrigés sont dans les blocs repliables ▶

## Exercice 1 — Arborescence 🟢

Depuis votre dossier personnel, avec des commandes :

1. Créer `projet/src` et `projet/docs`
2. Créer un fichier vide `projet/src/main.py`
3. Le copier dans `projet/docs/` sous le nom `exemple.py`
4. Renommer `projet/docs` en `projet/documentation`
5. Supprimer tout le dossier `projet`

<details>
<summary>Corrigé</summary>

```bash
cd ~
mkdir -p projet/src projet/docs
touch projet/src/main.py
cp projet/src/main.py projet/docs/exemple.py
mv projet/docs projet/documentation
rm -r projet
```

</details>

## Exercice 2 — Chemins 🟢

Vous êtes dans `/home/alice/docs`. Où êtes-vous après chacune de ces commandes (indépendantes) ?

1. `cd ..`
2. `cd ../..`
3. `cd /tmp`
4. `cd ~` (en étant `alice`)
5. `cd ./cours`

<details>
<summary>Corrigé</summary>

1. `/home/alice`
2. `/home`
3. `/tmp` (chemin **absolu** : commence par `/`)
4. `/home/alice`
5. `/home/alice/docs/cours` (chemin **relatif**)

</details>

## Exercice 3 — Droits 🟢

1. Convertir `rwxr-xr--` en octal.
2. Convertir `640` en lettres.
3. Pour un fichier `-rw-r----- alice devs rapport.txt` : qui peut lire ? qui peut modifier ?

<details>
<summary>Corrigé</summary>

1. `rwx`=4+2+1=7, `r-x`=4+0+1=5, `r--`=4 → **`754`**
2. 6=`rw-`, 4=`r--`, 0=`---` → **`rw-r-----`**
3. **Lire :** alice et les membres du groupe `devs`. **Modifier :** seulement alice. Les autres : rien.

</details>

## Exercice 4 — Chercher 🟡

1. Trouver tous les fichiers `.txt` de votre dossier personnel.
2. Compter les lignes de `/etc/passwd` qui contiennent `bash`.

<details>
<summary>Corrigé</summary>

```bash
find ~ -name "*.txt"
grep bash /etc/passwd | wc -l     # ou : grep -c bash /etc/passwd
```

</details>

## Exercice 5 — Redirections 🟡

Que contient `f.txt` après ces commandes ?

```bash
echo "un" > f.txt
echo "deux" >> f.txt
echo "trois" > f.txt
echo "quatre" >> f.txt
```

<details>
<summary>Corrigé</summary>

```
trois
quatre
```

`>` **écrase** le fichier, `>>` **ajoute** à la fin. La 3ᵉ commande a effacé `un` et `deux`.

</details>
