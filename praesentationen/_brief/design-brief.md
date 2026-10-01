# Design-Brief — zwei KIRA-Präsentationen (Orchestrator → Worker)

Ziel: Zwei eigenständige HTML-Präsentationen, die man nach einem Design-Kongress vor 1.000 Leuten zeigen könnte.
Scroll ist die Zeitleiste. Jede Bewegung hängt am Scroll-Fortschritt (scrubbed), nicht an Autoplay-Loops.

## Verbindliche Skills (installiert unter ~/.claude/skills — mit dem Skill-Tool laden UND befolgen)
Reihenfolge der Anwendung:
1. `ui-ux-pro-max` — Design-System-Entscheidung (Stil, Palette-Rollen, Typo-Paarung, Pre-Delivery-Checkliste).
2. `hallmark` — Makrostruktur wählen, Slop-Test-Gates, Pre-Emit-Kritik, Stempel-Kommentar im CSS.
3. `scroll-craft` (Nate Herk) — Seiten-Grammatik + Signature-Move, **Tiefenebenen (hero-depth.md)**, Gefühlskurve (feel.md), Devices (devices.md), Uniqueness-Gate, Verifikation per Scroll-Screenshots.
4. `scroll-world-storytelling` / `build-threejs-scroll-worlds` / `scroll-world` — eine durchgehende Welt statt gestapelter Abschnitte. KEINE KI-generierten Videos, keine bezahlten Dienste (kie.ai, Higgsfield, Monid): alles prozedural mit Canvas/SVG/CSS/WebGL.
5. `scroll-scrubbed-word-reveal` — für Kernsätze.
6. `emil-design-eng` + `animate` — Kurven, Dauern, Unterbrechbarkeit.
7. `design-taste-frontend` (Anti-Slop) + `no-ai-design-slop` + `impeccable` — als Gate während und nach dem Bau.
8. Texte: `stop-slop` + `humanizer` auf JEDEN sichtbaren Satz anwenden.
Am Ende: `audit-ai-design-slop` gegen die eigene Datei laufen lassen und die Funde beheben.
Hinweis: Fremde Skripte aus den Skills NICHT ausführen (kein kie.ai, keine Generierung). Lesen und anwenden.

Referenz-Niveau: Dribbble/Mobbin/Refero-Qualität (editorial, ruhig, präzise; große Typo, echte Bildflächen, viel Luft). Diese Seiten nur als Maßstab im Kopf; nichts kopieren.

## Marke (fix)
- Petrol `#2C5F5A` (Primär) · Petrol dunkel `#1A3D3A` · Gold `#B8935A` (Akzent, sparsam) · Creme `#F5F0E8` · Tinte `#1C1C1C`.
  Ableitungen erlaubt (Tonwerte von Petrol, Nacht `#0E211F`), aber keine Fremdfarben (kein Lila, kein Neon-Cyan, keine Regenbogen-Verläufe).
- Name immer „Die Kieferchirurgen“ (nie GmbH). Kontakt: office@diekieferchirurgen.at · Austraße 51, OG 1, 6122 Fritzens.
- Logo: `assets/dkc-logo-white.svg` / `assets/dkc-logo-black.svg` — kreisrunde Wortmarke um einen **Low-Poly-Kopf aus Dreiecken**. Als data-URI einbetten. Pflicht: groß auf Titel + Schluss, dezent fix als Wasserzeichen.
- **Gemeinsames Signaturmotiv:** das Dreiecksnetz des Logo-Kopfes. Punkte und Kanten setzen sich beim Scrollen zusammen, lösen sich auf, werden zu Netzwerken (Helfer-Team, Wissensgraph). So hängen beide Decks optisch zusammen.
- Typo: Display-Serif **EB Garamond** (Website-Entscheidung des Owners) + geometrische Sans als Ersatz für Brandon (z. B. **Jost** oder **Figtree**). Schriften als base64-woff2 einbetten (von fonts.gstatic.com laden), System-Fallback. Keine Inter/Roboto/Arial/Space Grotesk.
- Sprache: österreichisches Standarddeutsch, kurze aktive Sätze, konkrete Zahlen. Keine Floskeln, keine „nicht X, sondern Y“-Ketten, keine Dreier-Aufzählungen aus Reflex, keine Gedankenstrich-Orgie.

