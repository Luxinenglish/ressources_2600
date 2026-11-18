# 🐧 Commandes Linux de base

> **Niveau :** débutant

💡 Bloqué sur une commande ? `man <commande>` ou `<commande> --help`.

## Se repérer

| Commande | Rôle |
|---|---|
| `pwd` | affiche le dossier courant |
| `ls -la` | liste les fichiers (y compris cachés) avec les détails |
| `cd /chemin` | change de dossier (`cd ..` = remonter, `cd ~` = home) |
| `whoami` | quel utilisateur suis-je ? |
| `id` | mon UID, GID et mes groupes |

## Fichiers et dossiers

| Commande | Rôle |
|---|---|
| `touch f.txt` | crée un fichier vide |
| `mkdir -p a/b` | crée des dossiers |
| `cp src dst` | copie (`-r` pour un dossier) |
| `mv src dst` | déplace / renomme |
| `rm f.txt` | supprime (⚠️ pas de corbeille !) |
| `cat f.txt` | affiche le contenu |
| `less f.txt` | lit un long fichier page par page (`q` pour quitter) |
| `head` / `tail -n 20` | début / fin d'un fichier |

## Chercher

```bash
find ~ -name "*.txt"                 # chercher des fichiers par nom
grep -ri "bash" /etc 2>/dev/null     # chercher un texte dans des fichiers
which python3                        # où est installé un programme
```

`2>/dev/null` cache les messages d'erreur (ex : « Permission denied »).

## Redirections et pipes

```bash
echo "hello" > f.txt     # écrit (écrase)
echo "world" >> f.txt    # ajoute à la fin
cat f.txt | grep world   # | envoie la sortie d'une commande à la suivante
cat f.txt | sort | uniq -c
```

## Droits

```
-rwxr-x--- 1 alice devs 1234 nov 18 10:00 script.sh
 └┬┘└┬┘└┬┘
  │  │  └── autres  : ---  (rien)
  │  └───── groupe  : r-x  (lire + exécuter)
  └──────── proprio : rwx  (lire + écrire + exécuter)
```

| Lettre | Valeur | Sens |
|:-:|:-:|---|
| `r` | 4 | lecture |
| `w` | 2 | écriture |
| `x` | 1 | exécution |

```bash
chmod 750 script.sh   # rwx r-x ---
chmod +x script.sh    # rend exécutable
sudo commande         # exécuter en tant que root
```

## Processus et système

| Commande | Rôle |
|---|---|
| `ps aux` | liste les processus |
| `top` / `htop` | moniteur en temps réel |
| `kill <PID>` | tue un processus |
| `uname -a` | infos sur le noyau |
| `df -h` | espace disque |

📝 [Exercices corrigés](exercices.md)
