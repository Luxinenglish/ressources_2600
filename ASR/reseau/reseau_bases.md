# 🌐 Bases du réseau

> **Niveau :** débutant

## Le modèle OSI (et TCP/IP)

| # | Couche OSI | Exemple | Unité | Modèle TCP/IP |
|:-:|---|---|---|---|
| 7 | Application | HTTP, DNS, SSH | données | Application |
| 6 | Présentation | TLS, encodage | données | Application |
| 5 | Session | — | données | Application |
| 4 | Transport | TCP, UDP | segment | Transport |
| 3 | Réseau | IP, ICMP | paquet | Internet |
| 2 | Liaison | Ethernet, Wi-Fi (MAC) | trame | Accès réseau |
| 1 | Physique | câble, ondes | bit | Accès réseau |

💡 Moyen mnémotechnique (de 1 à 7) : **P**our **L**e **R**éseau **T**out **S**e **P**asse **A**utomatiquement.

## Adresse IP (IPv4)

4 octets écrits en décimal : `192.168.1.42`

Le **masque** indique quelle partie est le *réseau* et quelle partie est l'*hôte* :

```
IP     : 192.168.1.42   /24
Masque : 255.255.255.0
Réseau : 192.168.1.0       ← première adresse
Broadcast : 192.168.1.255  ← dernière adresse
Hôtes utilisables : 192.168.1.1 → 192.168.1.254  (2⁸ - 2 = 254)
```

| CIDR | Masque | Nb d'hôtes |
|:-:|:-:|:-:|
| /8 | 255.0.0.0 | 16 777 214 |
| /16 | 255.255.0.0 | 65 534 |
| /24 | 255.255.255.0 | 254 |
| /30 | 255.255.255.252 | 2 |

🧠 L'adresse réseau = `IP AND masque` → c'est un [AND bit à bit](../../Crypto/logic_gate/README.md) !

### Plages privées (RFC 1918)

- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`
- (+ `127.0.0.0/8` = localhost)

## TCP vs UDP

| | TCP | UDP |
|---|---|---|
| Connexion | oui (*three-way handshake* : SYN → SYN/ACK → ACK) | non |
| Fiabilité | garantit l'ordre et la livraison | aucune garantie |
| Vitesse | plus lent | plus rapide |
| Exemples | HTTP, SSH, FTP | DNS, DHCP, streaming, jeux |

## Ports à connaître

| Port | Service |
|:-:|---|
| 21 | FTP |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |
| 445 | SMB |
| 3306 | MySQL |
| 3389 | RDP |

## Commandes réseau utiles

```bash
ip a                     # mes interfaces et adresses IP
ip route                 # table de routage (passerelle par défaut)
ping 8.8.8.8             # tester la connectivité
traceroute google.com    # chemin des paquets
ss -tulpn                # ports en écoute sur ma machine
dig google.com           # requête DNS
curl -I https://example.com   # en-têtes HTTP
nmap 192.168.1.0/24      # scanner un réseau (⚠️ uniquement sur VOS réseaux / avec autorisation)
```