## Leitidee des Owners: „Flug in unseren Kopf“
- Start: das Logo groß, der Low-Poly-Kopf in Pseudo-3D (Punkte mit Tiefe, leichte Rotation am Scroll).
- Scroll = Kamera fliegt auf das Gesicht zu und durch die Dreiecksflächen hinein.
- Im Inneren öffnet sich das KIRA-Cockpit (Dashboard) als Explosionsansicht: Module fächern sich in Ebenen auf, jedes Modul wird nacheinander erklärt.
- Die Hermes-Agenten erscheinen mit Gesicht (Tierporträts in Anzug aus `assets/`): Donald (Eule) in der Mitte als Orchestrator, Fachrollen verbunden durch Netzlinien – funktional und logisch (wer gibt wem was, wo ist die Freigabe), nicht als Deko-Galerie.
- Team-Deck: Fokus Dashboard + Abläufe. Technik-Deck: Fokus Werkzeuge, Modelle, Agentic OS; dort wird der Obsidian-Vault als 3D-Graph gezeigt, der rotiert und Knoten öffnet.
- Details/Storyboard: `_brief/inspiration.md` (sobald vorhanden).

## Technik (beide Decks)
- EINE selbstständige `.html`-Datei, alles inline (CSS, JS, Bilder als data-URI, Fonts als base64). Keine CDNs. Ziel < 4 MB.
- Engine: gepinnte Bühne (`position:sticky`) + Kapitel mit Fahrweg (≥180vh), CSS-Variable `--p` (0→1) je Kapitel per rAF aus dem Scroll berechnet; globale `--g` (0→1) für den ganzen Weg.
- **Mehrere Tiefenebenen pro Szene (scroll-craft hero-depth):** mind. 3 Ebenen (fern / mittel / nah + Text), unterschiedliche Parallax-Faktoren, leichte Skalierung/Unschärfe in der Ferne. Der Pointer darf zusätzlich minimal verschieben (Desktop).
- Bodenfarbe wandert beim Scrollen (Creme ↔ Petrol ↔ Nacht) statt harter Abschnittswechsel.
- Navigation: Fortschrittsleiste, Kapitelmarken (Desktop), Pfeiltasten/Leertaste springen kapitelweise, Präsentationsmodus-Taste „P“ (Kapitel vollbild durchschalten, optional).
- `prefers-reduced-motion`: Bewegung aus, Inhalte vollständig lesbar.
- Mobil (390×844) muss funktionieren: Text nicht abgeschnitten, Bühne skaliert.
- Performance: nur `transform`/`opacity` animieren, Canvas mit devicePixelRatio ≤ 2, keine Layout-Thrash-Schleifen.
- Fakten nur aus den Briefs `_brief/inhalt-*.md`. Status ehrlich per Badge: „läuft“, „Pilot“, „im Aufbau“, „geplant“.
- 0-PID: keine Patientendaten, keine echten Namen von Patienten, nur synthetische Beispiele.

## Verifikation (Pflicht vor Abgabe)
Playwright (Python ist installiert; Browser: `executable_path='/opt/pw-browsers/chromium'`):
- Desktop 1440×900 und Mobil 390×844 (`is_mobile=True`), pro Kapitel 3 Scroll-Stände (Anfang/Mitte/Ende, `behavior:'instant'`), Screenshots nach `praesentationen/_shots/<deck>/`.
- Jeden Screenshot ansehen (Read-Tool). Prüfen: bewegt sich die Szene zwischen den Ständen sichtbar? Überlappungen? Leere Flächen? Lesbarkeit? Konsolenfehler = 0.
- Danach `audit-ai-design-slop` und Hallmark-Slop-Test; Funde beheben; erneut screenshotten.
