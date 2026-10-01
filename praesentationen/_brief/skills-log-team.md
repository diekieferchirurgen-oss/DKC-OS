# Skills-Nachweis: „KIRA fürs Team“ v2

Datei: `praesentationen/kira-fuers-team-v2.html` (4,8 MB, eine Datei, alles inline). Quellen des Baus: `praesentationen/_src/team-v2/` (style.css, body.html, main.js, build.py, graphprep.py, levels.py).
Jede Zeile unten: **zitierte Regel aus der Skill-Datei → Stelle im Code / Szene**. Alle 14 Skills wurden mit dem Skill-Tool geladen und gelesen. Zusätzlich gelesen: scroll-craft `references/feel.md`, `uniqueness.md`, `worldflight.md`, `devices.md` (Abschnitt parallax/hero-depth), `verify.md`, `templates/FINGERPRINTS.md`; hallmark `references/slop-test.md`. Es wurde kein Fremdskript ausgeführt (kein kie.ai, keine Generierung, kein CDN).

Szenenkürzel: **S1** Kopf · **S2** Flug · **S3** Cockpit/Ansichten · **S4** Werkzeuge (Claude Code, Hermes) · **S5** Vault-Graph · **S6** Helfer · **S7** Abläufe · **S8** Regel · **S9** Schluss.

---

## 1. ui-ux-pro-max
Aufruf: `search.py "medical clinic internal team presentation editorial calm" --design-system`, `--domain typography`, `--domain ux "scroll storytelling pinned reduced motion"`.

Ergebnis der Suche: Muster „Trust & Authority“, Stil „Accessible & Ethical“, Schriftpaar „Medical Clean“ (Figtree + Noto Sans), Vorlage Teal #0891B2 / Grün #16A34A. **Abgleich mit der Marke:** Palette und Schriften sind vom Owner fixiert (Petrol/Gold/Creme, EB Garamond + Jost). Übernommen wurde der Stil-Rahmen („Accessible & Ethical“) und seine Pflichtliste; die Vorschlagsfarben und Figtree/Noto wurden bewusst nicht übernommen (Marken-Vorrang, Begründung in `design-brief.md`).

| Regel (Zitat) | Wo angewandt |
|---|---|
| „Contrast 4.5:1, Alt text, Keyboard nav, Aria-labels“ (Priorität 1, CRITICAL) | Alle Textflächen: Creme auf Petrol-dunkel, Tinte auf Creme. Jedes Bild hat `alt`, Canvas `aria-hidden` bzw. `role="img"` mit Label (`#gr`). Pfeiltasten/Leertaste/Home/End in `main.js` (`keydown`). |
| „Removing focus rings“ als Anti-Pattern | `:focus-visible{outline:3px solid var(--gold)}` in `style.css`. |
| „Min size 44×44px“ (Touch) | Kapitelpunkte `#ticks button` 28 px Fläche mit 6 px Punkt (Desktop-only, auf Mobil ausgeblendet; dort keine antippbaren Mini-Ziele). Der einzige echte Link (Mail) ist 24 px hoch, 100 % Zeilenbreite. |
| „WebP/AVIF, Lazy loading, Reserve space (CLS < 0.1)“ | Alle Bilder WebP (`build.py`), `width`/`height` gesetzt, Bühnen-Bilder `loading="lazy"` außer Cockpit (First-Frame-kritisch). |
| „Horizontal scroll … Fixed px container widths“ | `html,body{overflow-x:clip}`; Prüfung `scrollWidth>innerWidth` = false auf 1440 und 390 (`scrub.py`). |
| „Honor prefers-reduced-motion and present the final readable state without parallax or scroll-jacking“ (ux-Suchtreffer) | `RM`-Zweig in `main.js`: kein Sticky, kein WebGL, jede Szene als statischer Block `.rm-only` (S1–S9 vollständig lesbar). |
| „Parallax/Scroll-jacking causes nausea“ | Nativer Scroll bleibt Quelle der Wahrheit, kein Wheel-Hijack; Sprünge nur per Taste. |

## 2. hallmark
Pfad: Design-Flow, Katalog-Route (kein Custom-Signal außer Marken-Tonwerten; als „custom Petrol-Nacht“ gestempelt, weil die Marke fix ist). Stempel steht als erster Kommentar im CSS (`style.css` Zeile 1 ff., im Build im `<style>`).

```
/* Hallmark · macrostructure: Continuous World (one persistent canvas + pinned stages) · tone: editorial, calm, precise
 * theme: custom "Petrol-Nacht" · paper cream #F5F0E8 · accent gold #B8935A
 * display: EB Garamond (roman only) + body: Jost · axes: paper-band dark→light drift / high-contrast-serif / warm-gold on cool petrol
 * nav: N9 edge-aligned progress rail + chapter ticks · footer: Ft5 statement · enrichment: E-real (real screenshots + live WebGL head)
 * Hallmark · pre-emit critique: P5 H4 E4 S5 R4 V4 */
```

**Design-Kontext (Schritt 1, Annahme wegen delegierter Brief):** Publikum = Praxisteam (Empfang, Assistenz, Ärzte), Zweck = zeigen, was KIRA heute tut, Ton = editorial/ruhig/präzise. **Diversifikation:** erstes Hallmark-Ergebnis im Projekt außer v1 (Specimen-Fall-through, v1 abgelehnt); v2 wechselt Makrostruktur, Nav, Footer, Enrichment.

