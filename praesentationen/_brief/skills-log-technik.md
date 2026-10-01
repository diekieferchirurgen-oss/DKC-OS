# Skills-Nachweis: ki-werkzeugkasten-v2.html

Quellcode: `_src/technik-v2/{build.py,body.html,style.css,main.js,graphprep.py}`. Aufnahmen: `_shots/technik-v2/`.

## Hallmark
- Stempel (Kopf von style.css): `Chaptered Editorial · custom "Beleg-Nacht" · EB Garamond + Jost · nav: Folio + Belegzeile + Index (I) · pre-emit critique: P5 H4 E4 S5 R4 V5`.
- Regel "Pick a macrostructure FIRST / diversification": Team-Deck = Continuous World. Dieses Deck = Chaptered Editorial (harte Grundwechsel Nacht, Creme, Petrol pro Kapitel, Folio statt Fortschrittsleiste, Beleg-Kolophon am Ende).
- Gate 38a "no italic headers": alle Überschriften roman. Gate 46 "no fabricated content": alle Zahlen aus Anthropic-Tabellen, Briefs, Review-Dokumenten. Gate 47 "re-drawn chrome forbidden": keine nachgezeichneten Fenster, nur echte Screenshots. Gate 48 "locked tokens": Farben und Schriften als `--petrol/--gold/--serif` auf `:root`. Gate 54 "tag left/heading right": nirgends, Überschriften stehen immer über dem Text.
- Slop-Protokoll: Eyebrows 0; Section-Nummern nur im Folio (Navigation); keine Cards (Dokument-Blätter in Szene 6 sind echte Auszüge); kein Gradient-Text; keine Seitenstreifen-Rahmen; Reduced-Motion und 390px geprüft.

## scroll-craft
- Grammatik (uniqueness.md §2.2 "Chaptered editorial") gewählt. Warum nicht die anderen sieben: Continuous world gehört dem Team-Deck, Filmic one-shot braucht Video (verboten), Live surface würde Oberflächen nachbauen (verboten), Poster/Gallery/Split/Cutlist passen nicht zu 12 belegten Kapiteln.
- Fingerprint gegen Team-Deck (Continuous World, Rand-Fortschrittsleiste, Iris-Kopfflug, kein Folio): Grammatik, Nav (Folio + Belegzeile gegen Edge-Rail), Hero (3D-Gitterkopf bei Nacht + Wortmarke statt Flug), Close (Gitterkopf plus Ring, Kolophon), Signature Move verschieden = 5 von 6 Dimensionen.
- Signature Move "Beleg-Rahmen": ein Goldrahmen zeichnet sich Kante für Kante über die exakte echte Zelle oder Zeile im echten Bild (Astra-Spalte, Haiku-Balken, `mcp`-Zeile in `codex --help`), die Belegzeile unten links nennt die Quelldatei. Kamera über echten Bildern: `data-cam` Keyframes, Plate wird skaliert und verschoben (`applyCam` in main.js).
- feel.md Kurve: Ruhe (Titel) → Überblick (Zeitleiste) → Spannung (OpenAI-Zahlen) → Weite (Anthropic-Himmel, Merksatz) → Nähe (Terminals) → Vertrauen (Review-Zitate) → Klarheit (CLI/API/MCP) → Verantwortung (läuft heute) → Wärme (Agenten) → Ehrlichkeit (lokal) → Staunen (Kreislauf) → Peak: Obsidian-Screenshot wird zum rotierenden Live-Graphen und zieht sich zum Gitterkopf zusammen (größte Strecke, 1100vh) → Ruhe (Schluss hält).
- Tell-someone: "Es ist die Präsentation, in der der echte Obsidian-Graph unseres Vaults aus dem Screenshot aufspringt, sich dreht und am Ende zum Logo-Kopf wird."
- hero-depth: je Szene fern (Launch-Art/Ghost-Wort mit `--par`), mittel (Titel), nah (Fakten, Goldrahmen, Karte). Pointer-Parallax auf Desktop.

## ui-ux-pro-max
- Pre-Delivery: Kontrast Fließtext ≥4.5:1 (Creme auf Nacht, Tinte auf Creme, Folio-Farbe wechselt mit Grund), Touch-Ziele Folio und Index ≥44px, Tastatur (Pfeile, Leertaste, I, P, Esc), `prefers-reduced-motion`, 390px ohne Horizontal-Scroll, SVG statt Emoji.

