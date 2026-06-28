# 🏗 Inspección Técnica Estructural — Venezuela 2026

**Live app:** https://inspeccion-venezuela.netlify.app

A mobile-first structural inspection tool for post-earthquake damage assessment. Built for field engineers conducting rapid evaluations of buildings in the affected zone (Vargas state, Caracas, La Guaira).

Developed in collaboration with Ing. JefV & Ing. RmsV, 2026.

---

## What it does

**📋 Nueva inspección** — 7-step mobile form covering:
1. Identification (inspector, building type, resident info)
2. Location (GPS coordinates + automatic UTM Zone 20N conversion)
3. Structural system (columns, beams, nodes)
4. Masonry pathology (crack morphology, width, wall type)
5. Electromechanical systems and stairs
6. Facade evaluation (N/S/E/W)
7. Final verdict — auto-calculated from answers, engineer can confirm or override

**📊 Métricas** — Live dashboard showing:
- Total inspections
- Breakdown by verdict with progress bars
- Inspections by parroquia
- Inspections by building type
- 10 most recent inspections

**🗺 Mapa** — All inspected buildings plotted on a map of the affected zone, color-coded by verdict

**PDF Report** — One tap generates a professional PDF report matching the original paper form, ready to submit to Protección Civil

---

## Verdict system

The app replicates the scoring algorithm from the original inspection instrument:

| Verdict | Color | Trigger conditions |
|---|---|---|
| 🟢 Habitable | Green | No significant damage detected |
| 🟡 Precaución | Yellow | Friso damage or crack > 1mm |
| 🟠 Acceso Restringido | Orange | Beam/node failure, critical masonry, severe facade damage |
| 🔴 Inhabitable | Red | Column failure, foundation damage, severe stair damage |

The engineer always has the final say and can override the calculated verdict.

---

## Tech stack

| Layer | Tool |
|---|---|
| Frontend | React + TypeScript (Vite) |
| Database | Supabase (PostgreSQL + PostGIS) |
| PDF generation | jsPDF (browser-side) |
| Hosting | Netlify |
| Coordinates | UTM Zone 20N auto-conversion |

---

## Database schema

Single table: `inspecciones`

All 6 sections of the inspection form are stored as structured columns. Location stored as both decimal degrees and auto-generated UTM coordinates. PostGIS enabled for spatial queries.

Run `inspeccion-schema.sql` to set up the database.

---

## How to deploy your own instance

1. Create a free account at [supabase.com](https://supabase.com)
2. Create a new project
3. Run `inspeccion-schema.sql` in the SQL Editor
4. Fork this repo
5. Replace `SUPABASE_URL` and `SUPABASE_ANON` in `src/App.tsx` with your project credentials
6. Deploy to [netlify.com](https://netlify.com) — connect GitHub repo, click Deploy

Total setup time: ~15 minutes.

---

## Adapting for other regions

- Update the map viewBox coordinates to your affected zone
- Add or remove inspection sections as needed
- Update the verdict scoring logic in `calcularVeredicto()` to match your instrument
- Update UTM zone in `toUTM()` if outside Venezuela (Zone 20N covers most of Venezuela)

---

## Built by

Paula Lima — Data Engineer, Miami FL  
In collaboration with Ing. JefV & Ing. RmsV  
Built June 24–25, 2026 in response to the Venezuela earthquakes

---

## License

MIT — free to use, fork, and deploy for humanitarian purposes.
