# Prov i historia

Underlag och verktyg för att skapa kapitelprov med Claude.

| Mapp | Innehåll |
|---|---|
| `kapitel/` | Bokens kapitel, inskannade som PDF (t.ex. `Kapitel 23.pdf`). |
| `exempelprov/` | Tidigare prov som visar stil och upplägg. |
| `prov/` | Nya prov. Varje prov får en egen mapp med `prov.json`, elevversion och facit. |
| `.claude/skills/skapa-prov/` | Skillen som skapar proven, och scriptet som bygger Word-filerna. |

## Skapa ett prov

Lägg kapitlet i `kapitel/` och skriv till exempel:

> Skapa ett prov på kapitel 23.

Provet får 12–15 flervalsfrågor, därefter begreppsfrågor och till sist resonerande frågor som kräver allt längre svar.
Resultatet hamnar i `prov/kapitel-23/`:

- `kapitel-23_elev.docx` – provet som delas ut
- `kapitel-23_facit.docx` – rätta svar, modellsvar och bedömningsstöd (E/C/A)
- `prov.json` – provet i strukturerad form (används även för rättning)

Bygga om Word-filerna efter en ändring i `prov.json`:

```bash
pip install python-docx
python3 .claude/skills/skapa-prov/scripts/bygg_prov.py prov/kapitel-23/prov.json
```
