# vCenter Sync for NetBox
Diese Ansible‑Rolle synchronisiert deine vCenter‑Umgebung mit NetBox mit den unten genannten Funktionen.
In meiner Umgebung dauert dies ca 20 minuten.
Dies ist nicht perfekt aber es tut was es soll.

# Voraussetzungen
Ansible: Version 2.9 oder höher
Python: 3.x
Collections:
community.vmware
vCenter:
Erreichbarer vCenter-Server mit gültigen Zugangsdaten
NetBox:
Eine NetBox‑Instanz mit API‑Zugang und gültigem API‑Token
Erstelle ansible role

# Variablen
Unter vcentersync/defaults/main.yml
Definiert ihr eure Login Daten am vcenter, euren API Key in Netbox und welches Cluster überprüft werden soll in Netbox

# Funktionen
## VM‑Synchronisation:
VMs, die in vCenter existieren, werden in NetBox als virtuelle Maschinen (Virtual Machines) eingetragen.

## IP‑Adress-Synchronisation:
Aus den vCenter-Daten werden IP-Adressen extrahiert. Fehlende IPs in NetBox werden über die API hinzugefügt.

## Schnittstellen-Synchronisation:
Die Netzwerkschnittstellen (Interfaces) der VMs werden erfasst und in NetBox erstellt, sofern sie noch nicht existieren.

##IP‑zu‑Interface Verknüpfung:
Die IP-Adressen werden den entsprechenden Schnittstellen in NetBox zugeordnet (gepatcht).

## Status-Synchronisation:
Der Status der VMs (active/offline) wird in NetBox anhand des Power‑States in vCenter aktualisiert.

## Automatischer Löschprozess:
Falls VMs in vCenter gelöscht werden, erfolgt auch in NetBox die Entfernung der VM sowie der zugehörigen IP-Adressen und Schnittstellen. Dabei wird anhand eines Vergleichs der in vCenter vorhandenen Objekte mit den in NetBox vorhandenen Daten entschieden, welche Einträge gelöscht werden müssen.

# geplant
- tags synconisieren
- Betriebs systemem sync
- mehrere Cluster aus einem vcenter abrufen können
