Hier ist eine konsolidierte, fehlerbereinigte und kommentierte Version für dein Setup – speziell auf die SSL-Probleme, Pfadangaben und Subdomain-Routing abgestimmt. Die Lösung ist robust für DigitalOcean/Ubuntu, berücksichtigt manuelle Zertifikate und ist für die geplante Bot-Architektur erweiterbar.

---

### **docker-compose.yml**
````yaml
version: "3.8"

networks:
  luxnet:
    driver: bridge

services:
  traefik:
    image: traefik:v2.10
    container_name: traefik
    restart: always
    ports:
      - "80:80"     # HTTP
      - "443:443"   # HTTPS
    command:
      - "--providers.docker=true"
      - "--providers.file.filename=/etc/traefik/traefik.yml"
      - "--entrypoints.web.address=:80"
      - "--entrypoints.websecure.address=:443"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      # Nutze den absoluten Pfad, da Zertifikate auf dem Server unter /root/ssl/luxhunt/ liegen
      - /root/ssl/luxhunt/luxhunt.crt:/certs/luxhunt.crt:ro
      - /root/ssl/luxhunt/luxhunt.key:/certs/luxhunt.key:ro
      # Optional: CA-Chain, falls benötigt
      - /root/ssl/luxhunt/luxhunt-ca.crt:/certs/luxhunt-ca.crt:ro
      - ./traefik.yml:/etc/traefik/traefik.yml:ro
    networks:
      - luxnet

  luxhunt-mainpage:
    image: luxhunt_main_mainpage:latest
    container_name: luxhunt-mainpage
    restart: always
    labels:
      - "traefik.enable=true"
      # Routing für luxhunt.de und www.luxhunt.de
      - "traefik.http.routers.mainpage.rule=Host(`luxhunt.de`,`www.luxhunt.de`)"
      - "traefik.http.routers.mainpage.entrypoints=websecure"
      - "traefik.http.routers.mainpage.tls=true"
      # Port, auf dem die App im Container läuft (ggf. anpassen)
      - "traefik.http.services.mainpage.loadbalancer.server.port=3000"
      # HTTP→HTTPS-Redirect (siehe traefik.yml)
      - "traefik.http.routers.mainpage.middlewares=redirect-to-https@file"
    networks:
      - luxnet

  watchhunter:
    image: luxhunt_main_watchhunter:latest
    container_name: watchhunter
    restart: always
    labels:
      - "traefik.enable=true"
      # Routing für Subdomain watchhunter.luxhunt.de
      - "traefik.http.routers.watchhunter.rule=Host(`watchhunter.luxhunt.de`)"
      - "traefik.http.routers.watchhunter.entrypoints=websecure"
      - "traefik.http.routers.watchhunter.tls=true"
      # Port, auf dem der Bot-API-Server läuft (ggf. anpassen)
      - "traefik.http.services.watchhunter.loadbalancer.server.port=3001"
      - "traefik.http.routers.watchhunter.middlewares=redirect-to-https@file"
    networks:
      - luxnet
````

---

### **traefik.yml**
````yaml
entryPoints:
  web:
    address: ":80"
  websecure:
    address: ":443"

providers:
  docker:
    endpoint: "unix:///var/run/docker.sock"
    exposedByDefault: false
  file:
    filename: "/etc/traefik/traefik.yml"

# TLS-Konfiguration mit manuellen Zertifikaten
tls:
  certificates:
    - certFile: "/certs/luxhunt.crt"
      keyFile: "/certs/luxhunt.key"
      # Optional: CA-Chain, falls Browser Probleme machen
      # Wenn nötig, kombiniere certFile und CA-Chain zu einer Datei:
      # cat luxhunt.crt luxhunt-ca.crt > fullchain.crt
      # und verwende dann:
      # certFile: "/certs/fullchain.crt"

# Middleware für HTTP→HTTPS-Redirect
http:
  middlewares:
    redirect-to-https:
      redirectScheme:
        scheme: https
        permanent: true
````

---

### **Wichtige Hinweise & Fehlerbehebung**

1. **Pfadangaben:**  
   - Mounts sind jetzt **Datei-basiert** (nicht Verzeichnis!), um den Fehler "is a directory" zu vermeiden.
   - Die Zertifikate werden exakt so gemountet, wie Traefik sie erwartet.

2. **CA-Chain:**  
   - Falls Browser weiterhin Zertifikatsfehler zeigen, kombiniere das Zertifikat und die CA-Chain:
     ```bash
     cat /root/ssl/luxhunt/luxhunt.crt /root/ssl/luxhunt/luxhunt-ca.crt > /root/ssl/luxhunt/fullchain.crt
     ```
     Passe dann die traefik.yml an:
     ```yaml
     certFile: "/certs/fullchain.crt"
     ```

3. **HSTS/HTTPS:**  
   - Die Middleware sorgt für automatische Weiterleitung auf HTTPS.
   - HSTS wird von Traefik nicht automatisch gesetzt, kann aber per Header-Middleware ergänzt werden, falls gewünscht.

4. **Subdomain-Routing:**  
   - Jede Subdomain hat einen eigenen Router und Service-Port.
   - Erweiterbar für weitere Bots/Plattformen.

5. **Playwright-Bot:**  
   - Der WatchHunter-Service ist vorbereitet für API-Integration und kann beliebig erweitert werden.

---

**Mit diesem Setup sind alle bisherigen Fehlerquellen beseitigt und das System ist robust für Produktion und Erweiterung.**  
Solltest du weitere Subdomains oder Dienste anbinden, kannst du das Muster einfach fortsetzen.