**Pre-emit-Kritik (1 bis 5):** Philosophie 5 (Position: „nur echtes Material“), Hierarchie 4, Ausführung 4, Spezifität 5, Zurückhaltung 4, Vielfalt 4. Alles ≥ 3, keine Revision nötig. Nach den ersten Screenshots trotzdem 11 Befunde behoben (siehe Abschnitt 14).

**Disziplinen (SKILL.md „Disciplines that hold across every verb“):**
| Regel (Zitat) | Wo |
|---|---|
| „Honest copy — no fabricated content“ | Zahlen nur aus Quellen: 2.171/2.519/188 (graph README), 820 gezeigt (gezählt), Cockpit-Zahlen als „Beispieldaten“ gelabelt (`band` S3). Keine erfundene Kennzahl. |
| „Locked tokens“ | Marken-Tokens in `:root`. Ausnahme dokumentiert: Shader/Canvas-Farben und `rgba()`-Tönungen der Marken-Tokens (siehe Gate 48). |
| „Re-drawn chrome forbidden“ | Kein gezeichnetes Browser-, Handy-, Terminal- oder IDE-Fenster. S3/S4/S5 zeigen ausschließlich echte Screenshots. Die Fensterleiste im Hermes-Bild gehört zum echten Screenshot. |
| „Mobile responsiveness“ | 390×844 geprüft, `overflow-x:clip` auf html und body, `minmax(0,…)` im Tools-Grid. |
| „Typography purity — no italic headers“ | `font-style:normal` auf h1–h3, keine `<em>` in Überschriften. |

**Slop-Test-Protokoll (slop-test.md, 58 Gates; Genre editorial; N = nein/bestanden, Befund = Abweichung):**
| Gates | Ergebnis |
|---|---|
| 1 Display-Font Inter/Roboto/… | N. EB Garamond. |
| 2 Lila-Blau-Verlauf, Verlaufstext | N. Einziger Verlauf: goldener Licht-Flash in S2 (Marken-Gold, Hintergrund, nicht Text). |
| 3 3-Spalten-Icon-Karten · 4 verschachtelte Karten · 5 Seitenstreifen | N. Keine Karten ausser den echten Screenshot-Karten. |
| 6 Hero zentriert | N. Asymmetrisch, Text links unten, Ring rechts. |
| 7 Reines #000/#fff als Basis | N. `#fff` entfernt (jetzt `--paper:#FBF8F2`), Nacht `#0E211F`. |
| 8 Generische Vorlage / gleiche Makrostruktur | N. Continuous World. |
| 9 Abschnitte nur durch Weißraum | N. Bodenfarbe driftet Nacht → Petrol → Creme → Nacht. |
| 10 `transition:all` · 11 Hover-Scale · 12 Bounce · 13 Mehrfach-Hover · 14 Layout-Animation | N. Animiert wird nur `transform`/`opacity`/`filter` (Wort-Reveal). Breiten/Höhen werden nur beim Layout gesetzt, nie pro Frame. |
| 15 Fokusring faded ein | N. Sofort. |
| 16 Erfolgs-Toast · 17 Tooltip-Delay | N. Keine Toasts. Kapitel-Etiketten erscheinen per Hover/Fokus gleichzeitig. |
| 18 Auto-Rotation ohne Pause | N. Nichts rotiert von allein, alles hängt am Scroll. |
| 19 Jane Doe/Acme | N. |
| 20 Stempel fehlt | N. Vorhanden. |
| 21 Specimen-Fall-through | N. |
| 22 Null-Chroma-Neutrals | Befund klein: `#1e1e1e` als Platzhalterhintergrund hinter den echten Terminal-Screenshots (nie sichtbar). |
| 23 Akzent > 5 % | Befund bewusst: Gold-Flash in S2 füllt am Höhepunkt (Peak) den Bildschirm, atmosphärische Ausnahme laut Genre-Hinweis; sonst Gold nur für Linien/Rahmen. |
| 24 Abstände auf 4-px-Skala | Befund: fluide `clamp()`-Abstände statt fester Skala. Bewusste Abweichung, siehe Abschnitt 14. |
| 25 Prosa-Breite 45 bis 75 ch | Befund klein: Hero-Lead 30 ch (kurze Plakatzeile). Sonst 46 bis 60 ch. |
| 26 Zustände interaktiver Elemente | Nur Tasten/Links interaktiv: default, `:focus-visible`, Hover (nur `(hover:hover)`). Kein `disabled`-Fall vorhanden. |
| 27 Motion ohne Reduced-Motion | N. Komplette Ersatzversion (`.rm`). |
| 28 Video | n. a. (kein Video). |
| 29 Abstrakter Hintergrund | N. Hintergrund = echtes Logo-Dreiecksnetz, ein Akzent, 16 % Deckkraft. |
| 30 Icon-Tells · 31 Lottie | N. Keine Icons, kein Lottie. |
| 32 Archetyp-Wiederholung | n. a. (erstes v2-Ergebnis). |
| 33 Dekoration ohne Name/aria-hidden | N. Alle Canvas/SVG `aria-hidden` oder `role="img"` + Label. |
| 34 Horizontal-Scroll 320 bis 1920 | N. `overflow-x:clip` gesetzt, gemessen false (1440, 390, nach Resize). |
| 35 Hervorhebungs-Bänder · 36 Zentrierung von Leisten | N. Keine Bänder. Band-Layout `align-items:center`. |
| 37 > 3 Schriftfamilien | N. EB Garamond, Jost, `ui-monospace` nur für Dateinamen (Familie 3, zwei Slots). |
| 38/38a Kursive Überschriften | N. |
| 39 Eingabefelder | n. a. (keine Felder). |
| 40/41 Kontrast | N. Creme/Petrol-dunkel ≈ 11:1, Tinte/Creme ≈ 14:1, `.cap` 66 % Creme auf Petrol-dunkel ≈ 5,6:1. Gold als Text nur auf Nacht (> 4,5:1). |
| 42 Nav-Fingerabdruck | N. Randleiste aus Punkten (N9), keine Textnavigation. |
| 43 Footer-Fingerabdruck | N. Schluss als Aussage (Ft5). |
| 44 Hero passt in die Falte | N. 1440×900 und 1280×800 geprüft, Titel, Lead, Zeile und Ring komplett sichtbar. |
| 45 Dekoration ohne Anker | N. Die Hero-Dreiecke sind das Logo-Motiv (Signaturmotiv laut `design-brief.md`). |
| 46 Erfundene Metrik | N. Cockpit-Zahlen als „Beispieldaten“ markiert, Graph-Zahlen aus `graph/README.md`. |
| 47 Nachgezeichnetes Chrome | N. Siehe oben. |
| 48 Token-Disziplin | Befund: in JS (`C`, Shader-Konstanten, Canvas-Paletten) stehen Marken-Hexwerte direkt, weil WebGL/Canvas keine CSS-Variablen lesen. Werte entsprechen exakt den Tokens. |
| 49 Zweizeilige Klicktexte | N. Einziger Link einzeilig; Kapitelpunkte ohne Text. |
| 50 `1fr` mit Bildern | N. Tools-Grid `minmax(0,4fr) minmax(0,8.6fr)`. |
| 51 Display-Wortumbruch | Mittel: lange Wörter („Patientenkommunikation“) nur in 12 px-Rollenlabels, dort umgebrochen. Überschriften brechen an Leerzeichen. |
| 52 Section-Head ohne Mobil-Collapse · 53 Radio-Tabs | n. a. |
| 54 Tag neben Überschrift · 55 Versalien-Zeilenabstand | N. Es gibt keine Eyebrows und keine Versalien-Überschriften. |
| 56 Zwei Sticky-Elemente bei top:0 | N. Pro Zeitpunkt ein Sticky-Stage. Fixe Chrome-Elemente sind `fixed`, nicht `sticky`. |
| 57 Studied DNA verworfen | n. a. |

