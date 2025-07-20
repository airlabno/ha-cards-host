# ha-cards-host

Dette prosjektet er et eksternt GitHub Pages-repo som hoster JavaScript-filer (kort) for Home Assistant, typisk installert via HACS. Dette er nødvendig fordi Home Assistant-instansen kjører via Cloudflare Tunnel uten lokal tilgang, og `/local/`-mappen ikke er tilgjengelig offentlig.

## 📌 Formål

Gi Home Assistant mulighet til å laste inn tilpassede kort (custom cards) via `https://ha-cards.airlab.no/` uten krav om lokal filtilgang eller proxy-regler.

## 🔧 Løsning

* JS-filer fra `/config/www/community` i Home Assistant synkes til dette repoet.
* Kortene plasseres i `public/`-mappen og eksponeres som statiske filer via GitHub Pages.
* Filene brukes i Home Assistant via URL-er som:

```yaml
resources:
  - url: https://ha-cards.airlab.no/mushroom.js
    type: module
```

## 🧪 Eksempelbruk i Lovelace

```yaml
type: custom:mushroom-light-card
entity: light.stue
show_brightness_control: true
fill_container: true
layout: horizontal
```

## 📁 Struktur

```
public/
├── mushroom.js
├── button-card.js
├── apexcharts-card.js
├── ...
```

## 🛠 Oppdatering av kort

### Manuell

1. Last ned `.js`-filer fra Home Assistant:

   ```bash
   cp /config/www/community/*/*.js ~/ha-cards-host/public/
   ```

2. Commit og push til repoet:

   ```bash
   git add .
   git commit -m "Oppdatert kort"
   git push
   ```

### Automatisk (foreslått senere)

* Via GitHub Actions eller shell\_command i Home Assistant
* Kan trigges ved oppstart, etter HACS-oppdatering eller etter fast intervall

## 🌐 Hosting

* Repo deployes via GitHub Pages
* Eget underdomene satt opp: `ha-cards.airlab.no`
* Ingen proxy, CDN eller tilpasning trengs – direkte lastet fra GitHub Pages

## ✅ Status

| Komponent                 | Status       |
| ------------------------- | ------------ |
| GitHub Pages aktivert     | ✅            |
| DNS (Cloudflare) satt opp | ✅            |
| mushroom.js lastes inn    | ✅            |
| Kort vises i UI           | ✅            |
| Automatisert sync         | ⚠️ planlegges |

## 📄 License

Følger lisensene til kortene du inkluderer. Dette repoet inneholder kun distribuerte `.js`-filer for bruk i Home Assistant.

## 📝 Forbedringer

* Automatisert sync av `.js`-filer fra Home Assistant
* 
