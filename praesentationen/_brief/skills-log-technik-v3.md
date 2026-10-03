# Skills-Nachweis: ki-werkzeugkasten-v3.html

Quelltext: `_src/technik-v3/{build.py,prep.py,body.html,style.css,main.js,vault.js,vault-section.html}`. Aufnahmen: `_shots/technik-v3/` (d-00..59 Desktop 1440x900, m-00..59 Mobil 390x844). Nichts davon steht auf den Folien.

## Umsetzung der Owner-Vorgaben
- Verbotsliste geprüft per Playwright (`innerText` der App plus alt/aria-label/title): kein "Beleg", "Quelle", ".png", ".jpg", ".webp", kein Kolophon, keine Chronologie, keine Benchmark-Tabelle, kein eigener Draht-Kopf. Der Einkaufs-Ablauf heißt auf der Folie "Einkauf".
- Logo (Stand 03.10.): die Originalpfade von `dkc-logo-white.svg` (Ring und Kopf, weiß, unverändert). In Ruhe pixelgleich zur Datei (Abgleich per Bildvergleich, nur Kantenglättung weicht ab). Bewegung nur durch Ebenen: `lines.py` leitet aus den Facetten die 112 Linien-Mittellinien ab, vier Masken zeigen je ein Viertel der Originallinien, die Ebenen driften per translateZ/translateX auseinander und kehren exakt zurück. Three.js ist aus dem Deck entfernt.
- Keine Klassen auf html/body, alles hängt an `#app`. (Three.js wurde nach Owner-Rückmeldung zum Logo entfernt.)
- Externe Bildplätze (`prep.py`/`build.py` lesen bei jedem Lauf): `launch/openai/{luna,sol,astra}.*`, `screens/claude-app*`, `screens/nous-hermes*`, `misc/mac-mini*`. Mit Testbildern geprüft, dass jeder Platz greift, danach entfernt. Ohne Datei: typografische Nacht (Ledger-Linien, Umrisswörter), nur Wort "Mac mini", nur Claude Code.
- Bildaufbereitung: Titeltexte aus Fable-, Opus- und Sonnet-Launchbild per Diffusionsfüllung entfernt (`prep.py`), Haiku-Wortmarke freigestellt, Mac Studio freigestellt und in fünf Scheiben zerlegt.
- Vault: echte Daten `assets-real/vault/vault-graph.json` (270 Notizen, 720 Links, Wachstum nach `rank`, Notiztext aus dem README, Em-Dash entfernt, Umschrift ae/ue zu Umlauten). Route durch den Vault per Breitensuche zwischen Donald, plan-current, H6-email-pipeline-plan, KIRA-Codex-Review, E38-vault-ordnerkanon und index.
- Hermes-Schleife nur aus Repo-Doku: MEMORY.md/USER.md (memory), skill_manage, session_search, cron, Curator.

## ui-ux-pro-max
Priorität 1 bis 5 durchgegangen: Kontrast Fließtext (Creme auf Nacht, Tinte auf Haiku-Cremegrund, Navy auf Fable-Himmel), Tastatur (Pfeile, Leertaste, Bild auf/ab, Home/End springen zu Stopps), Punktnavigation 26x22 px Klickfläche, 390 px ohne Horizontal-Scroll, `prefers-reduced-motion`, SVG-Icons statt Emoji.

## hallmark
Stempel im Kopf von style.css. Makrostruktur "Continuous Stage": gepinnte Bühnen mit Bildschichten, bewusst nicht Specimen. Gates: keine Eyebrow-Serie (genau eine Kicker-Klasse, nur in Hermes/Local-Titelzeilen nicht genutzt), keine Karten-Raster, keine kursiven Überschriften (kein Italic-Font eingebettet), Farben und Schriften als Tokens auf `:root`, keine nachgezeichneten Fenster-Rahmen (nur echte Screenshots, die Notiz im Vault ist eine Karte ohne Titelleiste), keine erfundenen Zahlen (alle Zahlen aus Briefs, Storyboard, Vault-Daten).

