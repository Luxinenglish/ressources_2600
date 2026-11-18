# 🐍 Python — Bytes & encodage

> **Niveau :** débutant · **Prérequis :** [les bases](../bases/bases_python.md), [bases & encodages](../../Crypto/encodage/bases_encodage.md)

En crypto et en exploitation, on manipule des **octets bruts**, pas du texte.
Python fait la différence entre les deux :

| Type | Exemple | Contient |
|---|---|---|
| `str` | `"Hi"` | du texte (caractères Unicode) |
| `bytes` | `b"Hi"` | des octets (0 à 255) |

## Passer de l'un à l'autre

```python
texte = "Hi"
octets = texte.encode()     # str -> bytes : b'Hi'
retour = octets.decode()    # bytes -> str : 'Hi'
```

## Un bytes, c'est une liste d'entiers

```python
data = b"Hi"
print(data[0])          # 72  (un int, pas un caractère !)
print(list(data))       # [72, 105]
print(bytes([72, 105])) # b'Hi'
```

## Hexadécimal

```python
data = b"Hi"
print(data.hex())                # '4869'
print(bytes.fromhex("4869"))     # b'Hi'
```

## Base64

```python
import base64
print(base64.b64encode(b"Hi"))   # b'SGk='
print(base64.b64decode("SGk="))  # b'Hi'
```

## Entiers ↔ bytes (très utilisé en RSA)

```python
n = int.from_bytes(b"Hi", "big")   # 18537
print(n.to_bytes(2, "big"))        # b'Hi'
```

## Mini-boîte à outils CTF

```python
import base64

def xor(a: bytes, b: bytes) -> bytes:
    """XOR de deux bytes (la clé est répétée si plus courte)."""
    return bytes(x ^ b[i % len(b)] for i, x in enumerate(a))

secret = bytes.fromhex("1a0b1c")
print(xor(secret, b"key"))
```

👉 Mise en pratique : [XOR simple](../../Crypto/logic_gate/XOR/simple_xor.md)
