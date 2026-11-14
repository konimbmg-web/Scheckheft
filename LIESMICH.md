# Golf V Scheckheft — als App aufs iPhone

Diese Dateien sind eine vollwertige Web-App (PWA). Einmal auf einen Webspace
gelegt, landet sie als Icon auf dem Homescreen, startet ohne Safari-Leiste und
läuft auch ohne Empfang — in der Tiefgarage genauso wie am Straßenrand.

## Was drin ist

    index.html              die App
    manifest.webmanifest    Name, Icon und Startverhalten
    sw.js                   Service Worker, macht die App offline-fähig
    icons/                  App-Icons
    core.html               Quelle für den Seiteninhalt
    build.py                baut index.html aus core.html

## Hosten — der Weg über GitHub Pages

Kostenlos und dauerhaft. Etwa fünf Minuten.

1. Auf github.com ein Konto anlegen, falls noch keines da ist.
2. **New repository**, Name zum Beispiel `scheckheft`, Sichtbarkeit **Public**,
   anlegen.
3. **Add file → Upload files**. Zieh `index.html`, `manifest.webmanifest`,
   `sw.js` und den ganzen Ordner `icons` hinein. **Commit changes**.
4. **Settings → Pages**. Unter *Source* **Deploy from a branch** wählen, Branch
   `main`, Ordner `/ (root)`, **Save**.
5. Nach ein, zwei Minuten steht oben die Adresse:
   `https://DEINNAME.github.io/scheckheft/`

HTTPS ist Pflicht — ohne verweigert iOS den Service Worker. GitHub Pages liefert
das von allein. Netlify Drop, Cloudflare Pages oder jeder eigene Webspace mit
Zertifikat tun es genauso.

## Aufs iPhone legen

1. Die Adresse **in Safari** öffnen. Chrome kann das unter iOS nicht.
2. Teilen-Symbol antippen → **Zum Home-Bildschirm**.
3. Namen bestätigen. Das Icon liegt jetzt zwischen den anderen Apps.

Beim ersten Start einmal online sein, danach läuft alles offline.

## Daten

Die App speichert auf dem Gerät, nichts geht an einen Server. Darum zwei Dinge:

- Unter **Fahrzeug → Daten sichern** regelmäßig exportieren, besonders vor einem
  Gerätewechsel. Der Export ist eine JSON-Datei, die dieselbe App wieder einliest.
- Die App nicht aus dem Homescreen löschen, ohne vorher zu exportieren — damit
  sind auch die Einträge weg.

Als Homescreen-App behält iOS die Daten dauerhaft. Rufst du die Seite nur in
Safari auf, räumt iOS den Speicher nach rund sieben Tagen ohne Nutzung auf.

## Etwas ändern

Inhalt und Logik stehen in `core.html`. Danach:

    python3 build.py

Das schreibt `index.html` neu. Anschließend in `sw.js` die Zeile
`const VERSION = "golf5-v1"` hochzählen, sonst zeigt das iPhone die alte
Fassung aus dem Cache. Dateien neu hochladen, App einmal schließen und öffnen.

## CarPlay

Geht nicht, und zwar nicht aus Faulheit. Apple gibt CarPlay nur für Navigation,
Audio, Kommunikation, Laden, Parken und ein paar Fahraufgaben frei. Ein
Wartungsheft fällt in keine dieser Kategorien und bekommt deshalb auch mit
Entwicklerkonto keine Berechtigung. Was im Auto funktioniert: die App per Siri
Kurzbefehl öffnen oder den Kilometerstand nach dem Abstellen am Handy nachtragen.
