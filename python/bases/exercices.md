# 📝 Exercices — Python : les bases

> **Cours :** [bases_python.md](bases_python.md) · Les corrigés sont dans les blocs repliables ▶
> Essayez **vraiment** avant de regarder la solution 😉

## Exercice 1 — Nombres pairs 🟢

Afficher tous les nombres pairs de 0 à 20 (inclus).

<details>
<summary>Corrigé</summary>

```python
for i in range(0, 21, 2):
    print(i)
```

</details>

## Exercice 2 — Moyenne 🟢

Écrire une fonction `moyenne(notes)` qui renvoie la moyenne d'une liste de notes.
`moyenne([12, 15, 9])` doit renvoyer `12.0`.

<details>
<summary>Corrigé</summary>

```python
def moyenne(notes):
    total = 0
    for n in notes:
        total += n
    return total / len(notes)

print(moyenne([12, 15, 9]))   # 12.0
```

(Version courte : `sum(notes) / len(notes)`)

</details>

## Exercice 3 — Maximum 🟢

Écrire `maximum(liste)` qui renvoie le plus grand élément **sans utiliser `max()`**.

<details>
<summary>Corrigé</summary>

```python
def maximum(liste):
    plus_grand = liste[0]
    for x in liste:
        if x > plus_grand:
            plus_grand = x
    return plus_grand

print(maximum([3, 17, 8, 2]))   # 17
```

</details>

## Exercice 4 — FizzBuzz 🟢

Pour les nombres de 1 à 15, afficher :
`Fizz` si divisible par 3, `Buzz` si divisible par 5, `FizzBuzz` si divisible par les deux, sinon le nombre.

<details>
<summary>Corrigé</summary>

```python
for i in range(1, 16):
    if i % 15 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)
```

⚠️ Le test `% 15` doit être **en premier**, sinon 15 afficherait seulement `Fizz`.

</details>

## Exercice 5 — Palindrome 🟡

Écrire `est_palindrome(mot)` qui renvoie `True` si le mot se lit pareil dans les deux sens (`"kayak"`, `"radar"`).

<details>
<summary>Corrigé</summary>

```python
def est_palindrome(mot):
    mot = mot.lower()
    return mot == mot[::-1]      # [::-1] inverse la chaîne

print(est_palindrome("Kayak"))   # True
print(est_palindrome("python"))  # False
```

Sans slicing :

```python
def est_palindrome(mot):
    mot = mot.lower()
    for i in range(len(mot) // 2):
        if mot[i] != mot[-1 - i]:
            return False
    return True
```

</details>

## Exercice 6 — Compter les mots 🟡

Écrire `compter_mots(phrase)` qui renvoie un dictionnaire `{mot: nombre d'apparitions}`.

<details>
<summary>Corrigé</summary>

```python
def compter_mots(phrase):
    compteur = {}
    for mot in phrase.lower().split():
        if mot in compteur:
            compteur[mot] += 1
        else:
            compteur[mot] = 1
    return compteur

print(compter_mots("le chat et le chien"))
# {'le': 2, 'chat': 1, 'et': 1, 'chien': 1}
```

</details>

## Exercice 7 — Factorielle récursive 🟡

Réécrire la fonction `factorielle(n)` du cours en version **récursive**.

<details>
<summary>Corrigé</summary>

```python
def factorielle(n):
    if n <= 1:          # cas de base : sans lui, la récursion ne s'arrête jamais
        return 1
    return n * factorielle(n - 1)

print(factorielle(5))   # 120
```

</details>

## Exercice 8 — Fichier 🟡

Le fichier `notes.txt` contient une note par ligne. Écrire un programme qui affiche le nombre de notes, la moyenne et le nombre de notes ≥ 10.

<details>
<summary>Corrigé</summary>

```python
notes = []
with open("notes.txt") as f:
    for ligne in f:
        ligne = ligne.strip()
        if ligne:                      # ignorer les lignes vides
            notes.append(float(ligne))

print("Nombre :", len(notes))
print("Moyenne :", sum(notes) / len(notes))
print("Reçus :", len([n for n in notes if n >= 10]))
```

</details>
