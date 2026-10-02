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
| `kapitel/` | Bokens kapitel, inskannade (PDF). Filnamnet anger utgåvan: `… Gy-11.pdf` eller `… Gy-25.pdf`. |
| `exempelprov/` | Lärarens tidigare prov. Visar stil, språknivå och upplägg. |
| `.claude/skills/skapa-prov/kursplan-gy11.md`, `kursplan-gy25.md` | Centralt innehåll (CI1, CI2 …) och betygskriterier med mål-id (varje mening märkt) för Gy-11 respektive Gy-25 (Historia nivå 1b). |
| `.claude/skills/skapa-prov/kriterier-gy11.json`, `kriterier-gy25.json` | Mål-id med korta namn – scriptet använder dem i facit och uppgiftsfilen. Mål-id är desamma som på lärarens kriteriesida (fliken Provet) och i bedömningsskillen `historia-bedomning`: Gy25 `1a, 1b, 2, 3, 4`; Gy11 `1a–1e, 2, 3a, 3b, 4a, 4b`. Hitta inte på egna nummer. |
| `prov/<namn>/` | Här hamnar nya prov: `prov.json`, `*_elev.docx`, `*_facit.docx`, `*_trelson.docx/.txt`. |

## Arbetsgång

### 1. Ta reda på underlaget
- Vilket kapitel/område? Hitta PDF:en i `kapitel/`. Finns den inte: fråga läraren, gissa inte innehållet.
- **Utgåva:** Läraren har boken i två utgåvor, Gy-11 och Gy-25. Finns kapitlet i båda och läraren inte sagt vilken: fråga. Använd kursplanen för samma utgåva (`kursplan-gy11.md` / `kursplan-gy25.md`). Saknas kursplanen för utgåvan: säg det till läraren och använd den som finns, och skriv det i överlämningen.
- Uppladdade filer hamnar ofta på `main`. Hämta in dem till arbetsgrenen (`git fetch` + merge) om de inte finns lokalt.
- Inskannade PDF:er saknar oftast textlager. Läs dem med Read-verktyget och `pages` (max 20 sidor per anrop) så att sidorna tolkas som bilder.
- Läs **hela** kapitlet. Anteckna: centrala begrepp, händelser med årtal, personer, orsaker och följder, samt vad kapitlet själv lyfter fram (rubriker, faktarutor, sammanfattningar, instuderingsfrågor).
- Titta på minst ett prov i `exempelprov/` för ton och svårighetsgrad om du inte redan gjort det i samtalet.

**Allt i provet ska gå att besvara med kapitlet.** Fråga aldrig om något som inte står där.

**Brödtext och fördjupningar.** Kapitlen innehåller fördjupningsrutor med annan färg eller ram och egen rubrik, ofta i versaler: *Källor*, *Historiebruk*, *Debatt*, porträtt (t.ex. Olympe de Gouges) och temarutor (t.ex. Det osmanska riket, Det habsburgska riket). Det är inte säkert att eleverna har läst dem. Rutor som bara sammanfattar brödtexten (t.ex. "…s konsekvenser", "…s resultat") och kapitelsammanfattningen räknas som brödtext.
- Flervalsfrågor och begrepp ska gå att besvara med **brödtexten**.
- En fritextfråga får utgå från en fördjupning bara om frågan själv ger den bakgrund som behövs, så att den som inte läst rutan ändå kan svara. Ange då rutan i fältet `fordjupning`, så syns det i facit.
- Är du osäker på om en ruta är en fördjupning: räkna den som fördjupning och nämn det i överlämningen.

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
- Fritextfrågorna ska ge eleven möjlighet att visa kunskaper enligt **betygskriterierna i kursplanen för rätt utgåva** (läs filen). Låt frågorna tillsammans täcka flera av kriteriernas områden, i mån av vad kapitlet ger stöd för. Använd områdena och progressionsorden i kursplanfilen för rätt utgåva – de skiljer sig mellan Gy-11 och Gy-25 (Gy-25: godtagbara → goda → mycket goda kunskaper, enkla → utvecklade → utvecklade och nyanserade resonemang). Ungefärliga områden:
  - förändringsprocesser, händelser och personer – förlopp, orsaker och konsekvenser
  - personers betydelse för skeenden
  - olika tolkningar (jämföra, förorda en, motivera)
  - samband mellan det förflutna och nutiden, och slutsatser om framtiden
  - historiska begrepp
  - källmaterial (om kapitlet innehåller källor, bilder eller citat)
  - historiebruk (hur historien har använts)
