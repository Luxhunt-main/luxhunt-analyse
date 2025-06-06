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

Created: 06.06.2025