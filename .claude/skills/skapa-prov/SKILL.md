---
name: skapa-prov
description: Skapar ett kapitelprov (elevversion + facit/bedömningsstöd som Word/PDF) utifrån ett inskannat bokkapitel, i samma stil som exempelproven i repot. Provet börjar med 12–15 flervalsfrågor och följs av frågor som kräver allt längre svar. Använd när läraren ber om ett prov, kapiteltest eller förhör på ett kapitel eller ett ämnesområde.
---

# Skapa prov

Skillen gör ett prov i tre steg: **läs kapitlet → skriv provet som `prov.json` → bygg Word/PDF med scriptet**.
`prov.json` är den enda källan: både elevversionen, facit och (senare) ett rättningsscript läser den.

## Mappar i repot

| Mapp | Innehåll |
|---|---|
| `kapitel/` | Bokens kapitel, inskannade (PDF). |
| `exempelprov/` | Lärarens tidigare prov. Visar stil, språknivå och upplägg. |
| `prov/<namn>/` | Här hamnar nya prov: `prov.json`, `*_elev.docx/pdf`, `*_facit.docx/pdf`. |

## Arbetsgång

### 1. Ta reda på underlaget
- Vilket kapitel/område? Hitta PDF:en i `kapitel/`. Finns den inte: fråga läraren, gissa inte innehållet.
- Inskannade PDF:er saknar oftast textlager. Läs dem med Read-verktyget och `pages` (max 20 sidor per anrop) så att sidorna tolkas som bilder.
- Läs **hela** kapitlet. Anteckna: centrala begrepp, händelser med årtal, personer, orsaker och följder, samt vad kapitlet själv lyfter fram (rubriker, faktarutor, sammanfattningar, instuderingsfrågor).
- Titta på minst ett prov i `exempelprov/` för ton och svårighetsgrad om du inte redan gjort det i samtalet.

**Allt i provet ska gå att besvara med kapitlet.** Fråga aldrig om något som inte står där.

### 2. Upplägg (standard)

Om läraren inte säger något annat:

| Del | Typ (`typ` i JSON) | Omfattning | Svarsutrymme |
|---|---|---|---|
| 1 | `flerval` – "Välj rätt alternativ." | **12–15 frågor**, 3 alternativ, ett rätt | kryssrutor |
| 2 | `begrepp` – "Förklara kortfattat med egna ord." | 4–5 begrepp | 3 rader/begrepp |
| 3 | `fritext` – kortare resonemang | 1 fråga | ca 8 rader |
| 4 | `fritext` – längre resonemang med historiska begrepp | 1–2 frågor | ca 22–24 rader (en sida) |

Svaren ska alltså bli **längre och längre** genom provet. **Ingen tidslinje** (klassen har inte arbetat med det ännu) – lägg bara till en om läraren ber om det.

### 3. Regler för frågorna

**Flervalsfrågor**
- Exakt 3 alternativ, ett entydigt rätt. Felalternativen ska vara rimliga – gärna hämtade från samma kapitel (andra årtal, personer, händelser).
- Blanda frågetyper: *vad var…, när…, vem…, varför…*. Minst 4 av frågorna ska gälla orsaker eller följder (*varför*), inte bara fakta.
- Variera var det rätta svaret står (scriptet varnar om fördelningen är sned).
- Undvik negationer ("Vilket stämmer inte…"), "alla ovanstående" och knep med ordval. Ett alternativ får inte avslöjas av att det är längst.
- Avsluta alternativen med punkt, som i exempelproven.
- Ordna frågorna ungefär i kapitlets kronologi.

**Begrepp**
- Välj begrepp som är centrala i kapitlet och som inte redan är besvarade av en flervalsfråga.
- Skriv i `facit` ett kort modellsvar (1–3 meningar) med det som krävs för full poäng.

**Fritextfrågor (resonemang)**
- Del 3: en fråga som kräver en förklaring eller ett perspektiv, t.ex. *"…Vilket perspektiv, och varför tror du att det är så?"*
- Del 4: en öppen fråga som kräver resonemang och där eleven ska använda historiska begrepp: **orsak och konsekvens, kontinuitet och förändring, villkor och värderingar** (och vid behov *förklaring*, *jämförelse*). Skriv ut i frågan vilka begrepp som ska användas, som i exempelproven.
- Ange `historiska_begrepp` (listan som står i frågan), `innehall` (vad ett bra svar bör ta upp, punktlista med fakta från kapitlet) och `bedomning` med nivåerna **E, C, A**:
  - E: enkla resonemang, några relevanta fakta, begreppen används på ett enkelt sätt.
  - C: utvecklade resonemang, kopplar orsaker/följder, begreppen används relativt säkert.
  - A: välutvecklade och nyanserade resonemang, flera samband, jämförelser, begreppen används säkert.
  Gör kriterierna konkreta för just frågan (vilka orsaker, vilka samband).

**Språk**: Svenska, anpassat för åk 7–9. Korta meningar, inga onödigt svåra ord i frågorna.

### 4. Skriv `prov/<namn>/prov.json`

`<namn>` t.ex. `kapitel-23`. Format (fullständigt exempel: `exempel-prov.json` i den här skillens mapp):

```json
{
  "titel": "Kapiteltest 23",
  "rubrik_hoger": "Kapitel 23",
  "kalla": "Fundament Historia 7–9, kapitel 23",
  "delar": [
    {"typ": "flerval", "instruktion": "Välj rätt alternativ.",
     "fragor": [{"fraga": "…?", "alternativ": ["….", "….", "…."], "ratt": 0, "poang": 1}]},
    {"typ": "begrepp", "instruktion": "Förklara kortfattat med egna ord.", "rader": 3,
     "begrepp": [{"term": "…", "facit": "…", "poang": 2}]},
    {"typ": "fritext", "fraga": "…", "rader": 8, "poang": 4,
     "historiska_begrepp": [], "innehall": ["…"],
     "bedomning": {"E": "…", "C": "…", "A": "…"}}
  ]
}
```
- `ratt` är index (0, 1 eller 2) för rätt alternativ.
- Delarna numreras automatiskt (1., 2., …) i den ordning de står.
- `kalla` hamnar bara i facit, inte på elevens prov.

### 5. Bygg och kontrollera

```bash
pip install python-docx   # om det saknas
python3 .claude/skills/skapa-prov/scripts/bygg_prov.py prov/<namn>/prov.json --pdf
```
Scriptet kontrollerar JSON-filen (antal flervalsfrågor, 3 alternativ, giltigt `ratt`, fördelning av rätta svar) och skriver `<namn>_elev.docx` och `<namn>_facit.docx` (+ PDF med `--pdf`) i samma mapp. Åtgärda alla fel och varningar och bygg om.

Granska sedan elev-PDF:en (Read-verktyget) innan du lämnar över: sidbrytningar, att inga rätta svar syns, att svarsraderna räcker. Om LibreOffice inte kan göra PDF (scriptet varnar), läs i stället texten ur Word-filerna med python-docx och kontrollera ordning och innehåll; läraren sparar PDF från Word.

### 6. Lämna över till läraren
Berätta kort: kapitel, antal frågor per del, totalpoäng, var filerna ligger, och om något i kapitlet var svårläst i skanningen.