- Minst en fråga i del 4 ska kunna nå A-nivå: den ska öppna för jämförelser, flera samband, olika tolkningar eller en koppling till nutiden.
- Ange för varje fritextfråga:
  - `historiska_begrepp` – listan som står i frågan
  - `kriterier` – vilka mål frågan prövar, som mål-id: `["1a", "2"]` (se `kriterier-<utgåva>.json`)
  - `centralt_innehall` – vilka punkter i det centrala innehållet frågan hör till, som nummer: `["CI2", "CI6"]`
  - `innehall` – vad ett bra svar bör ta upp, punktlista med fakta från kapitlet
  - `vanliga_missforstand` – en eller två meningar om typiska fel eller brister i svaren (hamnar i uppgiftsfilen)
  - `bedomning` med nivåerna **E, C, A**, formulerad med kriteriernas progressionsord (se tabellen sist i kursplanfilen): *översiktligt → utförligt → utförligt och nyanserat*, *enkla → välgrundade → välgrundade och nyanserade slutsatser*, *med viss säkerhet → med säkerhet*, *enkla → komplexa exempel* osv. Gör texten konkret för just frågan: skriv vilka orsaker, samband eller jämförelser som krävs på respektive nivå.
- Ange `kriterier` och `centralt_innehall` (nummer) även för flervals- och begreppsdelen – oftast 1a (Gy11 även 1b) och de CI som kapitlet tar upp.
- Begreppsfrågor och flerval prövar främst E-nivå (redogöra översiktligt, använda begrepp). Det är fritextfrågorna som skiljer mellan E, C och A.

**Språk**: Svenska. Lägg frågorna på samma språknivå som läroboken i `kapitel/` (exempelproven kommer från en bok för åk 7–9, medan kapitlen kan vara från en gymnasiebok). Korta, tydliga meningar och inga onödigt svåra ord. Bedömningsstödet i facit får använda kriteriernas språk.

### 4. Skriv `prov/<namn>/prov.json`

`<namn>` t.ex. `det-langa-1800-talet-gy25` – ta med utgåvan i namnet. Format (fullständigt exempel: `exempel-prov.json` i den här skillens mapp):

```json
{
  "titel": "Kapiteltest 23",
  "rubrik_hoger": "Kapitel 23",
  "utgava": "Gy-25",
  "kursplan": "Gy-25, Historia nivå 1b",
  "kalla": "Fundament Historia 7–9, kapitel 23",
  "delar": [
    {"typ": "flerval", "instruktion": "Välj rätt alternativ.",
     "fragor": [{"fraga": "…?", "alternativ": ["….", "….", "…."], "ratt": 0, "poang": 1}]},
    {"typ": "begrepp", "instruktion": "Förklara kortfattat med egna ord.", "rader": 3,
     "begrepp": [{"term": "…", "facit": "…", "poang": 2}]},
    {"typ": "fritext", "fraga": "…", "rader": 8, "poang": 4,
     "historiska_begrepp": [], "kriterier": ["1a", "2"],
     "centralt_innehall": ["CI2"], "fordjupning": "Historiebruk: Paris (frivilligt fält)", "innehall": ["…"],
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
Scriptet kontrollerar JSON-filen (antal flervalsfrågor, 3 alternativ, giltigt `ratt`, fördelning av rätta svar) och skriver i samma mapp:
- `<namn>_elev.docx` – pappersprovet
- `<namn>_facit.docx` – facit, bedömningsstöd, rättningsnyckel för flervalsfrågorna och en översikt över vilka mål och vilket centralt innehåll (CI) varje del prövar
- `<namn>_uppgift.txt` – uppgiftsfil i formatet som skillen `historia-bedomning` läser (Uppgift / Läroplan / Mål som testas / Underlag / Fråga N med Mål, E, C, A, Vanliga missförstånd). Läraren kan lägga den i Drive-mappen *Historia 1b – uppgifter*. Frågenumren är desamma som i Trelson-filen.
- `<namn>_trelson.docx` och `.txt` – provet som en lista av enskilda frågor med löpande nummer (Fråga 1, 2, …), utan kryssrutor och skrivrader, för att kopiera in i Trelson. Flervalsalternativen har bokstäverna A–C. Begreppen blir en fråga var.
- PDF med `--pdf` (kräver LibreOffice).

Den löpande numreringen är densamma i Trelson-filen, i rättningsnyckeln och vid rättning av elevsvar. Åtgärda alla fel och varningar och bygg om.

Granska sedan elev-PDF:en (Read-verktyget) innan du lämnar över: sidbrytningar, att inga rätta svar syns, att svarsraderna räcker. Om LibreOffice inte kan göra PDF (scriptet varnar), läs i stället texten ur Word-filerna med python-docx och kontrollera ordning och innehåll; läraren sparar PDF från Word.

### 6. Lämna över till läraren
Berätta kort: kapitel och utgåva, vilken kursplan som använts, antal frågor per del, totalpoäng, var filerna ligger, och om något i kapitlet var svårläst i skanningen.