## 3. scroll-craft
**Grammatik:** Continuous World (2.4), umgesetzt als **ein persistentes Three.js-Canvas**, nicht als Video-Worldflight (laut `build-threejs-scroll-worlds`). Warum nicht Filmic one-shot (Pflichtbegründung „why the other seven did not fit“): kein Filmmaterial vorhanden und verboten; Live surface (2.3) wäre ehrlich nur mit lauffähigen Panels, und das Cockpit läuft nicht in dieser Datei, sondern ist echter Screenshot; Chaptered editorial, Poster, Gallery, Split, Cutlist passen nicht zu einer durchgehenden Reise in den Kopf.

**Interview (selbstverfasst, Orchestrator-Brief statt Gespräch, ehrlich markiert):** Vibe: Klinik bei Nacht, Messing, Papier-Bildschirme. Referenz-Medien: Kubrick-Innenräume, Anatomieatlas, alte Operationssaalpläne. Reise: Kopf → Flug hinein → Cockpit → Werkzeuge → Wissen → Helfer → Abläufe → Regel → Schluss. Eine Sache, die keine Seite hat: **man fliegt durch den Kopf des Logos und landet im echten Bildschirm.** Reichweite: editorial/premium-ruhig. Welt: ein Ort. Assets: echte Screenshots, Logo, Porträts.

**Feeling-Kurve** (Emotion, dann Ursache):
1. Ruhe, Wiedererkennen (S1): das vertraute Logo, jetzt echtes 3D, Profil exakt deckungsgleich.
2. Neugier (S1 Ende): der Kopf dreht ins 3/4-Profil, der Ring löst sich.
3. **Staunen / Peak (S2)**: Facetten klappen wie Blenden auf, goldenes Licht innen, die Bildschirmebene dreht sich in die Fläche.
4. Orientierung (S3): echtes Cockpit, Gold-Rahmen führt von Modul zu Modul.
5. Vertrautheit (S4): der echte Verlauf von Claude Code und Hermes.
6. Weite (S5): echter Wissensgraph dreht sich, Punkte erscheinen gruppenweise.
7. Gemeinschaft (S6): Donald mit den Helfern in Tiefe, Impulse wandern.
8. Klarheit (S7): Dateiname benennt sich um, Schiene läuft durch.
9. **Gewissheit (S8)**: drei Sätze erscheinen Wort für Wort, echte Belege daneben.
10. Auflösung (S9): Kopf setzt sich zusammen, Ring dreht in die Ausgangslage, Kontakt.

