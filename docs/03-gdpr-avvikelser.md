GDPR-avvikelser i CityBike
Personuppgiftsinventering
Users: Id, Name, Personnummer, Email, Phone, PasswordHash, Status, CreatedAt. Namn, personnummer, mejl och telefonnummer kan direkt kopplas till en person. Även de andra uppgifterna räknas som personuppgifter eftersom de hör ihop med en viss användare.
PaymentMethods: UserId, ProviderToken, CardLast4, ExpiryMonth, ExpiryYear. Eftersom informationen är kopplad till användaren via UserId går det att se vilken kund betalningen tillhör.
Bikes: Inga personuppgifter. Här finns bara information om själva cyklarna.
Stations: Inga personuppgifter. Här sparas bara information om stationernas namn och platser.
Trips: UserId, StartStationId, EndStationId, StartedAt, EndedAt, PriceSek. Eftersom resorna är kopplade till användaren går det att se vem som har åkt, var personen har varit och när.
GpsPoints: TripId, Latitude, Longitude, RecordedAt. Koordinaterna är kopplade till en viss resa via TripId, så det går att se exakt var en kund har befunnit sig.
A1

Rutin: R1 Vad: CityBike kräver personnummer när en kund registrerar sig, trots att det egentligen inte behövs för att uppnå syftet. Artikel: Art. 5.1 c, dataskyddslagen 3 kap. 10 § Risk: Hög Åtgärd: Ta bort kravet på personnummer. Om företaget behöver kontrollera kundens ålder kan det göras på ett annat sätt, till exempel genom att bara fråga efter födelsedatum. Testfall: Testa att skapa ett konto utan att fylla i personnummer. Registreringen ska fortfarande fungera som vanligt (systemtest).

A2

Rutin: R2 Vad: GPS-punkter och resehistorik sparas för alltid. Det kan bli ungefär 44 miljoner GPS-punkter under en säsong, trots att det inte finns något behov av att spara alla dessa uppgifter så länge. Artikel: Art. 5.1 e Risk: Hög Åtgärd: GPS-punkter ska raderas efter 30 dagar. I tabellen Trips ska bara den information som behövs för bokföringen sparas. Testfall: Lägg in GPS-punkter som är 31 dagar gamla i en testdatabas. Kör sedan raderingen och kontrollera att de gamla punkterna försvinner (integrationstest).

A3

Rutin: R3 Vad: När en kund stänger sitt konto ändras bara statusen till Inactive. Alla personuppgifter finns fortfarande kvar i systemet. Artikel: Art. 17, art. 5.1 e Risk: Medel Åtgärd: När ett konto stängs ska kundens personuppgifter raderas eller anonymiseras. Det enda som får sparas är de uppgifter som företaget enligt bokföringslagen måste behålla. Testfall: Stäng ett testkonto och kontrollera att namn, personnummer, mejladress och telefonnummer har tagits bort från Users (integrationstest).

A4

Rutin: R4 Vad: Alla som jobbar inom kundtjänst använder samma konto och lösenordet delas i chatten. Det gör att alla kan se kundernas personnummer och det blir svårt att veta vem som har gjort vad i systemet. Artikel: Art. 32, art. 5.1 f, art. 25 Risk: Hög Åtgärd: Alla anställda ska ha egna konton och använda tvåfaktorsinloggning. Kundtjänst ska också få en särskild behörighet som gör att de inte kan se kundernas personnummer. Testfall: Logga in med ett kundtjänstkonto och hämta uppgifter om en kund. Kontrollera att personnumret inte visas i svaret (integrationstest).

A5

Rutin: R5 Vad: Alla anrop i systemet sparas i loggar under ett helt år. Det innebär att känsliga uppgifter, som personnummer och lösenord, kan hamna direkt i loggfilerna och läsas av obehöriga. Artikel: Art. 5.1 c, art. 5.1 e, art. 32 Risk: Hög Åtgärd: Känsliga uppgifter ska döljas innan de sparas i loggarna. Loggfilerna ska inte heller sparas längre än 30 dagar. Testfall: Gör en registrering och sök sedan i loggfilen efter personnumret och lösenordet. Inget av dessa ska gå att hitta (integrationstest).

A6

Rutin: R6 Vad: Alla kunder får nyhetsbrev trots att de inte har tackat ja till att ta emot dem. Artikel: Art. 6.1, art. 7, art. 21 Risk: Låg Åtgärd: Lägg till en ruta vid registreringen där kunden själv kan välja om den vill få nyhetsbrev. Rutan ska inte vara ikryssad från början. Det ska också finnas en avregistreringslänk i varje nyhetsbrev. Testfall: Registrera en ny kund utan att kryssa i rutan för nyhetsbrev. Kontrollera sedan att kunden inte hamnar på företagets utskickslista (systemtest).

A7

