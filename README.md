# Plaza Marketplace + UbicaPTY

A commercial real estate platform for finding and evaluating retail spaces in Panama City's shopping plazas.

**Live Site:** https://plaza-marketplace.vercel.app
**Access Code:** `0010`

---

## What is this?

Plaza Marketplace is an interactive platform that helps entrepreneurs and businesses find the perfect commercial space in Panama City. It combines:

1. **Plaza Marketplace** - A business intelligence tool that analyzes shopping plazas based on tenant mix, foot traffic, competition, and zone characteristics
2. **UbicaPTY** - An interactive Google Maps integration showing real locations of commercial spaces

---

## The Problem We Solve

Finding commercial real estate in Panama is fragmented and opaque:
- Information is scattered across multiple brokers
- No easy way to compare plazas
- Hard to evaluate if a location is good for your specific business type
- No visibility into competition or complementary businesses

---

## Key Features

### 1. Interactive Map (UbicaPTY)
- **Google Maps integration** with satellite view of Panama City
- **20+ commercial plazas** with real coordinates
- **Zone-based markers** - hover to see individual plazas
- **Search** - Find plazas by name, zone, or price range
- **POI Filters** - Show nearby restaurants, banks, transport, hospitals, etc.
- **Competition Search** - Find locations of major chains (Riba Smith, Arrocha, McDonald's, etc.)

### 2. Business Evaluation Tool
Answer 4 questions and get personalized plaza recommendations:
1. What type of business do you want to open?
2. What's your budget?
3. What size space do you need?
4. Which zones are you interested in?

The algorithm scores each plaza based on:
- **Anchor tenants** that drive foot traffic to your business
- **Competition** - existing businesses in the same category
- **Zone characteristics** - residential vs office, purchasing power, growth
- **Plaza type** - neighborhood, community, or lifestyle center

### 3. Opportunities Explorer
Quick view of which plazas are best for each business type:
- Shows open opportunities (no competition)
- Flags existing competition
- Ranks by score with detailed reasoning

### 4. Plaza Profiles
Detailed information for each plaza:
- Available spaces with size and pricing
- Current tenant mix
- Zone demographics
- WhatsApp contact for inquiries

### 5. Admin Dashboard (Demo)
Shows what plaza administrators see:
- Inquiry statistics
- Which business types are most in demand
- Lead management

---

## How the Scoring Algorithm Works

When you select a business type, each plaza is scored (0-100) based on:

```
Base Score = (Anchor Tenants × 22) + (Available Spaces × 8) + (Traffic Level × 6)

Bonuses:
+ Has complementary anchor tenants (supermarket, pharmacy, gym)
+ No direct competition in plaza
+ Plaza type matches business needs
+ Residential area for neighborhood services
+ High purchasing power zone
+ High growth zone

Penalties:
- Direct competition exists (-25 to -100)
- Competition in nearby zones
- Low visibility location
- High vacancy rate
```

### Anchor Tenant Logic
Different businesses benefit from different anchors:
- **Café** → Benefits from: Supermarket, Gym, Bank, Office buildings
- **Pharmacy** → Benefits from: Supermarket, Clinic, Gym
- **Restaurant** → Benefits from: Cinema, Retail stores, Banks

---

## Technical Architecture

### Stack
- **Frontend:** Vanilla HTML/CSS/JavaScript (single-file SPA)
- **Maps:** Google Maps JavaScript API with Advanced Markers
- **Hosting:** Vercel (auto-deploys from GitHub)
- **Data:** Static JSON embedded in HTML

### File Structure
```
MarketPlaza/
├── index.html                 # Main application (deployed)
├── app/
│   ├── index.html            # Same as root (backup)
│   ├── README.md             # App-specific docs
│   └── src-con-placeholders.html
├── ubicapty/
│   ├── index.html            # Original map application
│   ├── reporte-ubicapty.html
│   └── UbicaPTY-Reporte.pdf
└── Plaza Marketplace - Plan de Negocio.docx
```

### Google Maps Integration

**API Key:** Configured in code
**Map ID:** Required for Advanced Markers
**Libraries:** `marker`, `places`

```javascript
// Map initialization
gmap = new google.maps.Map(element, {
  center: { lat: 9.0, lng: -79.52 },  // Panama City
  zoom: 12,
  mapId: GOOGLE_MAP_ID,
  mapTypeId: 'hybrid'  // Satellite with labels
});
```

### Data Structure

**Plazas:**
```javascript
{
  id: "multiplaza",
  nombre: "Multiplaza Pacific Mall",
  zona: "Punta Pacífica",
  lat: 8.9897,
  lng: -79.5117,
  tipo: "Lifestyle",        // Vecinal, Comunitaria, Lifestyle
  trafico: 3,               // 1-3 scale
  estac: 2000,              // Parking spots
  tenants: [
    { n: "Zara", cat: "Moda" },
    { n: "Starbucks", cat: "Café" }
  ],
  locales: [
    { id: "L-245", m2: 120, precio: 85, nivel: "2", frente: "interior" }
  ]
}
```

**Zones:**
```javascript
ZONA_INFO = {
  "San Francisco": "mixta",      // residencial, oficinas, mixta
  "Costa del Este": "residencial",
  "Obarrio": "oficinas"
}

ZONA_PODER = {
  "Punta Pacífica": "alto",      // alto, medio-alto, medio
  "El Dorado": "medio"
}

ZONA_CRECIMIENTO = {
  "Costa del Este": "alto",       // alto, medio, bajo
  "Bella Vista": "bajo"
}
```

---

## Zones Covered

| Zone | Character | Purchasing Power | Growth |
|------|-----------|------------------|--------|
| San Francisco | Mixed | High | Stable |
| Costa del Este | Residential | High | High |
| Punta Pacífica | Mixed | High | Stable |
| Obarrio | Offices | High | Stable |
| El Dorado | Mixed | Medium | Stable |
| Condado del Rey | Residential | Medium | High |
| Brisas del Golf | Residential | Medium | High |
| Vía España | Mixed | Medium-High | Stable |
| Albrook | Mixed | Medium | Stable |

---

## Local Development

1. Clone the repository:
```bash
git clone https://github.com/josephmilhem4-sketch/MarketPlaza.git
cd MarketPlaza
```

2. Open in browser:
```bash
open index.html
# Or use a local server:
python -m http.server 8000
```

3. Access at `http://localhost:8000`

### Google Maps API Setup

To use your own API key:

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a project and enable:
   - Maps JavaScript API
   - Places API
3. Create an API key
4. Create a Map ID (for Advanced Markers)
5. Update in code:
```javascript
const GOOGLE_MAPS_API_KEY = 'your-api-key';
const GOOGLE_MAP_ID = 'your-map-id';
```

---

## Deployment

The site auto-deploys to Vercel when you push to the `main` branch.

Manual deploy:
```bash
vercel --prod
```

---

## Business Categories Supported

The platform analyzes 20+ business types:
- Farmacia (Pharmacy)
- Café
- Restaurante
- Gimnasio (Gym)
- Veterinaria
- Salón de belleza
- Barbería
- Lavandería
- Clínica
- Ferretería
- Óptica
- Panadería
- Pet shop
- Academia
- Comida rápida
- Coworking
- Licorería
- Moda (Fashion)
- Bar
- Entretenimiento

---

## Competition Database

Built-in locations for major Panama chains:

**Supermarkets:**
- Riba Smith (8 locations)
- Super 99 (10 locations)
- Rey (5 locations)
- El Machetazo (5 locations)

**Pharmacies:**
- Farmacias Arrocha (13 locations)
- Farmacias Metro (5 locations)

**Retail:**
- Melo (5 locations)
- Do It Center (3 locations)
- Novey (5 locations)
- Conway (3 locations)

**Fast Food:**
- McDonald's (10 locations)
- KFC (5 locations)

---

## Future Roadmap

- [ ] Real-time availability from plaza administrators
- [ ] User accounts and saved searches
- [ ] Inquiry tracking system
- [ ] Mobile app
- [ ] More plazas and zones
- [ ] Integration with property management systems

---

## Credits

- **Plaza Marketplace** - Business intelligence and evaluation system
- **UbicaPTY** - Interactive map integration
- **Data** - Illustrative/demo data (not real availability)

---

## License

Private project - All rights reserved.

---

## Contact

For inquiries about listing your plaza or partnership opportunities, use the contact form on the site.