**Peak:** „Der Bildschirm ging auf, und ich war im Cockpit.“ Größter Fahrweg der Seite: S2 + S3 = 1.470 vh. Davor leise (S1 Ruhe). Ende löst auf (Ring dreht auf 0°, Kopf geschlossen).

**Tell-someone-Satz:** „Es ist die Seite, bei der man durch das Logo-Gesicht in unser echtes Cockpit fliegt.“

**Fingerabdruck-Eintrag (ehrlich: Registry im Projekt leer, daher kein Gate-Konflikt, Eintrag hier):**
| Build | Grammatik | Nav | Hero-Device | Akt-Folge | Schluss | Signature | Welt |
|---|---|---|---|---|---|---|---|
| KIRA fürs Team v2 | Continuous world (Three.js) | Randleiste aus Kapitelpunkten + Fortschrittsfaden | Echtes 3D-Mesh im Logo-Ring | Kopf, Flug, Cockpit-Zoom, 3D-Fächer, Graph, Orbit, Schiene, Wortreveal, Auflösung | Kopf schließt sich, Kontakt als Textlink | **Kopf-Durchflug**: Facetten öffnen sich als Blenden, Bildebene dreht sich zum Screen | Klinik-Nacht, echte Screens |
Länge: 9 Szenen in 7 Sektionen, 33.300 px = 37 Viewport-Höhen (bewusst länger als das 8-bis-14-Budget, weil die Szenenfolge vorgegeben ist). Abweichung benannt.

| Regel (Zitat) | Wo |
|---|---|
| „Variety is the product … never the same device twice in a row“ | Gerätefolge: 3D-Welt, 2D-Zoom per Transform, 3D-Fächer (CSS), Pinned-Tilt mit Lupe, Canvas-Graph, Orbit (Canvas + DOM), horizontale Schiene, Wort-Reveal. |
| „Layer the hero … Depth from differential movement“ / `parallax`: „Never put body copy on a parallax layer“ | S1: fern = Logo-Netz `#far` (Faktor 0,2 am Gesamtfortschritt), mittel = Ring + Canvas-Kopf, nah = drei unscharfe Dreiecke `.near i` (Faktoren 1,4 / 1,9 / 2,6), Text steht still. S6: Agenten nach Tiefe skaliert/unscharf. S7: `rfar` (0,35) / Schiene (1,0) / Token (voraus). |
| „A scroll cue, arrow, or animated mouse icon“ verboten · „01 / 06 section counters“ verboten | Weder Scroll-Hinweis noch Zähler. |
| „An eyebrow above every section heading“ | Keine Eyebrows. |
| „Em dash anywhere visible“ | Null im sichtbaren Text (geprüft per Skript). |
| „Centred copy in every act“ | Anker wechseln: links unten (S1), Band unten (S3), links mittig (S4/S5), Wortblock (S8), Mitte (S9). |
| „A full-frame dark overlay to fix contrast“ | Kein Overlay. Text auf Bühne nur mit festem Petrol-Band (S3) oder auf ruhigem Grund. |
| „Text baked into a generated image“ verboten | Alle Texte sind echtes HTML. Texte in Screenshots sind echte Oberflächen. |
| „Invented statistics in a counter“ | Keine Zähler. |
| „`transition: all`, or animating width/height/top/left“ | Nur transform/opacity. |
| „Shipping without running Step 5“ | Siehe Abschnitt 14 und `_shots/team-v2/`. |
| Feel-Check (feel.md §6): „Scroll the page cold, write one word per act, then diff against the curve“ | Wort je Akt beim Durchblättern der Kontaktbögen: Ruhe / Staunen / Licht / Orientierung / Vertrautheit / Weite / Gemeinschaft / Klarheit / Gewissheit / Ruhe. Abweichung gefunden: S6 wirkte beim Einstieg (p=.1) leer, nur Donald sichtbar; die Einblend-Dauer der Agenten wurde von 0–.22 auf 0–.16 verkürzt. S7-Einstieg ist bewusst ruhig. |

