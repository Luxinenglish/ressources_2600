# 🔢 Bases & encodages

> **Niveau :** débutant

⚠️ **Encodage ≠ chiffrement.** Un encodage change la *représentation* des données, sans clé.
N'importe qui peut le décoder. Un chiffrement nécessite une clé.

## Binaire, décimal, hexadécimal

| Base | Nom | Chiffres utilisés | Préfixe Python | Exemple (65) |
|:---:|---|---|---|---|
| 2 | Binaire | `0 1` | `0b` | `0b1000001` |
| 8 | Octal | `0-7` | `0o` | `0o101` |
| 10 | Décimal | `0-9` | — | `65` |
| 16 | Hexadécimal | `0-9 a-f` | `0x` | `0x41` |

- 1 **bit** = `0` ou `1`
- 1 **octet** (*byte*) = 8 bits = valeurs de `0` à `255` = `0x00` à `0xFF`
- 1 chiffre hexa = 4 bits → **1 octet = 2 caractères hexa**

```python
print(bin(65), oct(65), hex(65))   # 0b1000001 0o101 0x41
print(int("41", 16))               # 65
print(int("1000001", 2))           # 65
```

### Convertir à la main (binaire → décimal)

```
  1    0    0    0    0    0    1
 2⁶   2⁵   2⁴   2³   2²   2¹   2⁰
 64 +  0 +  0 +  0 +  0 +  0 +  1  = 65
```

## ASCII

Table qui associe un nombre (0-127) à un caractère.

| Caractère | Décimal | Hexa |
|:-:|:-:|:-:|
| `espace` | 32 | `0x20` |
| `0` | 48 | `0x30` |
| `A` | 65 | `0x41` |
| `a` | 97 | `0x61` |

💡 Minuscule = majuscule + 32 (`0x20`) → `'A' ^ 0x20 == 'a'`

```python
print(ord("A"))   # 65
print(chr(97))    # a
```

## Base64

Encode des données binaires avec seulement 64 caractères imprimables : `A-Z a-z 0-9 + /` (et `=` pour le remplissage).

**Comment le reconnaître :** que des caractères alphanumériques + `+/`, longueur multiple de 4, souvent un ou deux `=` à la fin.

```python
import base64

e = base64.b64encode(b"2600")
print(e)                      # b'MjYwMA=='
print(base64.b64decode(e))    # b'2600'
```

En ligne de commande :

```bash
echo -n "2600" | base64        # MjYwMA==
echo "MjYwMA==" | base64 -d    # 2600
```

## Reconnaître un encodage au premier coup d'œil

| Ça ressemble à… | C'est probablement |
|---|---|
| `01001000 01101001` | Binaire |
| `48 69` / `4869` | Hexadécimal |
| `SGk=` | Base64 |
| `%48%69` | URL encoding |
| `&#72;&#105;` | Entités HTML |
| `.... ..` | Morse |

🛠️ **Outil indispensable :** [CyberChef](https://gchq.github.io/CyberChef/) (la baguette magique « Magic » devine souvent l'encodage toute seule).
