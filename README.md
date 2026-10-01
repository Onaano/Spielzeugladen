# 🧸 Spielzeugladen — Rechnen mit Geld

Ein Lernspiel zum Umgang mit Euro und Cent: Münzen und Scheine erkennen,
Beträge zusammenzählen, passend bezahlen, vergleichen und Wechselgeld
berechnen — verpackt als kleiner, freundlich illustrierter Spielzeugladen.

**Zielgruppe:** Grundschule
**Status:** Version 1.0

## 🎮 Die acht Modi

1. **Münzen** — Euro-Münzen, Cent-Münzen oder alle gemischt erkennen und zusammenzählen
2. **Scheine** — 5/10/20/50-€-Scheine erkennen und zusammenzählen
3. **Scheine & Münzen** — gemischte Beträge bestimmen (ganze Euro oder Euro & Cent)
4. **Bezahle passend!** — das Kind legt den Preis frei aus Münzen und Scheinen;
   **jede** mathematisch korrekte Kombination wird akzeptiert (z. B. 4 € als
   2+2, 2+1+1 oder 1+1+1+1)
5. **Einkaufskorb** — Preise mehrerer Spielzeuge addieren
6. **Reicht dein Geld?** — Budget mit Einkauf vergleichen (Ja/Nein), mit
   ausgewogener Mischung aus „reicht genau", „reicht mit Rest" und „reicht nicht"
7. **Wechselgeld** — Rückgeld berechnen; der Bezahlbetrag ist immer ≥ Preis
8. **Einkaufsauftrag** — zwei Spielzeuge finden, die eine Bedingung erfüllen
   (Budget einhalten oder exakte Summe treffen); **jede** gültige Kombination
   wird akzeptiert, nicht nur eine vorher festgelegte

Jeweils mit Unterauswahl „Ganze Euro" / „Euro & Cent" wo sinnvoll.

Eine Runde besteht aus 8 richtig gelösten Aufgaben (nicht 8 Versuche),
sichtbar als Einkaufskörbe in der Fortschrittsanzeige. Keine Zeitbegrenzung,
kein Punktabzug, kein Game Over — bei einer falschen Antwort bleibt die
Aufgabe bestehen und es gibt einen freundlichen Hinweis.

## 🛠️ Technik

Eine einzige, in sich geschlossene `index.html`-Datei — kein Build-Prozess,
keine Abhängigkeiten, kein Server nötig.

- Reines HTML, CSS und JavaScript (kein Framework)
- **Alle Geldbeträge werden ausschließlich in ganzen Cent-Werten berechnet**
  (nie mit Fließkommazahlen) — `centsToEuroString()`, `sumMoney()` als
  zentrale Hilfsfunktionen, deutsche Schreibweise (`3,50 €`, nicht `3.50 €`)
- Münzen und Scheine sowie alle acht Spielzeuge (Ball, Teddy, Auto, Puzzle,
  Springseil, Bauklötze, Roboter, Zug) als eigene SVG-Illustrationen, keine
  externen Bilder oder Emojis als Hauptgrafik
- **„Bezahle passend!" und „Einkaufsauftrag" prüfen ausschließlich die
  Summe**, nie eine vorher festgelegte Kombination — jede rechnerisch
  richtige Lösung wird akzeptiert
- Distraktoren bei Multiple-Choice-Aufgaben werden über eine enge und eine
  breitere Rückfall-Suche erzeugt, geprüft auf Eindeutigkeit und auf
  „enthält garantiert die richtige Antwort"
- Einkaufsaufträge werden vor der Anzeige darauf geprüft, dass mindestens
  eine gültige Lösung unter den angezeigten Spielzeugen existiert
- Sprachausgabe optional über den Lautsprecher-Button (native
  `SpeechSynthesis`-API), rein manuell, kein automatisches Vorlesen
- Sicherheitsnetz: löst sich ein interner Sperr-Zustand durch einen
  unerwarteten Fehler nicht rechtzeitig, wird er automatisch freigegeben
- Läuft vollständig offline, keine externen Ressourcen, keine Cookies,
  kein Tracking
- Responsiv für Smartboard, Desktop, Tablet und Smartphone

## 📁 Projektstruktur

```
spielzeugladen-projekt/
├── index.html      ← das komplette Spiel
├── README.md
└── .gitignore
```

## ▶️ Lokal ausprobieren

Einfach `index.html` im Browser öffnen — kein Server, keine Installation
nötig.

## 🌐 Veröffentlichung

### GitHub
1. Neues Repository auf [github.com](https://github.com) anlegen.
2. `index.html`, `README.md` und `.gitignore` hochladen.

### Netlify (per Drag & Drop)
1. Auf [app.netlify.com](https://app.netlify.com) einloggen.
2. Den Projektordner direkt in den Browser ziehen („Deploy manually").
3. Netlify vergibt sofort einen Link. Build command: leer, Publish
   directory: `.`

## ✅ Qualitätssicherung

- Alle in der Spezifikation genannten Testfälle (Abschnitt 21) einzeln
  nachgerechnet: Münzen, Scheine, Scheine & Münzen, Wechselgeld — alle korrekt
- **„Bezahle passend!" explizit mit mehreren unterschiedlichen gültigen
  Kombinationen für denselben Preis getestet** (z. B. 4 € sowohl als 2+2 als
  auch als 2+1+1), sowie zu viel/zu wenig Geld korrekt abgelehnt, Münze durch
  erneutes Antippen im Tresen entfernbar
- Über 80 automatisiert erzeugte Aufgaben je Modus/Unterauswahl geprüft:
  0 Fehler bei Summen, Distraktor-Eindeutigkeit, korrekter Antwort in den
  Optionen und (bei „Reicht dein Geld?") ausgewogener Verteilung der drei
  Szenarien
- Alle 15 Modus/Unterauswahl-Kombinationen als volle Runde (8/8) mit echten
  Klicks durchgespielt
- Einkaufsauftrag: garantierte Lösbarkeit vor jeder Aufgabe geprüft
- Navigationsfluss getestet: Start → Unterauswahl → Spiel → Zurück, sowie
  Modi ohne Unterauswahl (Scheine, Einkaufsauftrag) starten direkt
- Alle 6 vorgeschriebenen Bildschirmgrößen (375×667 bis 1920×1080) geprüft:
  kein horizontales Scrollen, alle Geldwerte und Buttons vollständig sichtbar

## 📄 Lizenz

© Förderfreude Games. Alle Rechte vorbehalten.
