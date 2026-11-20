# Kravspecifikation

## Problemet, med kundens egna ord

”Vi är ett team på åtta personer som använder er uppgiftsapp
varje dag. Problemet är att vi missar deadlines hela tiden,
och ingen märker det förrän kunden ringer och är arg.”

Sara har också rapporterat att appen visar uppgifter som
försenade redan under förfallodagen. Det har gjort att teamet
slutat lita på listan.

Det finns redan ett förfallodatum och en endpoint,
GET /api/todos/overdue, för att hämta försenade uppgifter.

## Mål, och hur vi vet att vi har nått dem

### Korrekt förseningsstatus

- Nuläge – enligt buggrapporten visas uppgifter som försenade
  redan under förfallodagen.
- Mål – samtliga fastställda acceptanskriterier för
  förseningsstatus ska vara uppfyllda.
- Tidsram – kontrolleras innan buggrättningen godkänns.
- Mätmetod – automatiserade tester kopplade till kriteriernas ID.

### Färre missade deadlines

- Nuläge – behöver mätas med Sara.
- Målvärde – behöver bestämmas med Sara.
- Tidsram – behöver bestämmas med Sara.
- Föreslagen mätmetod – andelen uppgifter med deadline under
  mätperioden som slutförts senast på förfallodagen.

Det behöver fastställas hur ändrade deadlines och avbrutna
uppgifter ska hanteras i mätningen.

## Frågor vi ställde, och svaren

Vi har ännu inga dokumenterade svar från en egen kundintervju.
Följande kundsvar finns i kursmaterialet.

### Bekräftat i underlaget

- Sara beskriver ett team på åtta personer.
- Teamet upptäcker missade deadlines först när kunden hör av sig.
- Appen markerar uppgifter som försenade under förfallodagen.
- I onsdagens material säger Sara:
  ”Har jag sagt fredag så får det bli klart fredag kväll.”

Förfallodatumet ska därför vara ett datum utan klockslag.
Uppgiften får bli klar under hela förfallodagen.

### Öppna frågor till Sara

- Vilken tidszon ska styra när förfallodagen har passerat?
- Hur stor andel av uppgifterna blir klara i tid idag?
- Vilket resultat vill ni nå och inom vilken tid?
- Hur använder ni listan för att upptäcka och hantera förseningar?
- Behöver ni påminnelser före deadline?

## User stories med acceptanskriterier

### US-02 – Korrekt förseningsstatus

Som teammedlem vill jag se vilka uppgifter som faktiskt är
försenade, så att jag kan lita på listan och prioritera arbetet.

AK-2.1 och AK-2.2 bygger på buggrapporten och Saras datumregel.
Övriga kriterier är föreslagna preciseringar att bekräfta med Sara.
Tidszonen behöver fastställas för tester vid dygnsgränsen.

- AK-2.1 Givet en oavslutad uppgift med förfallodatum idag,
  när listan visas kl. 09.00 samma dag,
  så visas uppgiften inte som försenad.

- AK-2.2 Givet en oavslutad uppgift med förfallodatum idag,
  när listan visas kl. 23.59 samma dag,
  så visas uppgiften inte som försenad.

- AK-2.3 Givet en oavslutad uppgift med förfallodatum igår,
  när nästa dag börjar kl. 00.00 i överenskommen tidszon,
  så visas uppgiften som försenad.

- AK-2.4 Givet en slutförd uppgift vars förfallodatum har passerat,
  när listan över försenade uppgifter hämtas,
  så finns uppgiften inte med i listan.

- AK-2.5 Givet en uppgift utan förfallodatum,
  när listan över försenade uppgifter hämtas,
  så finns uppgiften inte med i listan.

ID US-02 behålls från det tidigare utkastet.
Den tidigare US-01 om påminnelser har tagits bort i väntan
på svar från Sara.

## Ett use case med huvudflöde, alternativa flöden och undantag

### UC-01 – Kontrollera försenade uppgifter

Aktör
En teammedlem.

Mål
Att upptäcka försenade uppgifter och kunna prioritera arbetet.

Förutsättningar
Teammedlemmen har tillgång till uppgiftsappen.

### Huvudflöde

1. Teammedlemmen öppnar listan över försenade uppgifter.
2. Systemet hämtar uppgifterna.
3. Systemet jämför förfallodatumen med dagens datum.
4. Systemet visar oavslutade uppgifter vars förfallodatum
   har passerat.
5. Teammedlemmen ser vilka uppgifter som behöver hanteras.

### Alternativa flöden

- Inga uppgifter är försenade. Listan innehåller inga uppgifter.
- En uppgift förfaller idag. Den visas inte som försenad.
- En uppgift är slutförd eller saknar förfallodatum.
  Föreslagen hantering är att den inte visas som försenad,
  enligt AK-2.4 och AK-2.5.

### Undantagsflöde

API:t svarar inte.

Föreslagen hantering att bekräfta med Sara är att appen visar
ett felmeddelande och ger möjlighet att försöka igen.
Ett misslyckat anrop ska då inte presenteras som en tom lista.

## Icke-funktionella krav, med siffror

Följande är förslag från övningens prestandaexempel.
De behöver bekräftas och preciseras innan de används som
godkända krav.

- NFK-01 – API-anropet GET /api/todos/overdue ska ha en svarstid
  under 200 ms vid åtta samtidiga användare.

För NFK-01 behöver datamängd, testmiljö, testets längd och
vilket svarstidsmått som ska användas fastställas.

Högsta tillåtna felfrekvens och mätperiod behöver också
bestämmas. Kundgodkända sifferkrav saknas ännu.

## Utanför scope, alltså det vi medvetet inte gör nu

I detta utkast fokuserar vi på korrekt förseningsstatus.

Följande funktioner ingår inte i den föreslagna avgränsningen
och behöver diskuteras med Sara om de ska tas vidare.

- Automatiska påminnelser före deadline.
- Tilldelning av uppgifter till teammedlemmar.
- Automatiska meddelanden till kunder.

Avgränsningen behöver bekräftas med Sara.
