# Prov i historia – läget just nu

Senast uppdaterad 2026-10-02. Kan klistras in i en annan tråd eller läggas som kunskap i ett Claude-projekt.

## Vad som finns

- **Skillen `skapa-prov`** (i repot `Erengisle/prov_Historia`, grenen `claude/awesome-pasteur-ozn5b1`). Den gör kapitelprov utifrån inskannade bokkapitel.
- **Ett prov på *Det långa 1800-talet*** i två versioner, en för varje läroplan:
  - `prov/det-langa-1800-talet-gy25/` – Gy-25-boken, s. 84–113
  - `prov/det-langa-1800-talet-gy11/` – Gy-11-boken, s. 74–99
  - Samma frågor i båda. Bedömningsstödet följer respektive läroplan.
  - 24 frågor i sex delar. Del 1–3 obligatoriska (flerval, begrepp, ideologifrågan), del 4–6 frivilliga (gatunamnen i Paris, franska revolutionen, Tysklands enande).
  - Historiebruket (Gy25 mål 4, Gy11 4a/4b) och Gy11 1c prövas bara i de frivilliga delarna. Elever som slutar efter del 3 behöver pröva dem på E-nivå vid ett annat tillfälle.

## Beslut

**Provets upplägg**
1. Välj rätt alternativ: 12–15 flervalsfrågor, 3 alternativ var.
2. Förklara begrepp med egna ord: 4–5 begrepp.
3. En kortare skrivfråga (cirka 8 rader).
4. En eller två längre skrivfrågor (cirka en sida), där historiska begrepp ska användas.

Svaren blir alltså längre och längre genom provet. Ingen tidslinje än.

**Betygsnivåer per del**
- **Del 1–3 är obligatoriska** och kan tillsammans ge **E**. Del 3 (kortare skrivfråga) skrivs på E-nivå, så att eleven får visa förklaringar och enkla resonemang. Det klarar inte flerval och begreppsförklaringar ensamma.
- **Del 4 är frivillig** och ger möjlighet till **C och A**.
- Varje mål som prövas i del 1–3 ska också prövas i del 4. Annars kan eleven inte visa C eller A på det målet.
- Ett mål som bara prövas i del 4 bedöms inte hos elever som slutar efter del 3. Det är tillåtet, men byggscriptet säger till.
- Eleven börjar med de korta delarna. Det är tänkt som ett stöd för elever som inte känner sig starka.
- Provet anger tydligt vad varje del kan ge. Facit och uppgiftsfilen anger samma sak, så att `historia-bedomning` inte letar efter C-kvaliteter i del 1–3.

**Ofullständiga svar**
- Eleven behöver inte ha svarat på allt för att gå vidare eller skicka in. Inga frågor görs obligatoriska i Trelson eller Formulär.
- `historia-bedomning` **flaggar** i lärarunderlaget när svar saknas eller är ofullständiga i de obligatoriska delarna. Tomma svar i frivilliga delar flaggas inte.

**Innehåll**
- Allt ska gå att besvara med kapitlet.
- Flervals- och begreppsfrågor bygger bara på brödtexten. Fördjupningsrutorna (Källor, Historiebruk, Debatt, porträtt och temarutor) är inte säkert lästa.
- En skrivfråga får utgå från en fördjupning bara om frågan själv ger bakgrunden. Facit markerar det.
- Eleven ska inte behöva skriva samma sak flera gånger, särskilt inte i längre svar. Skrivfrågorna handlar om olika delar av kapitlet, och ett begrepp i del 2 får inte vara det som en skrivfråga ber eleven förklara.

**Läroplaner**
- Gy-11 och Gy-25 blandas aldrig.
- Varje kapitel och prov märks med utgåva. Kursplanerna ligger i `kursplan-gy11.md` och `kursplan-gy25.md`.

**Mål-id** är desamma som på kriteriesidan (fliken Provet) och i bedömningsskillen `historia-bedomning`:
- Gy25: 1a, 1b, 2, 3, 4
- Gy11: 1a–1e, 2, 3a, 3b, 4a, 4b

Det centrala innehållet är numrerat CI1, CI2 osv.

**Språknivå:** som i läroboken. Facit använder kriteriernas ord.

