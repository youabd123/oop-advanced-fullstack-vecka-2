# Kravspecifikation

## Problemet, med kundens egna ord

”Vi missar deadlines hela tiden, och ingen märker det förrän kunden ringer och är arg.”

Appen visar också uppgifter som försenade redan under förfallodagen, vilket har minskat teamets förtroende för listan.

## Mål, och hur vi vet att vi har nått dem

Målet är att färre deadlines missas.
Nuläge, målvärde, tidsram och mätmetod behöver bekräftas med Sara.

## Frågor vi ställde, och svaren

Enligt våra anteckningar missas deadlines och användaren får ingen notis, trots att notisfunktionen finns.

Följande förslag har vi formulerat och behöver bekräfta med Sara:
- Påminnelsen visas i uppgiftsappen 24 timmar före deadline.
- Bara personen som uppgiften är tilldelad får påminnelsen.
- En redan slutförd uppgift ger ingen påminnelse.

## User stories med acceptanskriterier

### US-01 – Påminnelse före deadline

Förslag att bekräfta med Sara.

Som teammedlem vill jag få en påminnelse 24 timmar före deadline
för en uppgift som är tilldelad mig, så att jag hinner agera i tid.

- AK-1.1 Givet en oavslutad uppgift tilldelad mig med deadline
  den 25 november kl. 15.00, när klockan blir 15.00 den
  24 november, så får jag en notis i uppgiftsappen.
- AK-1.2 Givet samma uppgift, när påminnelsen skickas,
  så får övriga teammedlemmar ingen notis om den.
- AK-1.3 Givet att uppgiften har markerats som klar före
  påminnelsetidpunkten, när det återstår 24 timmar till deadline,
  så skickas ingen påminnelse.
  ### US-02 – Korrekt förseningsstatus

Som teammedlem vill jag att uppgifter får korrekt förseningsstatus,
så att jag kan lita på listan och prioritera mitt arbete.

- AK-2.1 Givet en oavslutad uppgift med förfallodatum idag,
  när listan visas kl. 09.00 samma dag,
  så visas uppgiften inte som försenad.
- AK-2.2 Givet samma uppgift,
  när listan visas kl. 23.59 samma dag,
  så visas uppgiften inte som försenad.

Öppen fråga till Sara
Vilken tidszon ska styra förseningsstatusen?

## Ett use case med huvudflöde, alternativa flöden och undantag

### UC-01 – Få en påminnelse före deadline

Förslag att bekräfta med Sara.

Förutsättningar
Uppgiften har en deadline och är tilldelad en person.

Huvudflöde
1. Det återstår 24 timmar till uppgiftens deadline.
2. Systemet kontrollerar att uppgiften fortfarande är oavslutad.
3. Systemet visar en notis i appen för personen som har uppgiften.

Alternativt flöde
- Uppgiften är redan klar. Ingen påminnelse skickas.

Undantagsflöde
- Påminnelsen kan inte levereras på grund av ett tekniskt fel.
  Hur systemet ska hantera detta behöver fastställas med Sara.

## Icke-funktionella krav, med siffror

Återstår att fastställa med Sara.

## Utanför scope

Återstår att avgränsa med Sara.
