# Inspiration und Bauplan: Scroll-Welt "Flug in den Kopf"

Stand 2026-10-01. Nur Ideen, keine Assets (alle Galerien/Seiten ohne Reuse-Lizenz). Verifikation: "[V]" = per Suche bestaetigt, "[K]" = aus Fachwissen, URL/Technik vor Zitat gegenpruefen (WebFetch war fuer mehrere Domains vom Proxy gesperrt). Lokale Skill-Dateien `approved-collection.md` und `hero-depth.md` existieren nicht; gelesen: CATALOG, worldflight.md, worlds.md.

## 1. Referenzen (eine uebertragbare Bewegung je Zeile)

| # | Referenz / URL | Technik | Transferable Move |
|---|---|---|---|
| 1 | Igloo Inc, igloo.inc (Awwwards SOTY 2024) [V] | Three.js/WebGL | Eine Szene, Kamera haengt an Scroll, Material/Licht wechseln pro Kapitel statt Schnitt. |
| 2 | Apple AirPods Pro / iPhone-Seiten, apple.com [V] | Canvas + Bildsequenz, Scroll=Frame-Index | Frame-Index aus Scroll, Frames vorgeladen, kein Seek-Lag. Wir ersetzen Frames durch Live-Projektion. |
| 3 | CSS-Tricks "Apple scrolling animation" https://css-tricks.com/lets-make-one-of-those-fancy-scrolling-animations-used-on-apple-product-pages/ [V] | Canvas, sticky | Sticky-Stage + hohes Spacer-Element, `scrollY/(docH-vh)` = Fortschritt. |
| 4 | DeepSee Commerce [V, Name] | Three.js, Abstieg durch Szene | Tiefe als Metapher: Scroll = Abstieg, Nebel/Farbe wechselt mit Tiefe. |
| 5 | Cartier Watches & Wonders (Awwwards SOTD) [V] | WebGL, sechs "Alkoven" | Kapitel als Raeume; Kamera faehrt Raum zu Raum, Text liegt fest als Overlay. |
| 6 | Sleep Well Creative (SOTD Jan 2026) [V] | illustrierte 3D-Welt, Scroll-Reise | Illustrierte Stilisierung statt Fotorealismus traegt Medizinthemen ruhig. |
| 7 | Primland (Aerial Flythrough) [V] | Kamerapfad ueber Terrain | Spline-Kamerapfad, Scroll = Parameter t, Easing nur am Pfadanfang/-ende. |
| 8 | Lusion, lusion.co [K] | Three.js, Partikel, Physik | Partikelfeld, das sich zur Form sammelt (Logo-Kopf aus Punkten bildet sich). |
| 9 | Active Theory, activetheory.net [K] | WebGL, Custom Engine | Portal-Uebergang: Zoom durch ein Loch, dahinter ist schon die naechste Szene. |
| 10 | Bruno Simon, bruno-simon.com [K] | Three.js, Physik | Welt ist spielbar; fuer uns: Hover-Reaktion der Szene auf Zeiger (Parallax 3-5 Grad). |
| 11 | Obsidian Graph View + Plugins: Agentage Galaxy https://github.com/agentage/obsidian-galaxy , 3D Graph https://community.obsidian.md/plugins/3d-graph [V] | Force-Layout, 3D-Rotation | Ordner = Farbcluster, Auto-Orbit, Klick fokussiert Knoten, Nachbarn bleiben hell, Rest dimmt. |
| 12 | 3d-force-graph (vasturiano), github.com/vasturiano/3d-force-graph [K] | Three.js | Kamera fliegt auf angeklickten Knoten zu (Distanz-Tween), Label erst nahe. |
| 13 | Linear, linear.app [K] | CSS/Canvas, Glow-Gradients | Dunkle UI-Flaeche mit einem Lichtkegel; Panel kippt perspektivisch in Sicht. |
| 14 | Stripe Sessions/Connect-Seiten, stripe.com [K] | Canvas-Gradients, CSS 3D | UI-Karten in `rotateX/Y` gestapelt, Abstand wird bei Scroll aufgefaecht = Exploded View. |
| 15 | Vercel Ship / Geist-Seiten, vercel.com [K] | CSS, SVG, WebGL-Dreieck | Ein einzelnes geometrisches Objekt als Held, Lichtbruch als Signatur. |
| 16 | Dashboard-Exploded-Views auf Dribbble/Mobbin/Refero (Suche: "isometric UI layers exploded") [K] | CSS 3D `translateZ` Layer | Schichten: Daten, Logik, UI, jede mit Beschriftungslinie; Auffaecherung = `translateZ(i*gap)`. |
| 17 | OpenAI GPT-6 Astra (4.9.2026), Sol/Luna (22.9.2026) [V Daten; Visuals nicht abgerufen, Gizmodo gesperrt]. Quellen: https://www.macrumors.com/2026/09/22/openai-gpt-6-sol-luna/ , https://en.wikipedia.org/wiki/GPT-6 | Marken-Bildsprache Stern/Sonne/Mond (Tierstufen = Astra gross, Sol mittel, Luna klein) | Modellfamilie als Himmelskoerper-Hierarchie: Groesse = Leistung, Farbe = Rolle. Auf unsere Agenten uebertragbar. |
| 18 | Anthropic Claude Design Launch (17.4.2026) https://www.anthropic.com/news/claude-design-anthropic-labs [V Fakten] | ruhige Typo, warme Flaechen | Zurueckhaltung: wenig Bewegung, ein Akzent, Text fuehrt. Gegengewicht zur Effekt-Schau. |
| 19 | NYT/Reuters Graphics (Scrollytelling, Datenstories) [K] | SVG + IntersectionObserver, `position: sticky` | Sticky-Grafik, Textschritte schalten Zustaende; Schritt-Zustand statt freier Animation. |
| 20 | scroll-craft "Worldflight" (lokal, worldflight.md) | EIN fixed Stage, leerer Spacer, Scroll steuert nur Timeline + Overlay-Opacity | Keine gepinnten Bloecke = keine Nähte. Gleiches Prinzip hier, nur mit Live-Render statt Video. |

