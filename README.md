# NAMRON 4-Channel ZigBee Switch Blueprint for Home Assistant v2.5.2

## Oversikt

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fowanvik%2FNamron%2Fblob%2Fmain%2FNamron4512773.yml)

Dette er en omfattende og avansert Home Assistant blueprint for NAMRON 4-kanals ZigBee dimmerbryter. Blueprint'en gir full kontroll over lysenheter med mange avanserte funksjoner som gjør den til en av de mest kraftfulle switch-automatiseringene tilgjengelig.

![Bilde](https://i.imgur.com/UvvY9Ok.png)

### 🚀 Hovedfunksjoner

- **4 uavhengige kanaler**: Hver knapp kan kontrollere sin egen lysenhet
- **Avanserte dimmefunksjoner**: Hold inne knappen for gradvis dimming opp/ned
- **Override-handlinger**: Erstatt standardfunksjoner med egendefinerte handlinger
- **Multi-press deteksjon**: Double-press og triple-press funksjoner
- **Scene-integrasjon**: Direkte kontroll av Home Assistant-scener
- **Nattmodus**: Automatisk lavere lysstyrke på natta
- **Fargetemperatur**: Varm/kald lysstyring
- **Gruppe-kontroll**: Kontroller alle lys samtidig
- **Status-feedback**: Visuell tilbakemelding via andre enheter
- **Smart state management**: Husker siste innstillinger
- **Konfigurerbare innstillinger**: Juster delays, brightness steps og mer
- **ZHA-integrasjon**: Bruker ZigBee Home Automation events

### ⚠️ Viktig merknad om knappelayout

**NAMRON 4 Strip switch har knappene arrangert baklengs!** 

Sett fra venstre til høyre er knappene:
- **Button 4** (lengst til venstre)
- **Button 3** 
- **Button 2** 
- **Button 1** (lengst til høyre)

## Installasjon

### Forutsetninger

1. Home Assistant med ZHA-integrasjon aktivert
2. NAMRON 4-kanal ZigBee switch koblet til ZHA
3. Lysenheter som skal kontrolleres

### Trinn 1: Import Blueprint

1. Åpne Home Assistant
2. Gå til **Settings** → **Automations & Scenes** → **Blueprints**
3. Klikk **Import Blueprint**
4. Lim inn URL eller last opp `Namron4Channel.yml` filen
5. Klikk **Preview Blueprint** og deretter **Import Blueprint**

### Trinn 2: Finn Device ID

1. Gå til **Developer Tools** → **Events**
2. Skriv inn `zha_event` i "Listen to events" feltet
3. Klikk **Start Listening**
4. Trykk på en knapp på NAMRON-bryteren
5. Kopier `device_id` verdien fra event-dataene som vises

### Trinn 3: Opprett Helper Entities (valgfritt)

For avanserte funksjoner som automation toggle, opprett disse helper entities:

1. Gå til **Settings** → **Devices & Services** → **Helpers**
2. Klikk **Create Helper** → **Toggle**
3. Opprett: `input_boolean.namron_automation_disabled`
4. Navn: "NAMRON Automation Disabled"
5. Icon: `mdi:power`

### Trinn 4: Opprett Automation

1. Gå til **Settings** → **Automations & Scenes** → **Automations**
2. Klikk **Create Automation** → **Use Blueprint**
3. Velg "NAMRON 4 Channel ZigBee Switch v2.5.2"
4. Konfigurer innstillingene (se konfigurasjon under)

## Konfiguration

### Device Settings

- **Device ID**: Lim inn device_id fra ZHA event (obligatorisk)

### Light Settings

Velg lysenheten som skal kontrolleres av hver knapp:
- **Light Entity 1**: Lysenhet for knapp 1 (høyre)
- **Light Entity 2**: Lysenhet for knapp 2 
- **Light Entity 3**: Lysenhet for knapp 3
- **Light Entity 4**: Lysenhet for knapp 4 (venstre)

### Dimming Delays (valgfritt)

Juster forsinkelsen mellom dimming-trinn (standard: 500ms):
- **Dim Delay**: 0-1500ms per lysenhet

### Brightness Steps (valgfritt)

Kontroller hvor mye lysstyrken endres per trinn:
- **Brightness Step UP**: 1-100% økning (standard: 10%)
- **Brightness Step DOWN**: -100% til -1% reduksjon (standard: -10%)

### 🎯 Multi-Press Actions (nytt!)

Aktiver double-press og triple-press funksjoner:
- **Enable Double Press**: Slå på/av double-press deteksjon
- **Double Press Timeout**: Tidsvindu for deteksjon (200-1000ms)
- **Double Press Actions**: Definer handlinger for hver knapp ved double-press

### 🎭 Scene Integration (nytt!)

Kontroller scener i stedet for individuelle lys:
- **Use Scenes**: Aktiver scene-kontroll
- **Scene ON/OFF**: Velg scener for on/off for hver knapp

### 🌈 Advanced Light Settings (nytt!)

Forbedret lysstyring:
- **Enable Color Temperature**: Aktiver fargetemperatur-kontroll
- **Warm/Cool Color Temperature**: Sett varme/kalde lystemperaturer
- **Transition Time**: Myke overganger (0-10 sekunder)

### 💡 Status Feedback (nytt!)

Visuell tilbakemelding:
- **Enable Status Feedback**: Aktiver feedback via andre enheter
- **Feedback Entity**: LED strip, smart bulb, eller speaker for tilbakemelding
- **Success/Error Colors**: RGB-farger for suksess og feil

### 🌙 Time-based Settings (nytt!)

Automatisk nattmodus:
- **Enable Night Mode**: Automatisk lavere lysstyrke om natta
- **Night Start/End Time**: Tidsperiode for nattmodus
- **Night Brightness**: Maksimal lysstyrke om natta (1-50%)
- **Night Color Temperature**: Varmere lys om natta

### 🏠 Group Control (nytt!)

Kontroller flere lys samtidig:
- **Enable All Lights Control**: Aktiver gruppekontrroll
- **All Lights Group**: Gruppe eller area med alle lys
- **All Lights Trigger**: Hvordan utløse gruppekontroll
  - Hold Button 1 + 4 samtidig
  - Double press Button 1

### ⚙️ State Management (nytt!)

Avansert tilstandshåndtering:
- **Save Last State**: Husk siste lysstyrke/farger
- **Enable Automation Toggle**: Tillat midlertidig deaktivering
- **Automation Toggle Combo**: Knappekombinasjon for toggle
  - Triple press Button 4
  - Hold Button 1 + 2 samtidig

### Override Actions (avansert)

Erstatt standard lysoperasjoner med egendefinerte handlinger:

1. **Velg Override-modus**: 
   - **Default**: Bruker standard lysoperasjoner
   - **Override**: Bruker egendefinerte handlinger

2. **Definer handlinger** (kun i Override-modus):
   - **Press UP**: Handling når knappen trykkes opp
   - **Press DOWN**: Handling når knappen trykkes ned
   - **Hold UP**: Handling når knappen holdes inn (opp)
   - **Hold DOWN**: Handling når knappen holdes inn (ned)

## Bruk

### 🔥 Standard modus (Default)

- **Enkelt trykk opp**: Skru på lyset (100% lysstyrke eller nattmodus-lysstyrke)
- **Enkelt trykk ned**: Skru av lyset
- **Hold inne opp**: Dim lyset opp gradvis til maksimum (respekterer nattmodus)
- **Hold inne ned**: Dim lyset ned gradvis til minimum

### 🎯 Multi-Press funksjoner

- **Double press**: Utfør egendefinerte handlinger per knapp
- **Triple press Button 4**: Toggle automation on/off (hvis aktivert)

### 🎭 Scene modus

- **Enkelt trykk opp**: Aktiver "ON" scene
- **Enkelt trykk ned**: Aktiver "OFF" scene

### 🏠 Group Control

- **Hold Button 1 + 4 samtidig**: Kontroller alle lys i gruppen
- **Double press Button 1**: Toggle alle lys (alternativ metode)

### 🌙 Nattmodus (automatisk)

Når nattmodus er aktivert (f.eks. 22:00-06:00):
- Lysene skrus på med lavere lysstyrke (standard 10%)
- Varmere fargetemperatur for bedre søvn
- Dimming stopper ved nattmodus-grensen

### ⚙️ Automation Control

- **Triple press Button 4**: Deaktiver/aktiver hele automationen midlertidig
- **Visual feedback**: LED-tilbakemelding viser status (grønn=på, rød=av)

### Override modus

I override-modus kan du definere helt egne handlinger for hver knapp og operasjon. Dette kan inkludere:
- Kontroll av andre enheter (vifter, persienner, etc.)
- Aktivering av scener
- Sending av notifikasjoner
- Utføring av scripts
- Smart home-rutiner

## 💡 Setup Tips & Best Practices

### Første gangs oppsett
1. **Start enkelt**: Begynn med kun Light Settings konfigurert
2. **Test grunnleggende funksjoner** før du aktiverer avanserte features
3. **Aktiver funksjoner gradvis**: Legg til en ny funksjon om gangen
4. **Dokumenter innstillingene dine**: Skriv ned hva som fungerer best

### Anbefalte innstillinger
- **Transition Time**: 0.5-1.0 sekund for responsiv følelse
- **Night Brightness**: 5-15% avhengig av romtype
- **Double Press Timeout**: 400ms for best responsivitet
- **Brightness Steps**: 10% for balansert kontroll

### Kompatibilitet
✅ **Støttede lystyper**:
- Dimmbare LED-pærer
- Smart bulbs med fargetemperatur
- RGB+CCT lysenheter
- Lysgrupper og areas

⚠️ **Ikke anbefalt**:
- Ikke-dimmbare pærer (kan fungere, men uten dimming)
- Meget trege lysenheter (>2s responstid)

## Feilsøking

### Blueprint importeres ikke

- Kontroller at YAML-filen har riktig syntaks
- Sjekk at du har tilstrekkelige rettigheter i Home Assistant

### Automation virker ikke

1. **Kontroller Device ID**: Sjekk at device_id er korrekt fra ZHA events
2. **Verifiser lysenheter**: Kontroller at alle valgte lysenheter eksisterer og fungerer
3. **Test ZHA events**: Bruk Developer Tools → Events for å se om events sendes når du trykker på knappene

### Dimming fungerer ikke som forventet

- Juster **Dim Delay** verdiene (lavere = raskere, høyere = tregere)
- Endre **Brightness Step** verdier (mindre = finere kontroll, størr e = grovere)

### Multi-press funksjoner virker ikke

- Sjekk **Double Press Timeout** innstilling (prøv 300-500ms)
- Kontroller at du trykker raskt nok
- Deaktiver og reaktiver funksjonen

### Nattmodus aktiveres ikke

- Verifiser **Night Start/End Time** innstillinger
- Sjekk Home Assistant sin tidssone-innstilling
- Kontroller at **Enable Night Mode** er aktivert

### Scene-kontroll fungerer ikke

- Sjekk at valgte scener eksisterer og fungerer
- Test scenene manuelt først
- Verifiser **Use Scenes** innstilling

### Automation toggle virker ikke

- Opprett `input_boolean.namron_automation_disabled` helper
- Sjekk at **Enable Automation Toggle** er aktivert
- Test helper entity manuelt

### Ytelse og responsivitet

- Reduser **Transition Time** for raskere respons
- Øk **Double Press Timeout** hvis du har trege fingre
- Deaktiver ubrukte funksjoner for bedre ytelse

## 📋 Quick Reference Card

### Standard Knappefunksjoner
| Handling | Resultat |
|----------|----------|
| **Enkelt trykk ↑** | Skru på lys (100% eller nattmodus) |
| **Enkelt trykk ↓** | Skru av lys |
| **Hold ↑** | Dim opp gradvis |
| **Hold ↓** | Dim ned gradvis |
| **Double press** | Egendefinert handling |

### Spesialfunksjoner
| Kombinasjon | Resultat |
|-------------|----------|
| **Triple press Button 4** | Toggle automation on/off |
| **Hold Button 1+4** | Kontroller alle lys |
| **Double press Button 1** | Toggle alle lys (alternativ) |

### Nattmodus (automatisk)
| Tid | Oppførsel |
|-----|----------|
| **22:00-06:00** | Lavere lysstyrke + varm farge |
| **06:00-22:00** | Normal lysstyrke + kald farge |

## Versjonsoversikt

### v2.5.2
- ✅ Gjorde `feedback_entity` valgfri (`default: null`).
- ✅ Gjorde `all_lights_group` valgfri (`default: null`).
- 🛠️ Fikser feilen: `Message malformed: Missing input all_lights_group, feedback_entity`.

### v2.5.1
- ✅ Gjorde scene-felter valgfrie (`default: null`), slik at bare `device_id` er påkrevd.
- 🧩 Bedre førstegangsoppsett for brukere som ikke bruker scene-integrasjon.

### v2.5.0 - MAJOR UPDATE! 🎉
- ✨ **Multi-Press Detection**: Double/triple press funksjoner
- 🎭 **Scene Integration**: Direkte kontroll av Home Assistant scener
- 🌈 **Advanced Light Settings**: Fargetemperatur og smooth transitions
- 💡 **Status Feedback**: Visuell tilbakemelding via andre enheter
- 🌙 **Time-based Behavior**: Automatisk nattmodus med lavere lysstyrke
- 🏠 **Group Control**: Kontroller alle lys med knappekombinationer
- ⚙️ **State Management**: Smart tilstandshåndtering og automation toggle
- 🔧 **Enhanced Override Actions**: Kraftigere override-system
- 📚 **Comprehensive Documentation**: Fullstendig oppdatert dokumentasjon
- 🐛 **Bug Fixes**: Forbedret stabilitet og ytelse

### v2.0.0
- Komplett implementering av alle 4 kanaler
- Override actions funksjonalitet
- Forbedret dimming logikk med `until` betingelser
- Støtte for individuell konfigurasjon per kanal

### v1.0.0
- Grunnleggende implementering
- Standard lysoperasjoner
- Basis override-funksjonalitet

## 🤝 Bidra

Fant du en bug eller har forbedringsforslag? Vi setter stor pris på bidrag fra fellesskapet!

### 🐛 Rapporter Issues
- Beskriv problemet detaljert
- Inkluder Home Assistant versjon og device modell  
- Legg ved relevante log-filer
- Spesifiser hvilke innstillinger du bruker

### 💡 Forbedringsforslag
- Forklar nytten av forslaget
- Gi konkrete brukseksempler
- Vurder bakoverkompatibilitet

### 🔧 Pull Requests
- Test grundig før innsending
- Følg eksisterende kodestil
- Oppdater dokumentasjon ved behov
- Beskriv endringene tydelig

### 📞 Support
- Sjekk denne README først
- Søk i eksisterende issues
- Opprett ny issue med detaljer

## 📄 Lisens

Dette prosjektet er tilgjengelig under MIT-lisensen. Se LICENSE-filen for detaljer.

---

**⭐ Hvis du liker denne blueprinten, gi den en stjerne på GitHub!**

**🚀 Del gjerne med andre Home Assistant-entusiaster!**
