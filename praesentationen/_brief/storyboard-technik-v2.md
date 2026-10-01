# Storyboard „KI-Werkzeugkasten“ v2 — echtes Material, keine Konstruktionen

Owner-Kritik an v1 (verbindlich): konstruierte Sonne/Mond/Planetensystem, generische Listen („9 Abläufe“), Skills nicht genutzt.
Regeln v2:
- Keine selbst gezeichneten Sinnbilder für reale Dinge (keine Sonne für Sol, kein Mond für Luna, kein Planetensystem, keine erfundenen Terminals/Chatfenster). Reale Dinge = echte Bilder aus `assets-real/`.
- Nur echte Fakten. Laufende Dinge aus `_brief/praxisarchitektur-real.md`; Modellfakten aus den offiziellen Launch-Bildern/Texten.
- Gestrichen: Planetensystem, Planer/Prüfer-Umlaufbahnen, „9 Abläufe“-Liste, konstruierte Sol-/Luna-/Astra-Szenen, generische Pipeline-Platten, News-Research (nicht praxisweit live).
- OpenAI-Quellen (openai.com, cdn.openai.com) sind in dieser Umgebung per Organisationsrichtlinie gesperrt → für OpenAI KEINE Bilder erfinden; stattdessen Typografie + echte Zahlen + die offizielle Anthropic-Vergleichstabelle, in der GPT-6 Astra steht (`assets-real/launch/anthropic/claude_opus_3.png`).

## Szenen

1. **Titel.** Nacht. Der Logo-Kopf als 3D-Modell (dieselbe Three.js-Geometrie wie im Team-Deck, hier nur Kanten in Gold, leuchtend), dreht sich beim Scrollen. „KI-Werkzeugkasten. Wie wir mit KI arbeiten.“
2. **Zwei Familien, ein Herbst.** Typografische Zeitleiste September 2026 (echte Daten): Fable 5.1 (1.9.), GPT-6 Astra (4.9.), Opus 5.5 (22.9.), GPT-6 Sol + Luna (22.9.), Sonnet 5.5 (28.9.). Zahlen groß, scroll-gescrubbt.
3. **OpenAI, von klein nach groß: Luna → Sol → Astra.** Drei typografische Kapitel (riesige Wortmarke „Luna“, „Sol“, „Astra“ in Creme auf Nacht, Wort-für-Wort-Reveal), je: wofür, Preis pro Mio. Token (Luna 0,10/0,50 $, Sol 2/10 $), Kontext 1,05 Mio. Token, Einsatz bei uns (aus inhalt-technik.md: z. B. Hermes/Donald laufen auf Sol — nur wenn als live belegt). Bei Astra: die echte offizielle Vergleichstabelle (Anthropic, `claude_opus_3.png`) einfliegen, Spalte GPT-6 Astra hervorgehoben (Gold-Rahmen über dem echten Bild, z. B. Business workflows 41,4 %, Agentic scientific research 64,6 %).
4. **Anthropic, von klein nach groß: Haiku → Sonnet → Opus → Fable.** Jede Stufe mit dem ECHTEN Launch-Bild als vollflächiger Hintergrund-Ebene (scroll-craft hero-depth: Bild = ferne Ebene mit langsamer Parallaxe + leichtem Zoom, Titel = mittlere Ebene, Fakten = nahe Ebene):
   - Haiku 4.5: `news_claude-haiku-4-5_2.webp` (offizieller SWE-bench-Chart) bzw. `claude_haiku_*.jpg`.
   - Sonnet 5.5: `claude-sonnet-5-5_10.jpg` (Erde durchs Fenster) + Fakt „30 % schneller, bis 30 % günstiger als Sonnet 5“, 28.9.2026.
   - Opus 5.5: `claude-opus-5-5_10.jpg` (Horizont) + offizielle Tabelle `claude_opus_3.png` (Spalte Opus 5.5) + „auf Fable-5.1-Niveau, 40 % günstiger als Opus 5“, 22.9.2026.
   - Fable 5.1: `claude-fable-and-mythos-5-1_6.jpg` (Himmel/Wolken) + „das fähigste Modell“, 1.9.2026.
   Merksatz am Ende: „Im Zweifel Sonnet. Wenn es knifflig wird Opus. Wenn es kritisch ist Fable.“
