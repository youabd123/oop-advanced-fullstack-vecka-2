# Kravspecifikation

## Problemet, med kundens egna ord

”Vi är ett team på åtta personer som använder er uppgiftsapp varje dag.
Problemet är att vi missar deadlines hela tiden, och ingen märker det
förrän kunden ringer och är arg.”

Sara har också rapporterat följande problem:

”Appen säger att saker är försenade samma dag som de ska vara klara.
Klockan nio på morgonen står det att 'Skicka offert' är en dag sen,
fast den ska vara klar idag. Folk har slutat lita på listan.”

Kim har redan lagt till förfallodatum och endpointen
GET /api/todos/overdue. Det saknas tester för denna funktion.

## Mål, och hur vi vet att vi har nått dem (nuläge, mål, tidsram, hur vi mäter)

### Korrekt förseningsstatus

- Nuläge – uppgifter visas som försenade redan under förfallodagen.
- Mål – samtliga acceptanskriterier för korrekt förseningsstatus
  ska vara uppfyllda.
- Tidsram – innan PR:en med buggrättningen godkänns.
- Hur vi mäter – automatiserade tester kopplade till
  acceptanskriteriernas ID:n.

### Färre missade deadlines

- Nuläge – uppgift saknas i tillgängligt kundunderlag.
- Mål – behöver fastställas genom kundintervjun.
- Tidsram – behöver fastställas genom kundintervjun.
- Föreslagen mätmetod – antal uppgifter som slutförts senast
  på förfallodagen delat med alla uppgifter med förfallodatum
  under mätperioden, multiplicerat med 100.

Hur ändrade deadlines och avbrutna uppgifter ska räknas behöver
bestämmas innan mätningen genomförs.

## Frågor vi ställde, och svaren

Intervjuanteckningarna från måndagen behöver kompletteras.
Nedan finns kunduppgifter från ärendet och kursmaterialet.

### Kunduppgifter från underlaget

- Teamet består av åtta personer och använder appen dagligen.
- Missade deadlines upptäcks först när kunden hör av sig.
- Appen visar uppgifter som försenade under själva förfallodagen.
- I onsdagens kursmaterial säger Sara:
  ”Har jag sagt fredag så får det bli klart fredag kväll.”

Saras svar innebär att förfallodatumet gäller hela dagen.
Förfallodatumet ska därför vara ett datum utan klockslag.

### Frågor som återstår att besvara

- Vilken tidszon ska styra när förfallodagen har passerat?
- Hur stor andel av uppgifterna blir klara i tid idag?
- Vilken andel vill teamet nå och inom vilken tid?
- Hur använder teamet listan för att upptäcka och hantera förseningar?
- Vilka krav finns på svarstid och tillgänglighet?
- Behöver teamet påminnelser före deadline?

## User stories med acceptanskriterier (Givet/När/Så, med id)

### US-02 – Korrekt förseningsstatus

Som teammedlem vill jag se vilka uppgifter som är försenade,
så att jag kan prioritera arbetet och agera innan kunden hör av sig.

AK-2.1 och AK-2.2 bygger på buggrapporten och Saras datumregel.
AK-2.3–AK-2.5 är föreslagna preciseringar.
Vilken tidszon som ska gälla är fortfarande en öppen fråga.

- AK-2.1
  Givet en oavslutad uppgift med förfallodatum idag,
  när listan visas klockan 09.00 samma dag,
  så visas uppgiften inte som försenad.

- AK-2.2
  Givet en oavslutad uppgift med förfallodatum idag,
  när listan visas klockan 23.59 samma dag,
  så visas uppgiften inte som försenad.

- AK-2.3
  Givet en oavslutad uppgift vars förfallodatum är den 16 november,
  när datumet blir den 17 november i den tidszon som fastställts,
  så visas uppgiften som försenad.

- AK-2.4
  Givet en slutförd uppgift vars förfallodatum har passerat,
  när listan över försenade uppgifter hämtas,
  så finns uppgiften inte med i listan.

- AK-2.5
  Givet en uppgift utan förfallodatum,
  när listan över försenade uppgifter hämtas,
  så finns uppgiften inte med i listan.

## Ett use case med huvudflöde, alternativa flöden och undantag

### UC-01 – Kontrollera försenade uppgifter

**Aktör**

En teammedlem.

**Mål**

Att upptäcka försenade uppgifter och kunna prioritera arbetet.

**Förutsättningar**

Teammedlemmen har tillgång till uppgiftsappen.

### Huvudflöde

1. Teammedlemmen begär att få se försenade uppgifter.
2. Systemet hämtar uppgifterna.
3. Systemet jämför förfallodatumen med dagens datum.
4. Systemet visar oavslutade uppgifter vars förfallodatum har passerat.
5. Teammedlemmen ser vilka uppgifter som behöver hanteras.

### Alternativa flöden

- Inga uppgifter är försenade. Listan innehåller inga uppgifter.
- En uppgift förfaller idag. Den visas inte som försenad.
- En uppgift är slutförd. Enligt det föreslagna kriteriet
  AK-2.4 visas den inte i listan.
- En uppgift saknar förfallodatum. Enligt det föreslagna
  kriteriet AK-2.5 visas den inte i listan.

### Undantagsflöde

API:t svarar inte.

Föreslagen hantering är att appen visar ett felmeddelande
och låter användaren försöka igen. Ett misslyckat anrop
ska då inte presenteras som en tom lista.

Felhanteringen behöver fastställas i kravintervjun.

## Icke-funktionella krav, med siffror

### NFK-01 – Svarstid

Föreslaget krav utifrån lektionsmaterialets exempel:

GET /api/todos/overdue ska svara på under 200 ms
vid åtta samtidiga användare.

Före godkännande behöver följande fastställas:

- Vilken datamängd testet ska använda.
- Vilken testmiljö som ska användas.
- Hur länge belastningstestet ska pågå.
- Vilket svarstidsmått gränsen gäller för.

### Felfrekvens

Högsta tillåtna andel misslyckade anrop och mätperiod
behöver fastställas i kravintervjun.

Kundens sifferkrav är ännu inte dokumenterade.

## Utanför scope, alltså det vi medvetet inte gör nu

Den föreslagna avgränsningen för detta arbete är att rätta
och testa förseningsstatusen.

Följande ingår därför inte i detta utkast:

- Automatiska påminnelser före deadline.
- Tilldelning av uppgifter till teammedlemmar.
- Automatiska meddelanden till kunder.

Avgränsningen behöver stämmas av i kravintervjun.
