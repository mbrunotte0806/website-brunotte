# brunotte.de

Persoenliche Website von Malte Brunotte. Eine statische Seite, von Hand
geschrieben, ohne Framework und ohne Bauschritt: Was im Repository liegt,
ist genau das, was der Server ausliefert.

## Zweck

Rueckendeckung fuer die Grunwald GmbH, kein Verkaufskanal. Wer den Namen
Brunotte sucht, soll hier landen; wer eine Flaechenheizung sucht, auf
grunwald-gmbh.com. Deshalb bewusst keine Leistungs-SEO und kein Vertriebston.

## Veroeffentlichungsregel

**Alles, was im Repository liegt, geht live.** Die Entscheidung faellt
einmal in der `.gitignore`, nicht beim Hochladen.

Daraus folgt die Ordnerkonvention fuer alles, was NICHT auf die Website soll:

| Ordner       | Inhalt                                               |
|--------------|------------------------------------------------------|
| `notizen/`   | Arbeitsmaterial, Zwischenstaende, Recherche          |
| `dokumente/` | fertige Dokumente fuer Malte (PDFs, Analysen)        |

Beide sind pauschal ignoriert. Neue interne Dateien gehoeren dorthin - dann
ist nichts einzutragen. Nur eine lose Einzeldatei in der Wurzel braucht einen
eigenen `.gitignore`-Eintrag, und der ist vor dem naechsten Commit zu setzen.

Pruefen: `git status --short` zeigt, was veroeffentlicht wuerde.

## Veroeffentlichen

Hosting: STRATO-Webspace, Verzeichnis `/brunotte.de`. Uebertragung per
GitHub-Action `.github/workflows/deploy-strato.yml`, nur manuell ausloesbar
(Actions -> "Auf STRATO veroeffentlichen" -> Run workflow):

- `auflisten` - zeigt nur, was auf dem Server liegt. Aendert nichts.
- `hochladen` - spiegelt das Repository in das Zielverzeichnis. Loescht nichts.
- `aufraeumen` - einmaliges Aufraeumen der Wurzel, normalerweise nicht noetig.

Ein Push nach GitHub veroeffentlicht also noch nichts. Nach jedem `hochladen`
die Live-Seite pruefen, nicht nur das Protokoll des Laufs.

Die `--exclude-glob`-Zeilen im Workflow sind der zweite Filter: fuer Dateien,
die zwar ins Repository gehoeren, aber nicht auf den Server (`.github/`,
`.gitignore`, `CLAUDE.md`, `vercel.json`). Fuer ignorierte Dateien braucht es
sie nicht - die erreichen den Server ohnehin nie.

## Technik, kurz

- `index.html` traegt die gesamte Startseite samt Stil im `<style>`-Block.
- `impressum.html` und `datenschutz.html` teilen sich `recht.css`. Die
  Farbwerte und die Schrifteinbindung dort sind mit `index.html` gleichzuhalten.
- Schrift Hanken Grotesk liegt lokal unter `fonts/` - kein Google Fonts,
  kein Aufruf an Dritte beim Laden der Seite. Das steht so auch in der
  Datenschutzerklaerung und darf nicht stillschweigend aufgeweicht werden.
- Keine Cookies, kein Tracking, keine eingebundenen Dienste. Jede Aenderung
  daran zieht eine Aenderung der Datenschutzerklaerung nach sich.
- `.htaccess` regelt https-Zwang (ueber `SERVER_PORT`, nicht `%{HTTPS}`),
  Weiterleitung auf www, HSTS und Cache-Dauer.
- Deutsche Typografie: `text-wrap: pretty`, feste Zeilenbreiten
  (`--measure`), weiche Trennstriche in langen Komposita.

## Texte

Sachlich, in der ersten Person, ohne Werbesprache. Keine Floskeln
("individuelle Loesungen"), kein Prahlen mit Zertifikaten, keine Behauptung,
die nicht belegt ist. Fachliche Aussagen - besonders im Abschnitt
"Standpunkt" - muessen einer Rueckfrage vom Fach standhalten.

Textaenderungen immer wortgenau nach Maltes Vorgabe uebernehmen; Vorschlaege
davor unterbreiten, nicht danach.