**Bedömning:** all bedömning, även av flervalsfrågorna, görs av `historia-bedomning`. Trelsons egen rättning behövs inte.

## Provet i Trelson (under test)

Trelson tar emot textfiler (skrivytan) och importerade Google Formulär. Tre format testas med några elever:

- **Kryss i hakparenteser** i skrivytan: `[ ] A. …` och eleven skriver `[X]`. Närmast pappersprovet.
- **Samlad svarsblankett** i skrivytan: alla flervalsfrågor först, sedan en tabell med Fråga och Svar.
- **Två moduler:** del 1–2 i Google Formulär (klick och korta svar), del 3–4 i skrivytan (långa svar). Läraren tror på det här alternativet.

Oavsett format får varje svar en fast rubrik (`Svar 1:`, `Svar 16:` …), så att skillen kan dela upp svaren per fråga. Instruktionen säger att rubrikerna inte får tas bort. Blanda inte frågor eller alternativ, så att numren stämmer med facit.

## Filer som skapas för varje prov

| Fil | Till vad |
|---|---|
| `…_elev.docx` | Pappersprovet. Överst står vilka delar som är obligatoriska och vad de kan ge. De frivilliga delarna börjar på en ny sida. |
| `…_facit.docx` | Rätta svar, rättningsnyckel och modellsvar. För skrivfrågorna också vad ett bra svar tar upp och bedömningsstöd, bara för de nivåer delen kan ge. Överst en översikt över vilka mål och vilket centralt innehåll varje del prövar. Varje del är märkt med obligatorisk/frivillig och högsta nivå. |
| `…_trelson.docx` / `.txt` | En fråga per block med löpande nummer (1–24 i provet om 1800-talet), grupperade per del, med en fast svarsrubrik (`Svar 1:` …) efter varje fråga och en instruktion till eleverna överst. Flervalsformatet kan ändras när testet är klart. |
| `…_uppgift.txt` | Uppgiftsfil för bedömningsskillen `historia-bedomning`. Listar delarna med högsta nivå, märker varje fråga med sin del och säger åt skillen att flagga saknade svar i de obligatoriska delarna. Läggs i Drive-mappen *Historia 1b – uppgifter*. |
| `prov.json` | Hela provet i strukturerad form. Allt annat byggs från den. Fälten `obligatorisk` och `hogsta_niva` per del är frivilliga; standard är del 1–3 obligatoriska (högst E) och resten frivilliga (upp till A). |

Frågenumren är desamma i Trelson-filen, facit och uppgiftsfilen.

## I Drive

Under *Historia → Hi1b*:
- **Historia 1b – uppgifter**: uppgiftsfilerna som Google-dokument, en per läroplan (*Det långa 1800-talet (Gy25)* och *(Gy11)*). Det är den mapp `historia-bedomning` letar i.
- **Prov – Det långa 1800-talet**: Trelson-frågorna som Google-dokument (samma för båda läroplanerna), plus elevprov och facit som Word och PDF.

## Arbetsdelning mellan skillarna

- **`skapa-prov`** (Claude Code, i repot) gör proven och uppgiftsfilerna. Byggscriptet varnar om ett mål bara prövas i delar som högst kan ge E.
- **`historia-bedomning`** (claude.ai) bedömer elevsvar mot uppgiftsfilen och ger lärarunderlag och elevåterkoppling. Den flaggar saknade svar.

## Öppna frågor

- **Trelson-format:** vilket av de tre formaten fungerar bäst för eleverna? Testas med några elever.
- **Trelson-export:** vilket format får elevsvaren (en fil per elev eller en samlad fil)? Det styr hur rättningen läser in svaren.
- **Ordning mellan moduler:** kan Trelson låsa så att del 1–2 görs först? Annars räcker en tydlig instruktion.
- **Att göra:** `historia-bedomning` ska flagga saknade svar och respektera högsta nivå per del. (`skapa-prov` är klar.)
- **Ej prövat i det här provet:** källkritik (Gy25 mål 3, Gy11 3a/3b) och Gy11 1e. Läraren vill inte lägga till det nu.
- **PDF:** byggscriptet gör nu PDF med `--pdf` när LibreOffice finns. Annars sparar läraren som PDF från Word.