5. **So bedient man es.** Echte Oberflächen: Claude Code in VS Code (`assets-real/screens/claude-code-screenshot.png`), Codex CLI (`assets-real/screens/codex-cli-splash.png`), echte CLI-Aufnahmen aus `assets-real/screens/real-cli/` (Claude Code, Codex, Hermes). Kamerafahrt über die echten Screenshots, Gold-Markierung auf der jeweils relevanten Stelle.
6. **Einer plant, der andere prüft.** Echt: Auszüge aus realen Review-Dokumenten (z. B. `KIRA-Codex-Review-2026-06-01.md`, `ANTWORT-AN-OPUS-GESAMTREVIEW-2026-09-25.md` in SharePoint; Zitate kurz, 0-PID) als zwei echte Dokument-Ausschnitte nebeneinander: Plan links, Befunde rechts, dann Antwort. Kein Orbit.
7. **CLI, API, MCP — mit unseren echten Beispielen.** CLI = echter Terminal-Screenshot. API = echte Schnittstellen der Praxis (SoftDent nur lesend, Wawibox-Export) als nüchterne Zeile. MCP = die tatsächlich verbundenen Connectoren (Gmail, Google Kalender, Google Drive, Microsoft 365, Fireflies, PubMed, PDF Viewer) als echte Namensliste, die beim Scrollen „einrastet“. Kurz und präzise.
8. **Was heute automatisch läuft.** Nur LIVE aus praxisarchitektur-real.md: Belege (Hermes-Cron täglich 08:00, Monatsabschluss am 1. mit Excel/BMD-CSV/ZIP/Mail-Entwurf an die Steuerberaterin, Vincent prüft und sendet), Cockpit-Tagesplan 08:00, Empfang (Mail-Triage, Schmerz-Alarm, Draft Builder, soweit live). Darstellung: echte Dateinamen/Artefakte wandern, keine Platten.
9. **Hermes-Agenten (Wiring — vom Owner gelobt).** Echtes Hermes-Agent-Logo/Banner (`hermes-banner.png`) + echte CLI-Aufnahme; das Agenten-Netz mit echten Porträts (`assets-real/agents/`, inkl. Ivan, keine Patricia), Donald Mitte, wandernde Impulse. Ehrliche Formulierung zum Status aus praxisarchitektur-real.md.
10. **Lokale Modelle & Zonen.** Echtes Mac-Studio-Foto (`assets-real/misc/mac-studio.jpg`) + echte Modellliste (qwen3.6:35b, ornith, qwen2.5-coder:32b, gemma4:26b, whisper-large-v2, bge-m3); Zone A ohne Internet, Zone B online 0-PID, Export-Broker. Status ehrlich („im Aufbau“), sehr knapp.
11. **Agentic OS (Owner: „muss viel besser dargestellt werden“).** Die echten Workflow-Diagramme aus dem agentic-os-Repo (`assets-real/agentic-os/orchestration-dark.png`, `overnight-loop-dark.png`): Kamera fährt den Kreislauf Knoten für Knoten ab (Auftrag → Root → Parent-Check → Fable → Kanonisieren → Rebuild → Recall), je 1 Satz aus den 10 Fakten (README/PLAN/STATUS). Dann Übergang: „Rebuild → Graph“ öffnet das echte Obsidian (`assets-real/screens/obsidian-graph.png`), daraus wird der echte Graph live in 3D (`assets-real/graph/graph-data.json`; 2171 Knoten, 2519 Kanten, 188 Gruppen), rotiert am Scroll, Knoten öffnen sich mit echten Labels.
12. **Schluss.** Der Graph zieht sich in den 3D-Logo-Kopf zusammen. Drei Sätze, wie wir arbeiten. office@diekieferchirurgen.at.

## Skill-Pflicht mit Nachweis
`_brief/skills-log-technik.md` wie beim Team-Deck: pro Skill zitierte Regel → Szene/Codestelle; Hallmark-Stempel + Slop-Test-Protokoll; scroll-craft Fingerprint + Feel-Kurve; audit-ai-design-slop Befunde + Fixes. Muss sich in der Grammatik klar vom Team-Deck unterscheiden (uniqueness.md).
