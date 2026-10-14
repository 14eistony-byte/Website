# CDB Bäumlis Clan-Portal

Die Website enthält ein echtes Clan-Bewerbungsformular. Bewerber melden sich mit Discord an, müssen die Server-Regeln akzeptiert haben und können ihre Antworten über den Python-Webdienst in den konfigurierten Discord-Bewerbungskanal schicken.

## Lokal starten

1. `.env.example` kopieren und die Kopie `.env` nennen.
2. In `.env` Discord-Client-Secret, Bot-Token, Server-ID und ID der Regeln-akzeptiert-Rolle eintragen.
3. Den Discord OAuth2 Redirect exakt als `https://website-dvaj.onrender.com/auth/callback` in der Discord Developer Portal Anwendung hinterlegen.
4. Im Projektordner `py server.py` ausführen und lokal `http://localhost:3000/bewerbung.html` öffnen. Für lokale Discord-Anmeldung muss zusätzlich eine lokale Redirect-URI eingerichtet und `WEBSITE_URL`/`DISCORD_REDIRECT_URI` passend gesetzt werden.

## Render veröffentlichen

Das Formular braucht einen **Python Web Service**. Ein reiner Static-Site-Dienst kann die Anmeldungs- und Bewerbungs-API nicht ausführen. Das Projekt hat eine `render.yaml` mit Startbefehl und Health-Check. Beim bestehenden Dienst müssen die Dateien aus diesem Projekt bereitgestellt und der Dienst als Python Web Service konfiguriert sein.

In Render als Umgebungsvariablen hinterlegen:

- `WEBSITE_URL` = `https://website-dvaj.onrender.com`
- `DISCORD_CLIENT_ID` = `1556687990963576962`
- `DISCORD_CLIENT_SECRET` = Secret aus dem Discord Developer Portal
- `DISCORD_REDIRECT_URI` = `https://website-dvaj.onrender.com/auth/callback`
- `DISCORD_BOT_TOKEN` = Token des Bots, der Schreibrechte im Bewerbungs-Kanal hat
- `GUILD_ID` = ID deines Discord-Servers
- `RULES_ACCEPTED_ROLE_ID` = ID der Rolle, die der Bot nach Zustimmung vergibt
- `APPLICATION_CHANNEL_ID` = `1558576631814299759` (oder die ID deines Bewerbungs-Kanals)

Nach jedem Speichern der Variablen den Dienst neu deployen. Der Bot muss Mitglied des Servers sein und im Bewerbungs-Kanal Nachrichten senden dürfen. Lege echte Geheimnisse nur in Render oder lokal in `.env` ab, niemals in Dateien unter `public/`.

## Seiten

- `public/index.html` — Clan-Startseite
- `public/bewerbung.html` — Discord-Anmeldung und Bewerbungsformular
- `public/spieler.html` — Minecraft-Profil-Checker
- `public/quests.html` — persönliche Questliste
- `public/builds.html` — Build-Galerie
- `public/events.html` — Eventboard
- `public/regeln.html` — Regeln und FAQ
- `server.py` — Python-Webserver, Discord OAuth und Formular-API