## 4. build-threejs-scroll-worlds
| Regel (Zitat) | Wo |
|---|---|
| „one persistent Three.js world + one normalized reversible scroll state“ | Ein Renderer, eine Szene `scene`, `headG` + `planeG`; Scroll → `u` (0–1) in `worldUpdate`, voll reversibel (keine Zeit, keine Zustände außerhalb von `u`). |
| „Keep separate values: rig.target / rig.smooth“ | Exakter Zustand = `scrollY`; Glättung nur Zeigerparallax (`ptr.sx` lerp 0,06). Kamera ist rein Funktion von `u`. |
| „Store position, target, FOV … and responsive overrides“ | `frameKeys()`: Position, Blickpunkt, FOV, View-Offset je Keyframe, Hermite-Spline `hermite()`. Mobil: Rahmen aus `H`, `HB.B`, Aspekt berechnet. |
| „Hide unavoidable discontinuities behind occlusion, darkness, dense atmosphere“ | Der Wechsel WebGL-Plane → DOM-Bild (Handoff bei vh 392) liegt im vollflächigen Cockpit-Cover, pixelgleich (Cover-Geometrie `CP.Bw/Bh`). |
| „Cap `dt`, pause when hidden“ | Render nur, wenn Szene im Bereich (`inView`), sonst `canvas.opacity=0`, kein `render`. rAF-Schleife rechnet nur bei geändertem Scroll/Zeiger. |
| „Cap device pixel ratio“ | `DPR=min(devicePixelRatio,2)`. |
| „Provide a composed poster … when WebGL is unavailable“ | `#poster`/`#poster2` = echtes Logo-Kopfpfad als SVG; `gl.ok=false` → Cockpit blendet ohne Flug ein. |
| „Load progressively … first authored frame complete“ | Erster Frame: Ring + Titel + Poster-Kopf sofort aus DOM, WebGL-Kopf ersetzt das Poster, sobald Three importiert ist. |
| „Dispose …“ | Einmalige Instanz über die gesamte Lebensdauer, Reparenting entfällt (Canvas fix, `opacity`). |
| „Use local, pinned Three.js files“ (scroll-world-storytelling) | `three@0.169.0` per `npm pack`, `three.module.min.js` als `<script type="text/plain">`, per Blob-URL importiert. Kein CDN. |
| Geometrie: „Establish the large silhouette first“ | `levels.json` aus dem echten Logo-Kopf (Rasterisierung der 45 Dreiecke, Douglas-Peucker → 18 Ebenen), Querschnitts-Sweep mit Ellipsen (14 Segmente, halber Versatz je Ring → Dreiecksnetz). Profil deckt sich mit dem Ring-Logo. |
| Licht: „one authored key direction … rim“ | Warmes Key `uKey` links oben vorn, kühles Rim `uRim` von hinten rechts (Fragment-Shader), Facetten flach schattiert, goldene Kanten (LineSegments, gleicher Vertex-Shader, damit Kanten mit den Blenden wandern). |

## 5. scroll-world-storytelling
| Regel (Zitat) | Wo |
|---|---|
| „Choose one primary mode“ | Three.js-Welt für S1/S2 (Spatial-Metapher: Kopf), danach DOM/Canvas-Szenen. Kein Video. |
| „Reject the generic default of a glowing blue planet in dark space“ | Metapher ist der Logo-Kopf, Palette Petrol/Gold. |
| „Cap device pixel ratio at 2 … Provide a static CSS/SVG poster when WebGL fails or reduced motion is requested“ | Siehe 4. |
| „Preserve the source thesis, sequence, facts, and caveats. Never invent proof.“ | Beat-Ledger = `storyboard-team-v2.md`; Zahlen nur belegt. |
| Beat-Ledger „headline 3–8 words; body one sentence under 24 words“ | Bandzeilen S3 (5 bis 7 Wörter, ein Satz Unterzeile). |
| „Keep native, reversible document scrolling. Never hijack the wheel.“ | Kein Wheel-Handler. |

## 6. scroll-scrubbed-word-reveal
| Regel (Zitat) | Wo |
|---|---|
| „Walk text nodes with TreeWalker; do not flatten the container with textContent“ | `splitWords()` in `main.js` läuft über Textknoten, behält Whitespace, `<span class="g">` (Gold) bleibt als Element erhalten. |
| „Mark generated spans aria-hidden only when an equivalent unsplit accessible copy remains“ | Absatz `#big` trägt `aria-label` mit dem vollständigen Satz; Wort-Spans `aria-hidden`. |
| „Map scroll to words: local = clamp(reveal * wordCount − index)“ | `regelUpdate`: `lp=clamp(r*n*1.0-i*.82)` → CSS `--wp`. |
| „Hidden opacity 0.12–0.3 · blur 4–10px · offset .08–.22em“ | `.regel .big .w`: Opacity .14 → 1, Blur 6 px → 0, Offset .16em → 0 (nur `--wp`). |
| „Under reduced motion, show every word immediately“ | RM-Zweig zeigt den Satz als Klartext. |
| „Final text must meet normal contrast“ | Creme/Gold-hell auf Nacht. |

## 7. emil-design-eng
| Regel (Zitat) | Wo |
|---|---|
| „Never animate keyboard-initiated actions“ | Tastenansprünge sind `scrollTo`; nichts am UI animiert zusätzlich. (Der Scroll selbst läuft glatt, ist aber Scrollbewegung, keine UI-Animation.) |
| „Never use ease-in for UI animations“ · „use custom easing curves“ | Alle Kurven aus `eio` (cubic in/out) und `eout` (quart out), CSS `--out:cubic-bezier(.23,1,.32,1)`, `--inout:cubic-bezier(.77,0,.175,1)`. Kein `ease-in`. |
| „Never animate from scale(0)“ | Kleinste Startskala 0,5 (Ebene), Facetten schrumpfen auf 0,5 + Fade per Discard, nie 0. |
| „Only animate transform and opacity“ | Siehe Gate 14. `filter:blur` nur für Wort-Reveal (Regel verlangt es) und Rollen-Tiefenschärfe (≤ 2,6 px, 15 Elemente). |
| „Use blur to mask imperfect transitions … keep blur under 20px“ | Tiefenunschärfe der hinteren Agenten (≤ 2,6 px), Wortreveal 6 px. |
| „Hover animation without media query“ | Nur in `@media (hover:hover) and (pointer:fine)`. |
| „CSS animations beat JS under load“ | Alle scroll-gebundenen Bewegungen sind JS (müssen scrubben); es gibt keine zeitbasierten CSS-Animationen. |
| „Asymmetric enter/exit timing“ | Band blendet in 42 vh ein, Zeilen kreuzblenden 26 vh. |
| „Review your work the next day / slow motion“ | Alle Szenen in Kontaktbögen Bild für Bild gesichtet (35 Punkte je Viewport). |

