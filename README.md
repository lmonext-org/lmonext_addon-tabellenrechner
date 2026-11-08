# tabellenrechner (LMOnext-Addon)

Was-wäre-wenn-Rechner für [LMOnext](https://github.com/lmonext-org/core): Ergebnisse eines Spieltags in der Tabelle simulieren, ohne sie zu speichern - die geänderte Tabelle erscheint sofort live.

## Was das Addon zeigt

- **Aktuelle Tabelle** der gewählten Liga inklusive Spalten-Layout der Sportart (Tendenz, Wertungsspalten bei Kegeln, Zusatzspalten u.v.m.)
- **Was-wäre-wenn-Simulation**: Ergebnisfelder der Partien frei überschreiben - die Tabelle rechnet sofort neu, ohne dass ein Ergebnis gespeichert wird
- **Spieltag-Navigation**: zum Durchblättern der Spieltage; Simulationen bleiben je Spieltag aktiv
- **Reset**: alle Overrides auf einmal zurücksetzen (tatsächliche Ergebnisse)

## Eigenschaften

- **Reine Darstellung**: speichert nichts - alle Overrides leben nur im Browser-Request der Neuberechnung und faden beim Neuladen weg
- **CSRF-geschützt**: die Neuberechnung läuft als POST mit CSRF-Token über den zentralen Addon-Controller; Anfragen ohne Token werden abgewiesen
- **Extern einbettbar**: per iframe oder PHP-include über den zentralen Standalone-Controller
- **Eigene Templates**: Darstellung liegt im Template-Ordner des Addons (`templates/standard.tpl.php`), Template-Auswahl via URL-Parameter

## Voraussetzungen

- LMOnext ≥ `min_core_version` (siehe `addon.json`)
- PHP 8.2+

## Installation

Entweder über Administrator → Erweiterungen → Store/Katalog bzw. ZIP-Upload des Addon-Ordners, oder direkt aus dem eigenen GitHub-Repository: die Installations-URL `https://github.com/lmonext-org/lmonext_addon-tabellenrechner` installiert den neuesten Release des Addons (jedes Addon hat sein eigenes Repo mit eigenen Tags/Releases).

## Externe Einbettung

Per iframe (empfohlen, keine PHP-Abhängigkeit auf der Zielseite):

```html
<iframe src="https://DEINE-LIGA-URL/addon-run.php?addon=tabellenrechner&file=lmo-tabellenrechner.php&tr_liga=3"
        style="border:0;width:100%;height:640px"></iframe>
```

URL-Parameter:

| Parameter | Bedeutung |
|---|---|
| `tr_liga` | Liga-ID (erforderlich) |
| `tr_nr` | Spieltag-Nummer (0 = neuester Spieltag mit Ergebnissen) |
| `tr_template` | Template-Name (Standard: `standard`) |

Kein Liga-Einbettungs-Shortcode: bei fehlender/ungültiger Liga-ID bleibt die Ausgabe leer statt mit einer Fehlermeldung die Fremdseite zu füllen.
