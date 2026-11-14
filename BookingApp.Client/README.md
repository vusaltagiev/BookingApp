# Bokningssystem – SXX Maskiner och Utrustning AB

## Beskrivning

Det här projektet är en individuell implementation av två funktioner i bokningssystemet för SXX Maskiner och Utrustning AB.

Projektet fokuserar på följande User Stories:

- **US-04 – Prisberäkning i realtid:** Kunden ska kunna se totalpriset för en vald utrustningsmodell och bokningsperiod innan bokningen bekräftas. Om kunden ändrar bokningsperioden ska priset räknas om automatiskt.
- **US-05 – Prislåsning vid genomförd bokning:** Det pris som kunden godkänner ska sparas på bokningsobjektet och inte påverkas av senare ändringar av utrustningsmodellens dagspris.

Applikationen är utvecklad med **C#, .NET, Blazor och ett Web API**.

## Funktioner

### US-04 – Prisberäkning i realtid

- Kunden kan välja en utrustningsmodell.
- Kunden kan ange startdatum och slutdatum för bokningen.
- Systemet beräknar totalpriset utifrån modellens dagspris och antalet kalenderdagar.
- Både första och sista bokningsdagen räknas med.
- Priset uppdateras när kunden ändrar bokningsperioden.

Beräkningsformel:

`Totalpris = Dagspris × Antal kalenderdagar`

Exempel: Om dagspriset är 250 kr och kunden väljer perioden 12–14 november blir totalpriset 750 kr (3 × 250 kr).

### US-05 – Prislåsning vid genomförd bokning

- Kunden kan bekräfta bokningen med det visade totalpriset.
- Det godkända priset sparas i egenskapen `AgreedTotalPrice` på bokningsobjektet.
- Om administratören senare ändrar modellens dagspris påverkas inte priset på en redan skapad bokning.

## Teknik och struktur

Projektet använder:

- **C# och .NET** – programmeringsspråk och plattform.
- **Blazor** – webbgränssnitt.
- **ASP.NET Core Web API** – kommunikation mellan webbgränssnittet och tjänstelogiken.
- **BookingController** – tar emot API-anrop.
- **BookingService** – ansvarar för prisberäkning och skapande av bokningar.
- **Booking** – representerar en bokning och innehåller bland annat det överenskomna totalpriset.
- **EquipmentModel** – representerar en utrustningsmodell och dess dagspris.

Utrustningsmodeller och bokningar lagras i listor i minnet. Projektet använder därför ingen databas. Informationen finns kvar under applikationens körning men försvinner när applikationen startas om.

## Köra projektet

1. Klona eller ladda ner repositoryt från GitHub.
2. Öppna projektets lösningsfil (`.sln`) i Visual Studio.
3. Kontrollera att nödvändiga .NET-komponenter är installerade.
4. Välj serverprojektet som startprojekt.
5. Starta applikationen med Visual Studio.
6. Öppna webbgränssnittets bokningssida i webbläsaren.

API-adressen som används i den nuvarande lokala konfigurationen är:

`https://localhost:7075/`

## Testa funktionerna

### Test av US-04 – Prisberäkning i realtid

1. Öppna bokningssidan.
2. Välj utrustningsmodellen M1, vars dagspris är 250 kr.
3. Ange startdatum 12 november och slutdatum 14 november.
4. Kontrollera att totalpriset visas som 750 kr.
5. Ändra slutdatumet till 15 november.
6. Kontrollera att totalpriset uppdateras till 1 000 kr.

### Test av US-05 – Prislåsning vid genomförd bokning

1. Välj en utrustningsmodell och en bokningsperiod.
2. Kontrollera det beräknade totalpriset.
3. Bekräfta bokningen.
4. Kontrollera att det godkända priset har sparats på bokningen.
5. Använd administrationsfunktionen för att ändra utrustningsmodellens dagspris.
6. Kontrollera bokningen igen.
7. Det ursprungligen bekräftade totalpriset ska vara oförändrat.

## Avgränsningar

Projektet är en individuell och avgränsad implementation av US-04 och US-05. Det innehåller inte hela bokningssystemets funktionalitet.

Fullständig kontroll av tillgängliga utrustningsexemplar, reservation av specifika exemplar, kundregistrering, betalning och databashantering ingår inte i denna implementation.

## Publicerad applikation

Applikationen finns även publicerad här:

https://booking.vusaltagiev.se/booking

## Författare

Individuellt praktiskt prov – Bokningssystem för SXX Maskiner och Utrustning AB.