Kernmuster aus allen: (a) eine fixe Buehne, Scroll = ein Skalar `p` in [0,1]; (b) Kamera-Parameter als reine Funktion von `p`; (c) Text als zeitlich gefensterte Overlays; (d) Lerp-Glaettung (0.12-0.18) auf `p`; (e) `prefers-reduced-motion` = Stufen statt Fluss.

## 2. Storyboard "Flug in den Kopf" (Spacer 700vh, `p` = Scroll-Fortschritt)

Layer (hinten nach vorn): L0 Sternenfeld, L1 Kopf (Low-Poly, 3D-projiziert), L2 Logo-Ring (Schrift), L3 Innenraum/Cockpit, L4 Agenten-Portraits, L5 Graph, L6 Text-Overlay.

1. **0.00-0.12 Ruhe / Titel.** Kopf klein (Skalierung 1, Rotation Y -25 Grad, langsamer Idle-Drift), Ring dreht langsam. Sterne driften. Text "Die Kieferchirurgen" voll sichtbar.
2. **0.12-0.30 Annaeherung.** Kamera-Zoom 1 -> 4 (ease-in-out), Kopf dreht auf Profil (Y 0). Ring skaliert schneller als Kopf (Parallaxe), blendet bei 0.26 aus. Sterne laufen radial auseinander (Warp-Eindruck, Geschwindigkeit ~ Zoom).
3. **0.30-0.45 Durchbruch ins Auge/Schaedel.** Zoom 4 -> 18 auf Zielpunkt (Stirn/Schlaefe). Dreiecke der Huelle werden einzeln transparent (Alpha je Dreieck = Funktion von Abstand zum Zielpunkt), Kanten bleiben Gold. Bei 0.42 Weissblitz 6 Frames (Cream) als Schnittmaske.
4. **0.45-0.60 Innenraum oeffnet sich.** Huelle faellt aus dem Bild (Scale > Viewport, Alpha 0). Dashboard-Panels (KIRA Cockpit) fahren aus der Tiefe nach vorn: `translateZ -600 -> 0`, gestaffelt 60 ms. Hintergrund Petrol-dunkel.
5. **0.60-0.75 Exploded View.** Panels fachern in 3 Schichten (Daten / Logik / Oberflaeche) auf, Beschriftungslinien zeichnen sich (stroke-dashoffset). Kamera kippt 12 Grad.
6. **0.75-0.90 Agenten erscheinen.** Eule Donald zentral (Orchestrator), Falke Robert, Biber Karl-Heinz usw. im Kreis, Faden-Linien zeichnen sich von Donald zu jedem; Rollenlabel erscheint beim Fokus. Reihenfolge = Datenfluss, nicht Ring-Symmetrie.
7. **0.90-1.00 Wissensgraph.** Portraits schrumpfen zu Knoten im 3D-Graph; Graph rotiert, ein Knoten oeffnet sich (Karte klappt auf). Schluss-CTA.

