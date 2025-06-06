# LuxHunt Analyse – WatchHunter Bot & Frontend

Dieses Repository enthält das vollständige Projekt von *LuxHunt*, bestehend aus Frontend (Next.js), Botlogik, Docker-Umgebung und SSL-Zertifikat-Setup.

## 🔍 Ziel dieser Codespace-Analyse:

- *Fehleranalyse und Optimierung* der Docker-Konfiguration (docker-compose.yml, traefik.yml, SSL-Verknüpfung, Mounts)
- *Überprüfung der Domain-Zuordnung* (luxhunt.de, watchhunter.luxhunt.de) inkl. Reverse Proxy via Traefik
- *Erkennung und Behebung aller strukturellen Probleme* im Container-Aufbau, Pfadzuweisung und Zertifikatszuordnung
- *Modernisierung & Review* des Frontends im Verzeichnis /luxhunt_main, speziell:
  - Smooth Scroll & visuelle Darstellung wie auf ayocin.com
  - Struktur als Apple-inspiriertes Interface
  - Responsive Layout für Mobilgeräte (iOS iPhone/iPad)
- *Botlogik* prüfen und vorbereiten für Multi-Plattform-Metasuche (Chrono24, WatchPatrol, eBay, Foren etc.)

## 📁 Projektstruktur (vereinfacht):


/luxhunt_main     → Next.js-Frontend
/luxhunt-frontend → alternative UI-Basis
/watchhunter-traefik → Routing-Konfiguration Subdomain
/docker-compose.yml
/traefik.yml
/ssl              → GeoTrust & Wildcard-Zertifikate


## 📦 Hinweise für Copilot & Codespaces:

- Nutze /luxhunt_main als Einstiegspunkt zur UI-Analyse
- Konzentriere dich auf Docker-Volumes, Mounts & Traefik-Label
- Ziel: *luxuriöse, voll funktionsfähige Metasuche*
- Bitte bei Problemen neue strukturierte docker-compose.yml oder traefik.yml-Varianten vorschlagen

---

## 🧠 Kontext für GitHub Copilot / Codespace

Bitte berücksichtige folgende Anforderungen beim Refactoring oder beim Hinzufügen neuer Services:

- Zertifikate befinden sich in: /root/ssl/luxhunt/
- Docker-Socket via: /var/run/docker.sock
- TLS-Konfiguration erfolgt manuell, kein Let's Encrypt
- Subdomain-Routing via Traefik für:
  - luxhunt.de (Mainpage)
  - watchhunter.luxhunt.de (Bot-API)
- Ziel: Deployment auf DigitalOcean mit robustem Reverse Proxy & Port-Kompatibilität
- Framework: Next.js (Frontend), Playwright (Bots), Docker, Traefik

Created: 06.06.2025