# 🐍 Python — Les bases

> **Niveau :** débutant

## Lancer du Python

```bash
python3               # console interactive (quitter avec exit())
python3 script.py     # exécuter un fichier
```

## Variables et types

```python
nom = "Alice"        # str   (chaîne de caractères)
age = 20             # int   (entier)
taille = 1.75        # float (nombre à virgule)
admin = False        # bool  (True / False)
data = b"\x41\x42"   # bytes (octets bruts)

print(type(age))     # <class 'int'>
```

## Afficher et lire

```python
nom = input("Ton pseudo : ")
print(f"Salut {nom} !")      # f-string : on met des variables entre {}
```

## Conditions

```python
age = 20
if age >= 18:
    print("majeur")
elif age >= 13:
    print("ado")
else:
    print("enfant")
```

⚠️ En Python, **l'indentation** (4 espaces) définit les blocs. Pas d'accolades !

## Listes et dictionnaires

```python
ports = [22, 80, 443]
ports.append(8080)
print(ports[0])        # 22
print(len(ports))      # 4

user = {"nom": "Alice", "uid": 1000}
print(user["nom"])     # Alice
user["shell"] = "/bin/bash"
```

## Boucles

```python
for port in ports:
    print(port)

for i in range(5):     # 0, 1, 2, 3, 4
    print(i)

n = 3
while n > 0:
    print(n)
    n -= 1
```

## Fonctions

```python
def est_port_web(port: int) -> bool:
    return port in (80, 443, 8080)

print(est_port_web(443))   # True
```

## Lire / écrire un fichier

```python
with open("wordlist.txt") as f:
    for ligne in f:
        print(ligne.strip())

with open("sortie.txt", "w") as f:
    f.write("hello\n")
```

## Exercice

Écris une fonction `compter_voyelles(texte)` qui renvoie le nombre de voyelles dans une chaîne.

<details>
<summary>Solution</summary>

```python
def compter_voyelles(texte):
    return sum(1 for c in texte.lower() if c in "aeiouy")

print(compter_voyelles("Hello 2600"))  # 2
```
</details>

➡️ Suite : [Bytes & encodage](../bytes/bytes_encodage.md)
