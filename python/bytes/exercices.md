# 📝 Exercices — Python : bytes & encodage

[🏠 Index](../../index.md)

> **Cours :** [bytes_encodage.md](bytes_encodage.md) · Les corrigés sont dans les blocs repliables ▶

## Exercice 1 — Prédire le résultat 🟢

Sans exécuter, donner le résultat de :

1. `"abc".encode()`
2. `b"abc"[1]`
3. `len("é".encode())`
4. `type(b"A"[0])`

<details>
<summary>Corrigé</summary>

1. **`b'abc'`**
2. **`98`** — indexer un `bytes` donne un **entier** (le code de `b`)
3. **`2`** — en UTF-8, `é` est codé sur 2 octets
4. **`<class 'int'>`**

</details>

## Exercice 2 — Texte ↔ hexa 🟢

1. Convertir `"Python"` en chaîne hexadécimale.
2. Convertir `"426f6e6a6f7572"` en texte.

<details>
<summary>Corrigé</summary>

```python
print("Python".encode().hex())                  # 507974686f6e
print(bytes.fromhex("426f6e6a6f7572").decode()) # Bonjour
```

</details>

## Exercice 3 — Texte en binaire 🟡

Écrire `en_binaire(texte)` qui renvoie chaque caractère sur 8 bits, séparés par des espaces.
`en_binaire("Hi")` → `"01001000 01101001"`

<details>
<summary>Corrigé</summary>

```python
def en_binaire(texte):
    return " ".join(format(octet, "08b") for octet in texte.encode())

print(en_binaire("Hi"))   # 01001000 01101001
```

`format(x, "08b")` : binaire sur 8 caractères, complété avec des 0 à gauche.

</details>

## Exercice 4 — XOR de deux bytes 🟡

Écrire `xor_bytes(a, b)` qui fait le XOR octet par octet de deux `bytes` **de même longueur**.
Lever une `ValueError` si les longueurs sont différentes.

<details>
<summary>Corrigé</summary>

```python
def xor_bytes(a: bytes, b: bytes) -> bytes:
    if len(a) != len(b):
        raise ValueError("longueurs différentes")
    return bytes(x ^ y for x, y in zip(a, b))

print(xor_bytes(b"\x0f\xf0", b"\xff\xff"))   # b'\xf0\x0f'
```

</details>

## Exercice 5 — Ordre des octets 🔴

Que valent :

1. `int.from_bytes(b"\x01\x00", "big")`
2. `int.from_bytes(b"\x01\x00", "little")`

<details>
<summary>Corrigé</summary>

1. **`256`** — *big endian* : l'octet de poids fort est en premier → `0x0100`
2. **`1`** — *little endian* : l'octet de poids faible est en premier → `0x0001`

</details>