## build-threejs-scroll-worlds / scroll-world-storytelling
- "One persistent renderer": ein WebGLRenderer, eine Szene, `world`-Gruppe mit Kopf und Graph (main.js `initGL`). Scroll-Zustand deterministisch aus `scrollY` (`updateChapter`), geglättet nur für Render (`frame`, exp-Dämpfung). Tiefenfarbe und Punktgröße nach Kameraabstand. Fallback: SVG-Kopf aus denselben Polygonen (`.fallback-head`), DPR ≤2, pausiert bei `document.hidden`. Three.js 0.169.0 per `npm pack`, inline als Blob-Modul.
- Kopfgeometrie: Polygone aus `assets/dkc-logo-white.svg`, Silhouetten-Breakpoints (RDP) als Querschnittsebenen, Ellipsen-Sweep mit 18 Segmenten, Kanten Gold, Fläche Nachtpetrol.
- Graph: `graphprep.py` nimmt die 774 Knoten mit höchstem Grad aus `graph-data.json` (1214 Kanten, echte Labels), 3D-Force-Layout, Scroll dreht die Hubs nacheinander in den Fokus, Karte zeigt echtes Label, Dateipfad und Grad. Hover öffnet Knoten (Desktop).

## scroll-scrubbed-word-reveal
- `[data-words]` per TreeWalker in `<span class="wd">`, Fortschritt je Wort (`--o`), Reduced-Motion zeigt alles. Eingesetzt: Titel-Aussage, Luna/Sol/Astra, Schluss.

## emil-design-eng + animate
- Kurven `--out: cubic-bezier(.23,1,.32,1)` und `--inout`; nur `transform`/`opacity`/`clip-path`; keine Animation auf Tastatursprüngen außer Scroll; Folio-Farbwechsel 200ms; Reveal sichtbar-by-default (Gold-Rahmen, Ghost-Wörter ohne Layout).

## design-taste-frontend / no-ai-design-slop / impeccable
- "Eyebrow max 1 per 3 sections": null. "No scroll cue": keine. "No fake product UI": nur echte Screenshots. "Cream/sand body bg": Creme ist hier Markenfarbe (#F5F0E8 laut Brief), nur auf zwei von zwölf Kapiteln. "Hero-metric template": Preiszahlen in Szene 3 sind echte Presseangaben ohne Gradient und ohne Kachel.
- Absolute Bans geprüft: Gradient-Text, Seitenstreifen, Glas, identische Card-Raster: keiner.

## stop-slop + humanizer
- Jeder sichtbare Satz geprüft; Befunde und Umschreibungen u.a.: "Zwölf Szenen, ein Prinzip: …" (Staging) → "Alles in diesem Deck ist belegt. Unter jedem Bild steht, aus welcher Datei es stammt."; "Nicht der Chat, sondern …"-Konstruktionen nicht verwendet; "dafür für den Ernstfall" → "gedacht für den Ernstfall"; "Nichts bleibt im Gedächtnis hängen" → "Das spart Kontext, setzt aber ein lokal installiertes Programm voraus."; "Derselbe Gedanke, jetzt gerechnet" (Sinnspruch) → "Der Graph, gerechnet aus echten Daten."; keine Gedankenstriche, keine Dreierreflexe.

## audit-ai-design-slop (Screenshots `_shots/technik-v2/`)
| Prio | Befund | Fix |
|---|---|---|
| P1 | Szene 11 Loop: Text "Readback." und Statuszeile überlagern sich (d-aos-097) | `data-out` am Readback-Absatz, Statuszeile erst danach |
| P1 | Szene 8 mobil: Ablauf-Ketten überlagern sich (m-laeuft) | Lanes absolut übereinander mit eigenem Aus-Fenster, Kette senkrecht |
| P2 | Szene 4 Haiku: abgeschnittener Schriftzug "Claude Hai…" der Launch-Art wirkt wie Fehler | Deckkraft auf .14 gesenkt |
| P2 | Szene 12: Graph-Labels überlappten sich, Kopf zu klein im Ring | Kollisionsprüfung der Labels, Skalierung angepasst |
| P2 | Szene 2: Ereignisspalten kollidierten am rechten Rand (Opus/Sol, Sonnet) | schmalere Spalten, Cursor-Chip dreht am Ende nach links |
| P3 | Folio unlesbar auf hellen Anthropic-Bildern (Haiku, Fable) | Marken `|L` je Stufe schalten Chrome auf Tinte |

## Offene Punkte (ehrlich)
- Nicht auf echtem Smartphone getestet. Mobile Kamerafahrten über Bildschirmfotos (Szene 5, 7) nur in Screenshots geprüft, nicht jede Mikro-Position.
- Anthropic-Launch-Bilder `claude-sonnet-5-5_10.jpg` (1200px) in der Fenster-Szene kleiner als 1920px; die Vollbild-Ferne nutzt 1920px-Alternativen (`sonnet-5-5_8`, `opus-5-5_7`, `fable-and-mythos-5-1_6` auf 1920 hochskaliert, Original 1200).
- Faktenstand OpenAI nur aus Presse (Brief), Zeile "Astra schrieb die Antwort" folgt dem Dokumentkopf "Von: Astra / Codex".
