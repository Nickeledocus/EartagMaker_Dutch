# Oormerk Maker / Dutch Eartag Maker

> **NL** – Maak realistische Nederlandse rundveeoormerken in je browser, zodat je kunt testen zonder fysieke oormerken.
> **EN** – Generate realistic Dutch bovine ear tags in your browser, so you can test without physical ear tags at hand.

**Versie / Version:** V0.2 (03-09-2026) · **Licentie / License:** MIT

[Nederlands](#nederlands) · [English](#english)

---

## Nederlands

### Waarom dit bestaat

Sinds 2026 zijn er nieuwe 12-cijferige oormerken in omloop, maar er zijn onvoldoende fysieke voorbeelden om mee te testen. Deze tool tekent een oormerk na — inclusief scanbare barcode — zodat je scanners, invoerschermen en verwerkingsprocessen kunt uittesten zonder dat er een koe in de buurt hoeft te staan.

### Wat het is

Eén los HTML-bestand. HTML staat voor *HyperText Markup Language*, de taal waarin webpagina's geschreven zijn. Er is geen server nodig, geen installatie en geen internetverbinding: je dubbelklikt het bestand en het opent in je browser. Je kunt het net zo goed op een netwerkschijf of in SharePoint zetten en zo delen.

### Aan de slag

1. Download `OormerkMaker.html`.
2. Dubbelklik het bestand (of: rechtermuisknop → Openen met → Chrome/Edge/Firefox).
3. Vul de velden in, klik **Genereer oormerk** en download de afbeelding.

Bij het openen wordt er direct een voorbeeldoormerk getekend, zodat je meteen ziet wat je krijgt.

### De velden

| Veld | Wat het doet |
|---|---|
| **Volledig levensnummer** | Snelinvoer. Typ hier het hele nummer en klik op **Verdeel over velden**; de tool vult de losse velden hieronder voor je in. |
| **Landcode** | Staat linksboven, op dezelfde regel als het nummer boven de barcode. Standaard `NL`. |
| **Nummer boven de barcode** | Het kleinere nummer naast de landcode. |
| **Barcode-inhoud** | Wat de scanner daadwerkelijk uitleest. Dit hoeft niet gelijk te zijn aan wat er in tekst op het merk staat — handig om foutafhandeling te testen. |
| **Nummer onder de barcode** | Het grote nummer dat je van veraf leest (in de wei). |
| **Controlegetal** | Het kleine cijfer rechtsboven het grote nummer. |
| **Tekst op de lip** | Vrije tekst op het ronde bevestigingslipje. Leeglaten = weglaten. |

#### Hoe "Verdeel over velden" rekent

De tool pakt de letters aan het begin als landcode (geen letters gevonden? dan `NL`), en alle cijfers als barcode-inhoud. Van die cijfers wordt het **laatste cijfer** het controlegetal, de **vier cijfers daarvóór** het grote nummer, en alles wat er dan nog vóór staat het nummer boven de barcode. Er zijn minimaal zes cijfers nodig.

Voorbeeld met `NL538037637`:

| Onderdeel | Waarde |
|---|---|
| Landcode | `NL` |
| Boven de barcode | `5380` |
| Barcode-inhoud | `538037637` |
| Onder de barcode | `3763` |
| Controlegetal | `7` |

> Een controlegetal werkt zoals het totaalbedrag onderaan een factuur: het voegt zelf geen nieuwe informatie toe, maar als het niet klopt met de rest weet je dat er onderweg iets fout is gegaan.

### Barcodetypes

**Code 128** — een dichte, moderne barcode. De tool kiest zelf de beste variant:

- **Code 128C** als de invoer alleen cijfers bevat én een even aantal cijfers heeft. Deze variant propt twee cijfers in één symbool en is dus korter.
- **Code 128B** in alle andere gevallen. Deze kan ook letters en leestekens aan.

**Code 39** — een ouder, breder formaat dat je nog veel in bestaande installaties tegenkomt. Ondersteunt cijfers, hoofdletters en een handvol leestekens. De tool zet de invoer automatisch om naar hoofdletters en plakt er de verplichte `*`-tekens omheen.

Onder de afbeelding zie je welke variant gekozen is en uit hoeveel modules (de smalste streepjes-eenheid) de barcode bestaat.

> Code 128C tegenover Code 128B is als `VARCHAR` tegenover `NVARCHAR`: het smallere formaat past minder soorten tekens, maar wat er wél in past neemt minder ruimte in.

### Exporteren

- **PNG** — *Portable Network Graphics*, een gewone rasterafbeelding (opgebouwd uit pixels). Kies eerst een schaal van 1 tot 4; bij schaal 3 krijg je 1320 × 1665 pixels. Handig voor Word, e-mail of Confluence.
- **SVG** — *Scalable Vector Graphics*, een afbeelding die als tekeninstructies is opgeslagen in plaats van als pixels. Blijft scherp op elk formaat en is dus beter als het merk daadwerkelijk geprint wordt.

Voor scannen op een beeldscherm werkt schaal 3 of 4 het beste; bij schaal 1 zijn de streepjes vaak te dun voor de camera.

### Zelf aanpassen

Bovenin het `<script>`-blok staan een paar duidelijk gemarkeerde constanten die je kunt wijzigen zonder de rest van de code te snappen:

| Constante | Betekenis |
|---|---|
| `LETTERTYPE_OORMERK` | Het lettertype op het merk zelf. Alleen lettertypen die op de computer geïnstalleerd staan werken; zet reservenamen erachter, gescheiden door komma's. |
| `KLEUREN` | De kleurcombinaties. Voeg een regel toe en zet dezelfde naam ook in de keuzelijst `<select id="kleur">` in de HTML erboven. |
| `MAAT_BOVENREGEL` | Maximale lettergrootte van de bovenste regel; wordt automatisch kleiner bij lange nummers. |
| `MAAT_GROOT` | Lettergrootte van het grote nummer. |
| `MAAT_CONTROLE` | Lettergrootte van het controlegetal. |
| `MAAT_LIP` | Lettergrootte van de tekst op de lip. |
| `SILHOUET` | De vorm van het merk zelf (een SVG-pad). Alleen aankomen als je weet wat je doet. |

De kleuren van het bedieningsscherm zelf staan los daarvan, bovenin het `<style>`-blok onder `:root`.

### Beperkingen

- Alleen de Nederlandse indeling; andere landen staan op de wensenlijst.
- De verdeling over de velden is afgestemd op het gangbare NL-formaat en is nog niet voor álle NL-varianten gecontroleerd.
- Dit is een testhulpmiddel. De gegenereerde merken zijn geen officiële identificatie en horen niet aan een dier.
- Uitsluitend voor rundvee en vergelijkbaar landbouwhuisdier. Vogels vallen buiten scope: die zijn vanuit de fabriek al voorzien van ingebouwde apparatuur die rapporteert aan een hogere instantie, dus een extra merk zou dubbelop zijn.

### Wensenlijst

- Verdeling over de velden controleren voor alle NL-formaten
- Ondersteuning voor meerdere landen

### Wijzigingen

| Datum | Versie | Wat |
|---|---|---|
| 01-09-2026 | V0.1 | Aangemaakt |
| 03-09-2026 | V0.2 | Kleine aanpassingen doorgevoerd |

---

## English

### Why this exists

New 12-digit ear tags entered circulation in 2026, but there aren't enough physical samples to test with. This tool draws a look-alike ear tag — scannable barcode included — so you can exercise scanners, entry screens and downstream processing without needing an actual cow nearby.

### What it is

A single standalone HTML file. HTML stands for *HyperText Markup Language*, the language web pages are written in. No server, no installation, no internet connection required: double-click the file and it opens in your browser. It works just as well from a network drive or SharePoint.


### Getting started

1. Download `OormerkMaker.html`.
2. Double-click it (or: right-click → Open with → Chrome/Edge/Firefox).
3. Fill in the fields, click **Genereer oormerk** ("Generate ear tag") and download the image.

A sample tag is drawn automatically on load, so you see the result immediately.

> The interface is in Dutch, matching the domain it's used in. The field table below doubles as a translation key.

### The fields

| Field (Dutch) | English | What it does |
|---|---|---|
| **Volledig levensnummer** | Full life number | Quick entry. Type the whole number here and click **Verdeel over velden** ("split across fields") to fill in the individual fields below. |
| **Landcode** | Country code | Top left, on the same line as the number above the barcode. Defaults to `NL`. |
| **Nummer boven de barcode** | Number above the barcode | The smaller number next to the country code. |
| **Barcode-inhoud** | Barcode content | What the scanner actually reads. It doesn't have to match the printed text — useful for testing error handling. |
| **Nummer onder de barcode** | Number below the barcode | The large number, readable from a distance across the field. |
| **Controlegetal** | Check digit | The small digit above and right of the large number. |
| **Tekst op de lip** | Lip text | Free text on the round mounting lip. Leave empty to omit. |

#### How the split works

The tool takes any leading letters as the country code (none found? then `NL`), and all digits as the barcode content. From those digits, the **last digit** becomes the check digit, the **four digits before it** become the large number, and whatever remains in front becomes the number above the barcode. At least six digits are required.

Example with `NL538037637`:

| Part | Value |
|---|---|
| Country code | `NL` |
| Above barcode | `5380` |
| Barcode content | `538037637` |
| Below barcode | `3763` |
| Check digit | `7` |

> A check digit works like the total at the bottom of an invoice: it adds no new information by itself, but if it doesn't agree with the rest you know something went wrong along the way.

### Barcode types

**Code 128** — a dense, modern barcode. The tool picks the best variant on its own:

- **Code 128C** when the input is digits only and has an even length. This variant packs two digits into one symbol, so it comes out shorter.
- **Code 128B** in every other case. It handles letters and punctuation too.

**Code 39** — an older, wider format still common in existing installations. Supports digits, capital letters and a handful of punctuation marks. The tool uppercases the input automatically and wraps it in the required `*` characters.

Below the image you'll see which variant was used and how many modules (the narrowest bar unit) the barcode consists of.

> Code 128C versus Code 128B is like `VARCHAR` versus `NVARCHAR`: the narrower format accepts fewer kinds of characters, but what does fit takes up less room.

### Exporting

- **PNG** — *Portable Network Graphics*, an ordinary raster image (made of pixels). Pick a scale from 1 to 4 first; scale 3 gives you 1320 × 1665 pixels. Good for Word, email or Confluence.
- **SVG** — *Scalable Vector Graphics*, an image stored as drawing instructions rather than pixels. Stays sharp at any size, so it's the better choice if the tag will actually be printed.

For scanning off a screen, scale 3 or 4 works best; at scale 1 the bars are often too thin for the camera.

### Customising

Near the top of the `<script>` block are a few clearly marked constants you can change without understanding the rest of the code:

| Constant | Meaning |
|---|---|
| `LETTERTYPE_OORMERK` | The font used on the tag itself. Only fonts installed on the machine will work; list fallbacks after it, comma-separated. |
| `KLEUREN` | The colour combinations. Add a line here and add the same name to the `<select id="kleur">` dropdown in the HTML above. |
| `MAAT_BOVENREGEL` | Maximum font size of the top line; shrinks automatically for long numbers. |
| `MAAT_GROOT` | Font size of the large number. |
| `MAAT_CONTROLE` | Font size of the check digit. |
| `MAAT_LIP` | Font size of the lip text. |
| `SILHOUET` | The shape of the tag itself (an SVG path). Only touch this if you know what you're doing. |

The colours of the interface itself are separate, at the top of the `<style>` block under `:root`.

### Limitations

- Dutch layout only; other countries are on the wish list.
- The field split targets the common NL format and hasn't been verified against every NL variant yet.
- This is a testing aid. Generated tags are not official identification and do not belong on an animal.
- For cattle and comparable livestock only. Birds are out of scope: they ship from the factory with built-in equipment already reporting to a higher authority, so an extra tag would be redundant.

### Wish list

- Verify the field split for all NL formats
- Support for multiple countries

### Changelog

| Date | Version | What |
|---|---|---|
| 01-09-2026 | V0.1 | Created |
| 03-09-2026 | V0.2 | Minor adjustments |

---

## Licentie / License

MIT — © 2026 Nick Scheffers. Zie / see [LICENSE](LICENSE).