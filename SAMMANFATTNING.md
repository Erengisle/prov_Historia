# Prov i historia – läget just nu

Senast uppdaterad 2026-10-02. Kan klistras in i en annan tråd eller läggas som kunskap i ett Claude-projekt.

## Vad som finns

- **Skillen `skapa-prov`** (i repot `Erengisle/prov_Historia`, grenen `claude/awesome-pasteur-ozn5b1`). Den gör kapitelprov utifrån inskannade bokkapitel.
- **Ett prov på *Det långa 1800-talet*** i två versioner, en för varje läroplan:
  - `prov/det-langa-1800-talet-gy25/` – Gy-25-boken, s. 84–113
  - `prov/det-langa-1800-talet-gy11/` – Gy-11-boken, s. 74–99
  - Samma frågor i båda. Bedömningsstödet följer respektive läroplan.

## Beslut

**Provets upplägg**
1. Välj rätt alternativ: 12–15 flervalsfrågor, 3 alternativ var.
2. Förklara begrepp med egna ord: 4–5 begrepp.
3. En kortare skrivfråga (cirka 8 rader).
4. En eller två längre skrivfrågor (cirka en sida), där historiska begrepp ska användas.

Svaren blir alltså längre och längre genom provet. Ingen tidslinje än.

**Innehåll**
- Allt ska gå att besvara med kapitlet.
- Flervals- och begreppsfrågor bygger bara på brödtexten. Fördjupningsrutorna (Källor, Historiebruk, Debatt, porträtt och temarutor) är inte säkert lästa.
- En skrivfråga får utgå från en fördjupning bara om frågan själv ger bakgrunden. Facit markerar det.

**Läroplaner**
- Gy-11 och Gy-25 blandas aldrig.
- Varje kapitel och prov märks med utgåva. Kursplanerna ligger i `kursplan-gy11.md` och `kursplan-gy25.md`.

**Mål-id** är desamma som på kriteriesidan (fliken Provet) och i bedömningsskillen `historia-bedomning`:
- Gy25: 1a, 1b, 2, 3, 4
- Gy11: 1a–1e, 2, 3a, 3b, 4a, 4b

Det centrala innehållet är numrerat CI1, CI2 osv.

**Språknivå:** som i läroboken. Facit använder kriteriernas ord.

## Filer som skapas för varje prov

| Fil | Till vad |
|---|---|
| `…_elev.docx` | Pappersprovet. |
| `…_facit.docx` | Rätta svar, rättningsnyckel och modellsvar. För skrivfrågorna också vad ett bra svar tar upp och bedömningsstöd E/C/A. Överst en översikt över vilka mål och vilket centralt innehåll varje del prövar. |
| `…_trelson.docx` / `.txt` | En fråga per block med löpande nummer (1–23), utan kryssrutor, för att kopiera in i Trelson. |
| `…_uppgift.txt` | Uppgiftsfil för bedömningsskillen `historia-bedomning`. Läggs i Drive-mappen *Historia 1b – uppgifter*. |
| `prov.json` | Hela provet i strukturerad form. Allt annat byggs från den. |

Frågenumren är desamma i Trelson-filen, facit och uppgiftsfilen.

## Arbetsdelning mellan skillarna

- **`skapa-prov`** (Claude Code, i repot) gör proven och uppgiftsfilerna.
- **`historia-bedomning`** (claude.ai) bedömer elevsvar mot uppgiftsfilen och ger lärarunderlag och elevåterkoppling.

## Öppna frågor

- **Trelson:** hur tar den emot frågor (uppladdning eller kopiering), och kan den rätta flervalsfrågor själv? Läraren kollar.
- **Trelson-export:** vilket format får elevsvaren (en fil per elev eller en samlad fil)? Det styr hur rättningen läser in svaren.
- **Uppgiftsfilerna** ligger inte i Drive än.
- **Ej prövat i det här provet:** källkritik (Gy25 mål 3, Gy11 3a/3b) och Gy11 1e. Läraren vill inte lägga till det nu.
- **PDF:** kan inte göras i molnmiljön. Spara som PDF från Word.