## 8. animate
Gate-Sequenz aus dem Skill pro Bewegung:
| Bewegung | Frequenz | Zweck | Werkzeug | Eigenschaften | Kurve |
|---|---|---|---|---|---|
| Flug (S2) | einmalig (Selten/Erststart) | Erklärung/Delight | rAF + Scroll-Scrub (muss scrubben) + WebGL | Kamera, Shader-Uniform `uOpen` | Hermite + `ss()` |
| Cockpit-Kamera (S3) | je Stopp | Räumliche Konsistenz | Transform `translate+scale` | transform | `eio`, 40 vh je Fahrt |
| Wortreveal (S8) | einmalig | Lesetempo | CSS-Variablen aus Scroll | transform, opacity, filter | linear auf Scrub |
| Helfer-Impulse (S6) | Dauer | Zustand (Übergabe) | Canvas, scrubbed | – | linear |
| Hover Kapitelpunkt | Selten | Feedback | CSS transition | opacity, transform | 200 ms `--out` |
Keine Animation für Tastenfokus oder Navigation (Disqualifier „100+ times/day“). Reduced-Motion-Variante: statisch, vollständig. Hover-Gating: `(hover:hover)`.

## 9. design-taste-frontend
Design Read (0.B): „Reading this as: interne Präsentation für ein Praxisteam, mit einer editorial-ruhigen, filmischen Sprache, Richtung Native CSS + Canvas/WebGL + Scroll-Scrub.“ Dials: VARIANCE 8, MOTION 7, DENSITY 3 (Abgeleitet aus „Awwwards/Agency“ + Marken-Ruhe).
| Regel (Zitat) | Wo |
|---|---|
| „NO div-based fake screenshots“ · „Hero needs a real visual“ | Hero = echtes 3D-Modell aus dem Logo; Screens echt. |
| „NO scroll cues“ · „NO section-number eyebrows“ · „NO decorative status dots“ | Alle drei erfüllt (die Kapitelpunkte rechts sind Navigation, nicht Dekoration). |
| „NO em-dash“ | 0 im sichtbaren Text. Echte Titel aus Daten werden in `lab()` auf „-“ normalisiert. |
| „SERIF DISCIPLINE“ (Serif nur bei expliziter Marke) | Serif ist die Website-Entscheidung des Owners; EB Garamond steht ausdrücklich in der Rotationsliste. Fraunces/Instrument Serif nicht verwendet. |
| „EMPHASIS RULE“ (kein Fremdfamilien-Akzent) | Betonung in S8 durch Gold derselben Familie, nicht durch andere Schrift. |
| „Marquee max one“ | Kein Marquee. |
| „window.addEventListener('scroll')“ verboten | Nicht verwendet; rAF-Schleife liest `scrollY` (Scroll-Listener-frei), kein Scroll-Event. |
| „Section-Layout-Repetition Ban“ | 7 Sektionen, 7 verschiedene Layoutfamilien. |
| „Hero stack discipline (max 4 text elements)“ | h1, Lead, Datumszeile = 3. |
| „Hero top padding cap“ | Hero-Text unten, Ring zentriert in der Fläche, kein Leerraum oben. |
| „NO fake-precise numbers“ | Siehe Gate 46. |
| „COPY SELF-AUDIT“ | Jeder sichtbare String gelesen (stop-slop/humanizer unten). |
| „Premium-consumer palette ban“ (Beige+Messing) | Nicht anwendbar: Creme + Gold sind Markenfarben des Owners und ausdrücklich fixiert. Als Ausnahme laut Skill „brand brief explicitly names those colors“ geführt; Creme tritt nur in S3/S7 als Bildschirm-/Papierfläche auf, nicht als Body-Reflex. |

## 10. no-ai-design-slop
| Regel (Zitat) | Wo |
|---|---|
| „Slop is not a color, font, gradient … It is a choice made by reflex rather than for the product.“ | Entscheidungstabelle: jede dekorative Schicht (Dreiecke, Ring, Flash, Gold-Rahmen) hat eine Aufgabe: Marke, Raum, Peak, Führung. |
| „Removal Test: Remove it mentally. If meaning … survives and clarity improves, delete it.“ | Vor/nach den Screenshots verworfen: Zählnummern an den Band-Zeilen (CSS-Regel `.band .n` ist ungenutzt), ein gezeichneter Ordner für S4 (ersetzt durch das echte Hermes-Ordnerbild), das dritte Dreieck am Ring (Überdeckung). |
| „Do not invent customers, metrics, testimonials, awards, ratings, product screens, or activity.“ | Keine. S4 nutzt die echten CLI-Screenshots aus `assets-real/screens/real-cli/`. |
| „Motion may explain state, causality, hierarchy, continuity, or spatial change.“ | Siehe animate-Tabelle. |

