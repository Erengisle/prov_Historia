# Prov i historia

Underlag och verktyg för att skapa kapitelprov med Claude.

| Mapp | Innehåll |
|---|---|
| `kapitel/` | Bokens kapitel, inskannade som PDF. Ange utgåvan sist i filnamnet: `Det långa 1800-talet Gy-11.pdf`, `… Gy-25.pdf`. |
| `exempelprov/` | Tidigare prov som visar stil och upplägg. |
| `prov/` | Nya prov. Varje prov får en egen mapp med `prov.json`, elevversion och facit. |
| `.claude/skills/skapa-prov/` | Skillen som skapar proven, och scriptet som bygger Word-filerna. |

## Skapa ett prov

Lägg kapitlet i `kapitel/` och skriv till exempel:

> Skapa ett prov på Det långa 1800-talet, Gy-11.

Provet får 12–15 flervalsfrågor, därefter begreppsfrågor och till sist resonerande frågor som kräver allt längre svar.
Resultatet hamnar i `prov/det-langa-1800-talet-gy11/`:

- `…_elev.docx` – pappersprovet
- `…_facit.docx` – rätta svar, rättningsnyckel, modellsvar och bedömningsstöd (E/C/A)
- `…_trelson.docx` / `.txt` – en fråga per block, för att kopiera in i Trelson
- `prov.json` – provet i strukturerad form (används även för rättning)

Bygga om Word-filerna efter en ändring i `prov.json`:

```bash
pip install python-docx
python3 .claude/skills/skapa-prov/scripts/bygg_prov.py prov/det-langa-1800-talet-gy11/prov.json
```