Zeitfenster-Regel: Overlays blenden mit `smoothstep(a,b,p) * (1 - smoothstep(c,d,p))`, nie harte Schnitte.

## 3. Rezept: Low-Poly-Kopf aus 2D-SVG-Punkten mit Pseudo-Tiefe

Aus dem Logo-SVG die Profil-Dreieckspunkte (x,y) und Indizes exportieren (aus `<polygon points>` oder Pfad-Knoten). Tiefe z aus Profil: z = Breitenfunktion ueber x (Kopf ist in der Mitte dick, Nase/Stirn vorn). Gespiegelte Gegenseite (z negativ) schliesst den Koerper.

```js
// pts: [[x,y],...] normiert -1..1, tris: [[i,j,k],...]
const depth = (x,y)=> 0.55*Math.sqrt(Math.max(0,1-x*x*0.9)) * (1-0.25*Math.abs(y));
const V = []; pts.forEach(([x,y])=>{ const z=depth(x,y); V.push([x,y,z],[x,y,-z]); });
const T = tris.flatMap(([a,b,c])=>[[2*a,2*b,2*c],[2*a+1,2*c+1,2*b+1]]); // Vorder-/Rueckseite
function project(v,ry,rx,cam,f){          // Rotation + Perspektive
  let [x,y,z]=v; const c=Math.cos(ry),s=Math.sin(ry);
  [x,z]=[x*c+z*s,-x*s+z*c]; const c2=Math.cos(rx),s2=Math.sin(rx);
  [y,z]=[y*c2-z*s2,y*s2+z*c2]; const k=f/(cam-z); return [x*k,y*k,z];
}
function draw(ctx,ry,rx,cam){
  const P=V.map(v=>project(v,ry,rx,cam,420));
  T.map(t=>({t,z:(P[t[0]][2]+P[t[1]][2]+P[t[2]][2])/3})).sort((a,b)=>a.z-b.z)
   .forEach(({t,z})=>{ ctx.beginPath(); t.forEach((i,n)=>ctx[n?'lineTo':'moveTo'](cx+P[i][0],cy+P[i][1]));
     ctx.closePath(); ctx.fillStyle=shade(t); ctx.fill(); ctx.strokeStyle='#B8935A'; ctx.stroke(); });
}
```
Flat-Shading: Normale per Kreuzprodukt, Helligkeit = `max(0,n.dot(L))`, mischen zwischen `#1A3D3A` und `#2C5F5A`. Back-Face-Culling: n.z<0 ueberspringen (halbiert Arbeit). Ca. 150-300 Dreiecke, trivial fuer Canvas2D. Zoom 18x: Stroke-Breite mit Zoom skalieren (`lineWidth = 1.2/zoom^0.5`), sonst Linien zu dick.
Alternative bei Zeitnot: 7 geschichtete, leicht versetzte SVG-Kopfscheiben mit `translateZ` in CSS 3D (billig, aber nicht durchfliegbar).