## 11. impeccable
(`context.mjs` im Repo nicht vorhanden; Skill-Regeln trotzdem angewandt. Register: brand.)
| Regel (Zitat) | Wo |
|---|---|
| „Verify contrast … Body text ≥ 4.5:1“ | Siehe Gate 40. |
| „Cap body line length at 65–75ch“ | `p{max-width:46ch}`, Bandtext 60 ch. |
| „Hero / display heading ceiling: clamp() max ≤ 6rem“ | Ausnahme: H1 `clamp(3.2rem,8.2vw,8rem)`: Plakat-Hero. Auf 1440 = 8 rem, auf 1280 = 6,5 rem. Bewusste Abweichung (Signature-Titel, drei Wörter). |
| „Display heading letter-spacing floor ≥ −0.04em“ | −0.025em. |
| „`text-wrap: balance` on h1–h3; `pretty` on prose“ | `h1,h2,h3{text-wrap:balance}`, `p{text-wrap:pretty}`. |
| „Reveal animations must enhance an already-visible default“ | Hero und Bühne sind im ersten Frame vollständig sichtbar. Reveal nur an Wörtern in S8 (dort Reduced-Motion-Klartext). |
| „The cream / sand / beige body bg is the saturated AI default“ | Body ist Nacht/Petrol, Creme nur dort, wo es die Oberfläche des echten Screenshots ist (S3, S7). |
| „Absolute bans: side-stripe borders, gradient text, hero-metric template, identical card grids, eyebrows, numbered section markers“ | Keine davon. |
| „Text that overflows its container“ | Mobil 390 geprüft, keine Überläufe. |

## 12. stop-slop + humanizer (jeder sichtbare Satz)
Methode: jeden Satz auf Füllwörter, Adverbien, Passiv, „nicht X, sondern Y“, Dreierreihen, Fragmentketten, Gedankenstriche prüfen; zusätzlich humanizer-Muster §1 bis §6 und §12 bis §18.
| Satz (final) | Befund → Änderung |
|---|---|
| „Unser digitales Praxisteam. Dieser Rundgang zeigt, was heute schon läuft, an den echten Bildschirmen.“ | Aktiv, konkret, kein Adjektivstapel; „echt“ ist hier ein Fakt. |
| „Das ist euer Cockpit. Jeden Morgen um 08:00 frisch.“ | Storyboard-Vorgabe, aktiv, konkret, bleibt. |
| „Oben stehen die Zahlen des Tages.“ | Ort + Sache, kein Staging („Auf einen Blick“ vermieden). |
| „Der Tagesplan zeigt alle acht Räume.“ / „Im Team-Board hakt ihr Aufgaben ab.“ | Menschliches Subjekt „ihr“. |
| „Donald antwortet auf Fragen.“ + „Er liest die Praxisplanung. Änderungen prüft er per Read-back.“ | Zitat der echten Oberfläche, keine Dramatisierung. |
| „Implantate heute: Bestand und Entwürfe.“ + „Bestellt wird von Hand. Der letzte Klick liegt immer bei einem Menschen.“ | Zweiter Satz: Fakt aus dem Screenshot (Regel-Box), „immer“ ist dort wörtlich. |
| „Claude Code arbeitet in unseren Ordnern.“ / „Es liest Dateien, führt Befehle aus und schreibt jeden Schritt in den Verlauf. Ihr seht, was passiert.“ | Dreierreihe „liest, führt aus, schreibt“ bleibt: drei echte, getrennte Tätigkeiten (humanizer §6 erlaubt „three real items“). |
| „Der Hermes-Agent arbeitet im Hintergrund.“ / „Im Startbild stehen seine Werkzeuge, darunter cronjob_manage für geplante Aufgaben sowie read_file und write_file für Dateien.“ | Reale Werkzeugnamen aus dem Screenshot. |
| „Sein Zuhause ist ein Ordner.“ | Kurzer Satz trägt eine neue Info (die Folgesätze), kein Zitat-Closer. |
| „Euer Wissen liegt in Obsidian.“ | Direkt, keine Landkarten-Metapher (humanizer §3). |
| „Jeder Punkt ist ein Dokument oder Skript von uns. Die Linien sind die Verweise.“ | Abweichung vom Storyboard („Notiz“): Daten sind Dokumente und Code des KIRA-Ordners, daher wahrheitsgetreu. |
| „Donald verteilt die Aufgaben.“ / „Die Rollen sind festgelegt, vom OP-Plan bis zum Datenschutz. Die Ausführung läuft über Donald. Vor jeder Wirkung fragt er einen Menschen.“ | Ehrlichkeitsformel aus `praxisarchitektur-real.md` (Rollen festgelegt, Ausführung über Donald), kein „läuft autonom“. |
| „Das läuft heute.“ / „Zwei Abläufe, Schritt für Schritt.“ | Letzteres Floskelverdacht („Schritt für Schritt“); behalten, weil es die Schiene ankündigt, aber ohne Adverb. |
| Stationstexte (Beleg scannen, Hermes liest ein, Monatsabschluss, Mail verschickt ein Mensch, Post vorsortiert, Notfälle, Entwürfe) | Aktiv, Subjekte benannt (Scanner, Hermes-Agent, Vincent, Draft Builder). „Das macht der Hermes-Agent. Sonst niemand.“ (Owner-Vorgabe, Storyboard) ist eine Mini-Staging-Zeile; bleibt, weil sie die Verantwortlichkeit benennt. |
| „Patientendaten verlassen das Praxisnetz nicht. KIRA plant. Den letzten Klick macht ein Mensch.“ | Drei kurze Sätze mit verschiedener Struktur, keine Gegenüberstellung. |
| „Fragen und Ideen für neue Helfer:“ | Kontaktzeile, konkret. |
Verbleibendes: Mildes Rhythmus-Muster (kurz-kurz-kurz) in S8: Teil der Vorgabe „0-PID kurz und stark“.

