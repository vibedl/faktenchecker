# Faktenchecker (ohne KI)

**Online:** https://vibedl.github.io/faktenchecker/ · **Code:** https://github.com/vibedl/faktenchecker

Eine einfache, rein clientseitige Web-App: Du gibst einen Text ein, sie zerlegt ihn
in einzelne Sätze/Behauptungen und verlinkt jede davon direkt zu:

- Faktencheck-Portalen (Correctiv, ARD Faktenfinder, dpa, Mimikama, APA, Volksverpetzer,
  Google Fact Check Explorer)
- allgemeinen Suchmaschinen (Google, Bing, DuckDuckGo, Wikipedia)
- wissenschaftlichen Quellen (Google Scholar, PubMed)

Es findet **keine KI-Bewertung** statt – die App sammelt nur passende Such-Links,
die Einordnung machst du selbst anhand der Originalquellen.

## Lokal öffnen

Einfach `index.html` im Browser öffnen. Kein Build-Schritt, keine Abhängigkeiten.

## Veröffentlichen
Die App liegt öffentlich im Repo `vibedl/faktenchecker` und läuft über GitHub Pages.
Entwickelt wird weiter im WikiNotebook. Ein neuer Stand geht mit einem Befehl online:
```bash
./projects/fatenchecker/veroeffentlichen.sh "Kurze Beschreibung"
```

## Anpassen

- Weitere Quellen/Portale: `buildSearchLinks()` in `index.html` erweitern.
- Satztrennung verbessern: `splitIntoClaims()` anpassen (aktuell simple Regex-Heuristik,
  kein NLP – bei Abkürzungen, Zahlen mit Punkt o. Ä. kann sie danebenliegen).
- Design: CSS-Variablen im `<style>`-Block oben in der Datei.

## Sicherheit

- Alle Nutzer-Eingaben, KI-Antworten und Quellentitel werden vor der Anzeige escaped
  (`escapeHtml()`) – kein HTML/JS aus Text, der `<`, `>` o. Ä. enthält, wird ausgeführt.
- Links aus KI-Antworten werden geprüft (`safeUrl()`): nur `http(s)://`-Adressen werden
  als klickbarer Link gerendert, alles andere (z. B. `javascript:`-URIs) wird sichtbar
  als ungültig markiert statt verlinkt.
- Ein KI-API-Key verlässt den Browser ausschließlich in Richtung des gewählten Anbieters
  (Google/Anthropic/OpenAI) – kein eigener Server, kein Proxy, keine Analytics.