## scroll-craft
- Grammatik: gepinnte Kapitel mit je eigenem Gerät: Kopf-Rotation (Titel), mehrschichtige Bühne mit Parallaxe und Zoom (Modelle), typografisches Lineal (OpenAI), Token-Kacheln im Kontextfenster, Schaltbilder (CLI/API/MCP), Auto und Motor, Schleife, Porträt-Netz, Kette und Spur, 3D-Zerlegung (Mac Studio), Graph-Kamera (Vault).
- hero-depth: Modellbühnen haben fern (Launch-Bild, langsame Parallaxe und Zoom), Mitte (Modellname, anderer Faktor), nah (Randbilder mit schnellerem Faktor, Aufgaben). Zeiger-Parallaxe nur bei feinem Zeiger.
- feel: Ruhe (Titel), Weite (Himmel, Erde, Sonnenaufgang), Spannung (Preise), Erklärung (Token), Klarheit (CLI/API/MCP), Wärme (Porträts), Verantwortung (Einkauf, Empfang), Ehrlichkeit (Zonen "noch im Aufbau"), Peak: Vault wächst, zoomt, dreht, öffnet eine Notiz und zieht sich zum Kopf zusammen (längstes Kapitel, 1750 svh). Schluss hält mit Logo, Kopf und Adresse.
- Uniqueness: Kapitel wiederholen kein Gerät direkt hintereinander.
- Verifikation: je 60 gleichmäßige Scrollstände Desktop und Mobil, dazu kapitelweise Serien (`chshot.py`). Dabei gefundene Fehler: leere Vorhang-Zustände an Kapitelgrenzen (Vorhang auf 0,32 begrenzt, Inhalte ab p=0 sichtbar), überschriebene Opacity durch `cssText` (Lokal, Karte), Textüberlappung im Empfang und Tagesplan, abgeschnittene Schleifen-Beschriftung.

## build-threejs-scroll-worlds
(Nach der Logo-Korrektur ohne WebGL. Ursprünglich:) Ein Renderer, eine Szene; der Canvas wird in die aktive Bühne umgehängt (Titel, Schluss). Scroll-Zustand deterministisch aus `scrollY` je Kapitel (`p`), keine Wheel-Integration. DPR bei 2 gedeckelt, Resize neu vermessen, Schrift-Ladung löst Neumessung aus. Fallback ohne WebGL: statischer Kopf.

## scroll-scrubbed-word-reveal
Leitsätze der Modellbühnen: TreeWalker zerlegt Textknoten in `.wd`-Spans, Leerraum bleibt erhalten, `aria-label` am Absatz, Spans `aria-hidden`. Fortschritt je Wort aus dem Kapitel-`p`. Bei reduzierter Bewegung sofort sichtbar.

## emil-design-eng und animate
Gate: Alles hängt am Scroll und ist umkehrbar, keine Dauerschleifen. Nur `transform`, `opacity`, `clip-path` (Gold-Rahmen im Terminal), `translate`-Eigenschaft für Eintritte. Kurven `--ease-out`, `--ease-io`. Tastatur-Sprünge ohne Animation bei reduzierter Bewegung. Kein `transition: all`, kein `scale(0)`.

## design-taste-frontend, no-ai-design-slop, impeccable, audit-ai-design-slop
- Kein Gradient-Text, keine Seitenstreifen, keine Glasflächen als Standard, keine Icon-Kachel-Raster, keine Scroll-Hinweise, kein Zähler "01 / 06".
- Palette Petrol, Gold, Creme, Nacht; Obsidian-Dunkel (#161618) nur im Vault, dort mit Obsidian-Violett für Hervorhebungen, weil der Owner die Obsidian-Optik verlangt.
- Entfernt nach Audit: Zusatz-Eyebrows, doppelte Beschriftungen, die Schlagschatten-Fläche hinter dem Fable-Text (sah wie ein Fleck aus), der Titeltext, der den Ring überlappte.
- Offene Punkte: Hintergrundbilder in den dunklen Kapiteln sind weichgezeichnete echte Oberflächen (Cockpit, Terminals) und bewusst zurückhaltend; Tagesplan-Zoom ist moderat, damit der echte Screenshot lesbar bleibt.

## stop-slop und humanizer
Alle Sätze auf Folien kurz, aktiv, ohne "nicht X sondern Y", ohne Dreier-Reflex, ohne Gedankenstrich. Beispiele: "Schnell und günstig. Das kleinste der vier Modelle." "Das Frontier-Modell. Für die härtesten Fälle." Statusaussagen ehrlich: Zonen "noch im Aufbau", Fachagenten "Zuständigkeiten festgelegt, selbstständiges Ausführen im Aufbau".
