# Netzwerk Basics (Portfolio Projekt 2)

Dieses Projekt zeigt meine praktischen Grundlagen im Netzwerkbereich.  
Ich habe die wichtigsten Befehle in Linux ausprobiert, um IP-Adressen, DNS, Ports und Verbindungen zu verstehen.  
Diese Themen gehören zu typischen Aufgaben im IT-Betrieb und in der Systemintegration.

---

## Zweck des Projekts

Ich wollte verstehen, wie man:

- die IP-Adresse eines Systems prüft  
- testet, ob das Netzwerk funktioniert  
- DNS-Abfragen macht (Domain → IP)  
- Internetverbindungen prüft  
- Ports und Dienste kontrolliert  

Diese Grundlagen helfen bei Fehleranalyse, Betrieb und Dokumentation von IT-Services.

---

## Umgebung

Ich nutze einen Ubuntu-Linux-Container:

```
docker run -it ubuntu bash

```
Damit habe ich eine saubere Testumgebung, ohne extra ein Linux installieren zu müssen.

## 1. IP-Adresse anzeigen

Zuerst habe ich das Paket iproute2 installiert:
```
apt update
apt install iproute2 -y
```

Dann kann man die Netzwerkinterfaces sehen:
```
ip a
```

Ergebnis:

- lo (127.0.0.1) = Loopback, System spricht mit sich selbst

- eth0 (z. B. 172.17.0.2) = die IP des Containers im Docker-Netzwerk

Das zeigt, ob das Netzwerk aktiv ist.

## 2. Internet-Verbindung testen (Ping)

Ich habe Ping installiert:
```
apt install iputils-ping -y
```
### Beispiel 1: Internet erreichbar?
```
ping -c 4 8.8.8.8
```

8.8.8.8 ist ein öffentlicher DNS-Server von Google.
Wenn der Ping klappt → Internetverbindung funktioniert.

### Beispiel 2: DNS funktioniert?
```
ping -c 4 google.com
ping -c 4 amazon.de
```

## 3. DNS-Abfragen (nslookup, dig, host)

Ich habe die DNS-Tools installiert:
```
apt install dnsutils -y
```
### nslookup
```
nslookup amazon.de
```

Zeigt die IP-Adresse, die der DNS-Server zurückgibt.

### dig
```
dig amazon.de
```

Zeigt Details wie TTL (Gültigkeitsdauer eines DNS-Eintrags).

### host
```
host amazon.de
```

Zeigt kurz die IPv4- oder IPv6-Adressen.

*DNS ist wichtig*, um zu verstehen, wie Systeme im Netzwerk gefunden werden.

## 4. Ports und Verbindungen prüfen

Ich habe das Paket net-tools installiert:
```
apt install net-tools -y
```
*Offene Verbindungen anzeigen:*
```
netstat -tulnp
```

Damit sieht man:

- welche Dienste laufen
- welche Ports benutzt werden
- welcher Prozess dahinter steckt

Das hilft bei Fehlern wie „Dienst erreichbar / nicht erreichbar“.

## 5. Mini-Firewall-Beispiel

Mit ufw könnte man Regeln setzen (nur Beispiel, nicht im Container aktiviert):
```
ufw allow 80/tcp
ufw deny 22/tcp
```

Damit versteht man Grundprinzipien einer Firewall (erlauben/blockieren).

Wenn Domains funktionieren → DNS löst Namen in IP-Adressen um.