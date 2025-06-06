📦 Projektauftrag an GitHub Copilot

Ziel:
Erstelle ein vollständiges LuxHunt-System (inkl. WatchHunter, CarHunter, HouseHunter, BagHunter) basierend auf den bisherigen Inhalten, Befehlen, Screenshots und YAMLs dieses Projekts.

⸻

✅ Rahmenbedingungen (Bestätigt aus Chatverlauf):
	•	Produktionsumgebung: DigitalOcean Droplet (Ubuntu), Root-Zugriff vorhanden
	•	Live-IP: 164.92.166.12
	•	Domainverwaltung: INWX, z. B. luxfund.de auf DigitalOcean umgeleitet (NS-Einträge gesetzt)
	•	Zertifikate:
	•	luxhunt.crt
	•	luxhunt.key
	•	luxhunt-ca.crt
→ Pfad: /root/ssl/luxhunt/
	•	Reverse-Proxy: Traefik v2 mit manuellen Zertifikaten (kein ACME/Let’s Encrypt nötig)
	•	Bisher funktionierende Dienste: luxhunt-mainpage (Port 3000), Container vorhanden
	•	Smooth Scroll + UI Design: Wie ayocin.com – modern, Apple-inspiriert, mobiloptimiert
	•	Botbasis: WatchHunter bereits vorbereitet (Port 3001); weitere folgen

⸻

🧠 Aufgabenstellung an Copilot:
	1.	Struktur neu aufbauen:
Erstelle ein vollständiges Projektverzeichnis mit:
	•	root/luxhunt_main/
	•	root/luxhunt_traefik/
	•	root/luxhunt_api/
	•	root/ssl/
	•	docker-compose.yml und traefik.yml mit aktuellen Pfaden & Produktionslogik
	2.	YAMLs vollständig generieren & kommentieren
	•	Alle Ports & Labels korrekt
	•	Subdomain-Routing zu watchhunter.luxhunt.de, carhunter.luxhunt.de etc.
	•	HTTPS-Erzwingung über Middleware
	3.	Deployment-Befehle liefern für DigitalOcean-Droplet (Web-Terminal!)
	•	Keine externen Tools nötig (kein SCP, kein Git-CLI, kein GitHub Desktop)
	•	Alle Befehle direkt einfügbar über Konsole
	•	Optional: Bash-Script oder SIP-Kette
	4.	Antwort auf folgende Kommentarfelder liefern (aus vorherigen Vorschlägen):
	•	# optional: fullchain.crt
	•	# exposedByDefault: false (begründen oder anpassen)
	•	# root/luxhunt/watchhunter nicht vorhanden → was tun?
	5.	Produktionsfähig machen
	•	Finales docker-compose up -d
	•	Fehleranalyse vorbereiten (Logs anzeigen, bei Fehlern gezielt Hinweise geben)
	•	Vorschläge für Erweiterung

⸻

📂 Zielverzeichnis nach Deployment:
/opt/luxhunt/
├── docker-compose.yml
├── traefik.yml
├── ssl/
│   ├── luxhunt.crt
│   ├── luxhunt.key
│   └── luxhunt-ca.crt
├── luxhunt_main/
├── luxhunt_api/
├── luxhunt_traefik/
├── watchhunter/
├── carhunter/
├── househunter/
└── baghunter/
📌 Letzter Hinweis für GitHub Copilot:

Dies ist ein vollständig produktives Projekt. Es soll direkt live gehen – keine Teststruktur, sondern ein sauberes, lauffähiges Grundsystem mit Reverse-Proxy, manueller Zertifikatslogik, Botanbindung, modernen UI-Standards und nachhaltiger Skalierbarkeit.
Bitte baue daraus die vollständige Projektstruktur mit allen Unterordnern und gib mir alle nötigen Produktionsbefehle für mein DigitalOcean Droplet.