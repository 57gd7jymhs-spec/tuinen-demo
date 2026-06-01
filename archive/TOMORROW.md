# Handoff — AD Groenservice Website Ombouw

> **Voor Claude:** Lees dit eerst volledig voordat je iets doet.
> Zeg aan het begin van de sessie: "ik heb TOMORROW.md gelezen" zodat de gebruiker weet dat je de context hebt.

---

## Wat is dit project?

Dit is een **cloon van het Dropwork loodgieterstemplate** dat omgebouwd wordt naar een volledige website voor **AD Groenservice** — een Belgisch tuinonderhoudsbedrijf (Nederlandstalig).

De map staat op: `C:\Users\Apollo\Desktop\Buissensis\websites\ad-groenservice-new`

---

## Wat is al gedaan (sessie 26 mei 2026)

### ✅ AI chatbot — volledig omgezet naar tuindiensten
- `api/chat.js` — systeem-prompt herschreven voor AD Groenservice (diensten, prijzen, tone, placeholders)
- `index.html` — chatbot widget volledig bijgewerkt:
  - Header: "AD Groenservice Assistent"
  - 5 snelkoppelingen: ⛈️ Stormschade / 🌿 Diensten & prijzen / 📍 Bereikbaarheid / 📅 Afspraak & offerte / 🏡 Over ons
  - Prijschips: Gazon / Heg & struiken / Boomverzorging / Tuinaanleg / Anders
  - Intent-patronen: tuinspecifieke zoekwoorden
  - AI-model: llama-3.3-70b-versatile via Groq

### ✅ Vercel deployment
- **Live URL:** https://ad-groenservice-new.vercel.app
- **Vercel project:** ad-groenservice-new (team: 57gd7jymhs-specs-projects)
- `GROQ_API_KEY` is ingesteld als environment variable op Vercel
- Opnieuw deployen: `vercel --prod --yes` vanuit de projectmap

### ✅ CONTENT.md aangemaakt
- Volledige Nederlandstalige teksten voor elke sectie
- 6 diensten met beschrijvingen en indicatieve prijzen
- 20 FAQ's in het Nederlands
- Reviews-templates, CTA-varianten
- Media checklist (welke foto's/video's te verzamelen)
- Kleurpalet-suggesties (blauw → groen)
- Zoek op `[PLACEHOLDER]` om alles te vinden dat nog ingevuld moet worden

---

## Wat er morgen moet gebeuren

### De hoofdtaak
De gebruiker geeft een **nieuwe volledige template/site** als basis.
Die template moet volledig omgebouwd worden naar AD Groenservice.

### Stap-voor-stap aanpak
1. **Ontvang de nieuwe template** van de gebruiker
2. **Lees CONTENT.md** — alle teksten staan al klaar in het Nederlands
3. **Vervang alle Dropwork/loodgieters content** door AD Groenservice/tuin content
4. **Kopieer de chatbot** van de huidige versie (`api/chat.js` + widget in `index.html`) naar de nieuwe template
5. **Stel de placeholders in** (zie tabel hieronder)
6. **Deploy op Vercel** (hergebruik hetzelfde project of maak nieuw aan)

### Placeholders om in te vullen
Zoek in CONTENT.md op `[PLACEHOLDER]` voor de volledige lijst. De belangrijkste:

| Placeholder | Beschrijving |
|---|---|
| `[TELEFOONNUMMER]` | Echt telefoonnummer van AD Groenservice |
| `[EMAIL]` | Contactmailadres |
| `[STAD]` | Hoofdvestiging |
| `[SERVICEGEBIED]` | Volledig werkgebied |
| `[ZAAKVOERDER]` | Naam eigenaar |
| `[BTW_NUMMER]` | BTW-nummer |
| `[AANTAL_KLANTEN]` | Aantal klanten (bv. 450+) |
| `[OPRICHTINGSJAAR]` | Jaar van oprichting |

---

## Belangrijke aandachtspunten

### GitHub — NIET pushen
- De remote `origin` wijst naar `github.com/57gd7jymhs-spec/dropwork-plumber-template`
- Dat is het originele Dropwork loodgieterstemplate — dit mag **niet overschreven worden**
- De wijzigingen van 26 mei zijn **niet gepusht** — GitHub is nog intact
- Maak voor de nieuwe site een **nieuw GitHub repo** aan, of push nergens

### Groq API key
- Staat veilig als environment variable op Vercel
- Nooit in de code schrijven
- Model: `llama-3.3-70b-versatile`

### Visuele stijl
- Het huidige palet is blauw/marine (loodgieters-stijl)
- Voor AD Groenservice: overschakelen naar groen (zie CONTENT.md sectie "Kleurpalet")
- CSS-variabelen staan in de `<style>` tag van `index.html` — één aanpassing schakelt alles om

### Beeldmateriaal
- Huidige site gebruikt Pexels-stockvideo's van loodgieter — vervangen door tuinvideo's
- Zie CONTENT.md "Media Checklist" voor wat te verzamelen
- Voor/na-foto's: echte tuinfoto's van AD Groenservice gebruiken

---

## Bestanden in dit project

| Bestand | Beschrijving |
|---|---|
| `index.html` | Volledige site (1800+ regels, vanilla HTML/CSS/JS) |
| `api/chat.js` | AI chatbot backend (Groq/Llama, serverless) |
| `CONTENT.md` | Alle websiteteksten in het Nederlands, kant-en-klaar |
| `TOMORROW.md` | Dit bestand — context voor volgende sessie |
| `CLAUDE.md` | Web design operating manual (niet aanpassen) |
| `images/` | Voor/na-foto's (loodgieter) — vervangen door tuinfoto's |
| `.vercelignore` | Vercel upload-uitsluitingen |

---

## Snelle commando's

```bash
# Deployen naar Vercel (vanuit projectmap)
vercel --prod --yes

# Env var toevoegen
echo "waarde" | vercel env add NAAM production

# Git status bekijken
git status
git log --oneline -5
```

---

*Aangemaakt op 26 mei 2026 — einde van voorbereidingssessie.*