Rutin: R7 Vad: Mejladresser, användar-ID och reseinformation skickas till ett analysverktyg i USA utan att det finns något avtal på plats. Mejladresserna behövs dessutom inte för att kunna ta fram statistik. Artikel: Art. 28, art. 44, art. 46, art. 5.1 c Risk: Hög Åtgärd: CityBike behöver skriva ett personuppgiftsbiträdesavtal och kontrollera att överföringen av uppgifter till USA följer GDPR. Man bör också ta bort mejladresserna och bara skicka den information som faktiskt behövs, helst pseudonymiserad. Testfall: Kontrollera ett anrop till analysverktyget i testmiljön. Det ska inte innehålla någon mejladress (integrationstest).

A8

Rutin: R8 Vad: CityBike har varken en förteckning över hur personuppgifter behandlas eller en konsekvensbedömning. Det är extra viktigt eftersom företaget samlar in stora mängder GPS-data som kan visa var kunder befinner sig. Artikel: Art. 30, art. 35 Risk: Medel Åtgärd: Skapa en förteckning över företagets behandling av personuppgifter och gör en konsekvensbedömning. GPS-informationen bör få extra uppmärksamhet eftersom den kan avslöja mycket om kundernas rörelser. Testfall: Gå igenom förteckningen och kontrollera att alla sex tabeller finns med och att behandlingen av uppgifterna är dokumenterad (acceptanstest).

A9

Rutin: R8 Vad: Appen berättar inte hur kundernas personuppgifter används. Kunden får inte heller veta vilka uppgifter som sparas eller hur länge de kommer att finnas kvar. Artikel: Art. 12, art. 13 Risk: Medel Åtgärd: Lägg till en integritetspolicy som kunden får se när den registrerar sig. Policyn ska också vara lätt att hitta i appen även efter att kontot har skapats. Testfall: Kontrollera att länken till integritetspolicyn syns och går att öppna innan kunden skapar sitt konto (systemtest).

A10

Rutin: R11 Vad: CityBike använder SHA-256 utan salt för att lagra lösenord. Det är inte tillräckligt säkert eftersom det finns färdiga tabeller som gör att lösenorden kan bli ganska enkla att knäcka om någon kommer åt databasen. Artikel: Art. 32, art. 5.1 f Risk: Hög Åtgärd: Byt till en säkrare metod, till exempel Argon2 eller PBKDF2 med salt. Befintliga lösenordshashar kan uppdateras till den nya metoden när kunderna loggar in nästa gång. Testfall: Skapa två användare med samma lösenord och kontrollera att de får olika hashvärden (enhetstest).

R9

Rutin: R9 Bedömning: i ordning. Säkerhetskopior behövs för att företaget ska kunna återställa information om något skulle gå fel, och 90 dagar är rimligt eftersom det är en del av säkerheten enligt artikel 32. Om en kund raderar sitt konto finns uppgifterna däremot kvar i säkerhetskopiorna tills de tas bort, och det bör dokumenteras i förteckningen över personuppgiftsbehandlingar.

Incident R10

Tidpunkt för kännedom: tisdag 3 mars 2026 14:20 Frist för anmälan (datum och klockslag): fredag 6 mars 2026 14:20 Anmäla till IMY: Ja Informera berörda kunder: Nej, inte i nuläget Motivering: Namn, mejladresser och telefonnummer till ungefär 2 100 kunder har skickats till ett externt företag som CityBike inte har något avtal med. Eftersom det finns en risk att uppgifterna kan användas på fel sätt, till exempel för att skicka bluffmejl, tycker vi att händelsen ska anmälas till IMY. Samtidigt är risken inte särskilt hög eftersom inga personnummer, lösenord, kortuppgifter eller positionsuppgifter har läckt. Mottagaren är dessutom ett företag som vi kan kontakta och be att radera filen. Därför behöver kunderna inte informeras just nu, men om företaget inte kan bekräfta att filen har raderats bör kunderna informeras. Åtgärder för att förhindra upprepning:

Tekniker ska inte längre kunna exportera kunduppgifter till CSV-filer. Servicebrev ska i stället skickas direkt via företagets e-posttjänst.
Införa en varning i mejlsystemet när någon försöker skicka bilagor som innehåller personuppgifter till mottagare utanför företaget.
Utbilda personalen i hur personuppgifter ska hanteras och vad man ska göra om något går fel.
Kontrollfrågor
Enligt 3 kap. 10 § i dataskyddslagen får personnummer bara användas när det finns en tydlig anledning till det, till exempel om det behövs för att kunna identifiera en person på ett säkert sätt. I CityBikes fall finns det egentligen inget behov av personnummer. Kundernas ålder kan kontrolleras med födelsedatum och eftersom betalningen sker med kort behövs inte heller några påminnelsefakturor.
Att bara ändra Users.Status till Inactive räcker inte, eftersom alla kunduppgifter ligger kvar i databasen. Enligt artikel 17 har kunder rätt att få sina personuppgifter raderade, och artikel 5.1 e säger att personuppgifter inte ska sparas längre än nödvändigt. Om uppgifterna ligger kvar finns det dessutom en fortsatt risk att de kan läcka.
Det är ett integrationstest. Man behöver kontrollera att API:ets behörigheter fungerar tillsammans med databasen, så att kolumnen Personnummer verkligen döljs. Däremot behöver man inte testa hela systemet från början till slut, så adminpanelen behöver inte vara med i testet.