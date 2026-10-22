# klaviyo-content

Texte für Schlafgut-E-Mails in Klaviyo. Klaviyo liest `snippets.json` als Web Feed ein, die Templates holen sich die Werte daraus.

> **Dieses Repo ist öffentlich.** Jeder im Internet kann es lesen. Hier kommen nur Marketing-Texte rein, die sowieso in E-Mails landen — keine internen Infos, keine Preise vor dem Launch, keine Kundendaten, keine Zugangsdaten.

## Texte ändern (ohne Git, ohne Terminal)

GitHub im Browser öffnen → `snippets.json` → Stift-Icon → Text ändern → **Commit changes** → grünen Haken abwarten. Fertig.

Roter Haken = die Datei ist kein gültiges JSON mehr (meist ein fehlendes oder überzähliges Komma bzw. Anführungszeichen). Dann sofort korrigieren: Klaviyo zieht trotzdem den letzten Stand von `main`, auch wenn er kaputt ist.

## Regeln

- **Keys nie umbenennen.** `willkommen_01`, `headline`, `text` usw. werden in den Klaviyo-Templates verwendet. Umbenennen = leere Stellen in der Mail. Nur die Werte rechts vom Doppelpunkt ändern.
- **Neues Snippet = neuer Key.** Einen bestehenden Block kopieren, neuen Namen vergeben (klein, mit Unterstrich, z. B. `warenkorb_01`).
- **HTML ist erlaubt** (`<b>`, `<br>`, `<a href="…">`). Anführungszeichen im Text als `\"` schreiben oder typografische „…" verwenden.
- Änderungen sind nach **bis zu ~5 Minuten** in Klaviyo sichtbar (GitHub-Cache).

## Einbindung in Klaviyo

Feed-URL (Raw):

```
https://raw.githubusercontent.com/schlafgut/klaviyo-content/main/snippets.json
```

Klaviyo → Settings → **Web Feeds** → *Add web feed* (falls der Menüpfad anders ist: in der Klaviyo-Suche „web feed" eingeben)

| Feld | Wert |
|---|---|
| Feed name | `snippets` (wird zum Variablennamen) |
| URL | Raw-URL oben |
| Request method | GET |
| Content type | JSON |
| Auth | keine |

Im E-Mail-Template:

```
{{ feeds.snippets.willkommen_01.headline }}
{{ feeds.snippets.willkommen_01.text }}
<a href="{{ feeds.snippets.willkommen_01.cta_url }}">{{ feeds.snippets.willkommen_01.cta_text }}</a>
```

Die Vorschau in Klaviyo zeigt die Live-Werte — damit testen, bevor ein Flow live geht.

## Später: pro Flow aufteilen

Wenn `snippets.json` zu groß wird, pro Flow eine Datei anlegen (`welcome.json`, `cart.json`, …). Jede Datei ist dann ein eigener Web Feed in Klaviyo (z. B. Feed name `welcome`). Die JSON-Prüfung deckt automatisch alle `*.json`-Dateien ab.