## 4. Rezept: 3D-Force-Graph in Canvas2D (~150 Knoten)

Layout einmalig vorberechnen (Offline-Simulation 300 Schritte beim Laden, ~20 ms) oder aus der Vault-JSON uebernehmen; dann nur rotieren.

```js
// Layout: Abstossung O(n^2)=22k Paare/Schritt, nur beim Start
for(let s=0;s<300;s++){
  for(const a of N){ for(const b of N){ if(a===b)continue;
    const dx=a.x-b.x,dy=a.y-b.y,dz=a.z-b.z,d2=dx*dx+dy*dy+dz*dz+.01;
    const f=0.8/d2; a.vx+=dx*f; a.vy+=dy*f; a.vz+=dz*f; }}
  for(const [i,j] of E){ const a=N[i],b=N[j]; const k=0.02;
    for(const ax of 'xyz'){ const d=(b[ax]-a[ax])*k; a['v'+ax]+=d; b['v'+ax]-=d; }}
  for(const n of N){ n.x+=n.vx*=.85; n.y+=n.vy*=.85; n.z+=n.vz*=.85; n.vx-=n.x*.01; }
}
```
Render pro Frame: Rotation um Y (`ry = t*0.15 + p*2`), Perspektive wie oben, Knoten nach z sortieren, Radius `r*k`, Alpha `0.35+0.65*depthNorm` (Tiefenhinweis ist wichtiger als Schatten). Kanten als ein einziger `beginPath` pro Alphastufe (3 Stufen), nicht pro Kante.
"Node open": Knoten i bei `p` im Fenster: Radius lerp auf 90 px, Kreis wird abgerundetes Rechteck mit Titel/Inhalt (DOM-Overlay an projizierter Position, `transform: translate`), Nachbarn bleiben Gold, Rest `globalAlpha .15`. Rotation bremst auf 0 beim Oeffnen (ease). Hit-Test: naechster projizierter Knoten < r+6 px.
Farbe pro Ordner/Cluster: Petrol-Abstufungen, Gold fuer Hubs (Grad >= 8), Cream fuer Labels.

## 5. Rezepte: Astra (Sterne), Sol (Korona), Luna (Phase)