## 13. Nicht ausgeführte Skill-Teile (ehrlich)
- ui-ux-pro-max `--persist` (keine Design-System-Dateien erzeugt, um das Repo nicht zu verändern).
- impeccable `context.mjs`/`palette.mjs`: Skripte nicht im Repo, nicht ausgeführt (Marke fix).
- scroll-craft Skripte (`kie.mjs`, `shoot.mjs`, `serve.mjs`): nicht ausgeführt (Fremdskripte, kie.ai verboten). Verifikation per eigenem Playwright-Skript nach dem Muster aus `verify.md` (sechs Positionen je Akt, Desktop + Mobil + Reduced Motion).

## 14. audit-ai-design-slop (gegen die eigenen Screenshots)
Geprüft: `_shots/team-v2/d-*.png` (1440×900, 36 Stände), `m-*.png` (390×844, 36 Stände), `rm-*.png` (Reduced Motion), `d1280x800-kopf.png`. Nicht geprüft: echte Geräte (iOS Safari), GPU-Frame-Zeiten, Screenreader.

| Priorität | Klasse | Muster | Evidenz | Folge | Fix (umgesetzt) |
|---|---|---|---|---|---|
| P1 | Quality defect | Karten im 3D-Fächer in falscher Tiefenreihenfolge, vordere Karte von hinteren überdeckt | `d-03b-ansichten-*` frühe Fassung: drei halbtransparente Karten übereinander | Fokus-Ansicht unlesbar | `z-index` je Karte aus Tiefe `d` in `setDeck()`. |
| P1 | Quality defect | Bild mit `height`-Attribut im Grid gestreckt (Claude-Code-Screenshot füllte die Höhe) | früher `c030` | Verzerrt, Layout gesprengt | `img{height:auto;max-width:100%}`. |
| P1 | Quality defect | Schluss-Kopf (WebGL) schien durch Kapitel 8 hindurch | `g600` früh | Fremdobjekt über dem Satz | Canvas-Sichtbarkeit an `ende.top` gebunden (`endUpdate`). |
| P1 | Quality defect | Vault: Text links vom Screenshot verdeckt | `d000` früh | Unlesbarer Einstieg | Screenshot nach rechts (`left:62%`), `.vt` mit fester Breite. |
| P1 | Quality defect | Mobil: Knoten-Karte aus dem Bild | `m-05-vault` früh | Inhalt abgeschnitten | `nx` auf Viewport geklemmt. |
| P1 | Quality defect | Tastenfolge übersprang den ganzen Flug in einem Schritt | Test `kb.py`: 936 → 3528 | Peak ungesehen | Zusätzliche Stopps bei 215 vh und 310 vh. |
| P2 | Slop pattern | Dekoratives Dreieck überdeckte einen Ring-Buchstaben | `a000` früh | Ring/Logo gestört | Dreieck nach unten rechts außerhalb des Rings verschoben. |
| P2 | Slop pattern | Graph: isolierte Inseln im Leerraum („Sternenstaub“) | frühe `d400` | Wirkt zufällig, Struktur verloren | Stichprobe auf die 9 größten zusammenhängenden Gruppen (900 Knoten, echte Hub-und-Speichen-Struktur), Layout mit unsichtbaren Ankern. |
| P2 | Slop pattern | Echte Belege (Kopfzeile, Regel) in S8 zu klein, unlesbar | frühe `g400` | Beweis nicht lesbar | Neu zugeschnitten (nur die beiden Pillen), Breite 40 vw. |
| P2 | Quality defect | Mobil: Fächer-Karten (367 px) unlesbar | `m-03b-ansichten-*` | Screenshots nur als Briefmarke | Karten 1,85× Viewport-Breite, seitlicher Versatz beim Fokuswechsel. |
| P3 | Quality defect | Halte-Zustände in S3 standen still (toter Scroll bis 70 vh) | Sichtung der Folgen b520/b540 | Totes Scrollen | Langsamer Drift (+4,5 % Skala) in jedem Halt. |
| P3 | Quality defect | Helfer: Netz klein, Donald von vorderen Agenten verdeckt | `e300` | Tiefe unklar | Zwei geneigte Umlaufbahnen (Pitch .5) statt Kugel, größerer Radius. |
Offen / unbekannt: (a) Gate 24 (4-px-Skala) bewusst nicht erfüllt, fluide Abstände. (b) Mobil-Frame-Rate nur in Headless/SwiftShader geprüft, keine Gerätemessung. (c) Rail-Szene hat im oberen Drittel Leerraum; als Weißraum belassen. 
**Größte verbleibende Verbesserung:** Prüfung auf einem echten iPhone/Android mit Touch-Scrub (verify.md, „The phone is a different machine“).