```js
// Astra: 600 Sterne in Kugel, Rotation um Y; Warp = Streifen mit Laenge ~ Zoomgeschwindigkeit
const S=[...Array(600)].map(()=>{const u=Math.random()*2-1,a=Math.random()*6.283,r=Math.sqrt(1-u*u);
  return {x:r*Math.cos(a),y:u,z:r*Math.sin(a),m:Math.random()}});
S.forEach(s=>{const [X,Y,Z]=rot(s,t*.02); if(Z<0)return; const k=f/(2-Z);
  ctx.globalAlpha=.3+.7*s.m*(0.7+0.3*Math.sin(t*2+s.m*50)); // Funkeln
  ctx.fillRect(cx+X*k,cy+Y*k,1+s.m*1.5,1+s.m*1.5);});
```
```js
// Sol: Radialverlauf + 24 Strahlen mit wanderndem Rauschen, 'lighter'-Blending
ctx.globalCompositeOperation='lighter';
const g=ctx.createRadialGradient(cx,cy,r*.9,cx,cy,r*3); g.addColorStop(0,'rgba(184,147,90,.9)');
g.addColorStop(.4,'rgba(184,147,90,.18)'); g.addColorStop(1,'rgba(184,147,90,0)');
for(let i=0;i<24;i++){const a=i/24*6.283+t*.05, L=r*(1.4+.5*Math.sin(t+i*3.1));
  ctx.strokeStyle='rgba(245,240,232,.08)'; ctx.beginPath();
  ctx.moveTo(cx+Math.cos(a)*r,cy+Math.sin(a)*r); ctx.lineTo(cx+Math.cos(a)*L,cy+Math.sin(a)*L); ctx.stroke();}
```
```js
// Luna: Phase p01 in 0..1 (0 neu, .5 voll). Scheibe + Terminator-Ellipse
ctx.save(); ctx.beginPath(); ctx.arc(cx,cy,r,0,6.283); ctx.clip();
ctx.fillStyle='#F5F0E8'; ctx.fillRect(cx-r,cy-r,2*r,2*r);   // hell
ctx.fillStyle='#1A3D3A'; ctx.beginPath();
const k=Math.cos(p01*6.283)*r; ctx.ellipse(cx,cy,Math.abs(k),r,0,-Math.PI/2,Math.PI/2,k<0); // Schattenhaelfte
ctx.fill(); ctx.restore();
```
Zuordnung: Astra = Sternenfeld/Orchestrator-Himmel (Donald), Sol = Hauptakzent (Gold) bei Kapitel 6, Luna = kleine Cream-Scheibe als Statusanzeige. Luna-Phase (Kreisbogen-Richtung) im Browser pruefen und ggf. Vorzeichen tauschen.

## 6. Performance-Budgets

- 60 fps, Frame-Budget 16 ms; Ziel <8 ms Scripting auf Laptop-iGPU, <12 ms Mobil.
- Ein Canvas fuer Welt (L0-L1,L3,L5), DOM nur fuer Text/Portraits/Overlays; `devicePixelRatio` auf max 2 (Mobil 1.5), Canvas bei Scroll-Sprints ruhig halten.
- Dreiecke Kopf <= 400, Sterne <= 800 (Mobil 300), Knoten 150, Kanten <= 400, Portrait-Bilder inline als WebP-Data-URI <= 25 KB je, Gesamtdatei <= 2 MB.
- Ein `requestAnimationFrame`, `p` per passivem scroll-Listener, Lerp 0.14; Rendern nur wenn `|p - pRender| > 1e-4` oder Auto-Orbit aktiv.
- Kein `shadowBlur` (teuer); Glow ueber vorgerenderte Radial-Sprites auf Offscreen-Canvas.
- `prefers-reduced-motion`: 7 Beats als statische Zustaende, Uebergang per 300-ms-Fade, kein Auto-Orbit.
- Offscreen-Layer pausieren: Graph nur bei p>0.8, Kopf nur bei p<0.5.
- Textfallback (`<noscript>`/Schriftsatz) mit allen Rollen der Agenten fuer Zugaenglichkeit.

## 7. WebGL (nur falls Canvas2D nicht reicht)

Ohne Library: ein Vertex-/Fragment-Shader-Paar, Dreiecke aus Abschnitt 3 als Float32Array, Matrizen (Perspektive + Y-Rotation, 2 x 16 Zeilen) selbst geschrieben, Flat-Shading ueber `dFdx/dFdy`-Normale (WebGL2). Nutzen nur fuer Kopf-Durchbruch mit Alpha-pro-Dreieck, falls >1500 Dreiecke. Empfehlung: Canvas2D reicht fuer das ganze Storyboard.

## 8. Empfehlung

Bauen als Worldflight-Prinzip: ein fixed Stage, leerer Spacer, `p`-Skalar, alle Layer reine Funktionen von `p`. Reihenfolge: (1) Kopf+Zoom+Durchbruch, (2) Cockpit-Panels + Exploded, (3) Agenten-Kreis mit Rollenlinien, (4) Graph + Node-Open, (5) Sterne/Sol/Luna als Atmosphaere. Jeden Beat einzeln per Screenshot bei festem `p` pruefen.
