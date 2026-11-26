Regelverkschecklista för CityBike
GDPR
G1 – Radering av kunduppgifter

Gäller: Ja. Skäl: Enligt artikel 17 har kunder rätt att få sina personuppgifter raderade när det inte längre finns någon anledning att spara dem. Ansvarig: Backend-utvecklare. Verifieras med: Integrationstest på funktionell nivå. Bevis: En testrapport från CI som visar att namn, personnummer, mejl och telefonnummer försvinner från Users när ett testkonto stängs.

G2 – Personnummer ska inte behövas vid registrering

Gäller: Ja. Skäl: Enligt artikel 5.1 c och 3 kap. 10 § i dataskyddslagen ska man inte samla in fler personuppgifter än vad som behövs. CityBike behöver inte personnummer för att kontrollera kundernas ålder, vilket även tas upp i R1 och A1. Ansvarig: Produktägare och frontend-utvecklare. Verifieras med: Funktionellt systemtest. Bevis: En testrapport som visar att en kund kan registrera sig utan personnummer. En skärmbild på det skapade kontot ska också sparas.

G3 – Radera gamla GPS-punkter

Gäller: Ja. Skäl: Enligt artikel 5.1 e får personuppgifter inte sparas längre än nödvändigt. Just nu sparas GPS-information för alltid, vilket kan innebära ungefär 44 miljoner rader per säsong. Detta tas även upp i R2 och A2. Ansvarig: Backend-utvecklare. Verifieras med: Funktionellt integrationstest. Bevis: Spara en logg från gallringsjobbet och en testrapport som visar att alla GPS-punkter som är äldre än 30 dagar har raderats.

G4 – Egna konton och rätt behörighet för kundtjänst

Gäller: Ja. Skäl: Enligt artikel 32 och artikel 25 måste personuppgifter skyddas så att obehöriga inte kan komma åt dem. I nuläget delar kundtjänsten på ett konto och kan dessutom se kundernas personnummer. Detta tas upp i R4 och A4. Ansvarig: Backend-utvecklare och IT-ansvarig. Verifieras med: Funktionellt integrationstest. Bevis: En testrapport som visar att en användare med kundtjänstbehörighet inte kan få fram personnummer från API:et. Det ska även finnas en lista över alla personliga användarkonton.

G5 – Personuppgifter ska inte synas i loggarna

Gäller: Ja. Skäl: Artikel 5.1 c och artikel 32 handlar bland annat om att inte spara onödiga uppgifter och att skydda informationen. I dagsläget sparas alla anrop i 12 månader, vilket gör att personnummer och lösenord kan hamna direkt i loggfilerna. Detta beskrivs i R5 och A5. Ansvarig: Backend-utvecklare. Verifieras med: Icke-funktionellt integrationstest. Bevis: En testrapport och ett utdrag från en loggfil efter en testregistrering. Där ska det gå att se att personnummer och lösenord har dolts.

G6 – Avtal och säker överföring till analysverktyget

Gäller: Ja. Skäl: Enligt artikel 28 och artikel 44–46 måste det finnas rätt avtal och laglig grund när personuppgifter skickas till andra företag eller länder utanför EU/EES. Just nu skickas kunduppgifter till USA utan något avtal, vilket tas upp i R7 och A7. Ansvarig: Dataskyddsombud eller ledningen. Verifieras med: Icke-funktionellt acceptanstest. Bevis: Ett undertecknat personuppgiftsbiträdesavtal, dokumentation som visar hur överföringen till USA går till och ett protokoll från granskningen.

CE och produktkrav
C1 – Maskindirektivet och maskinförordningen

Gäller: Osäkert. Skäl: En elcykel som har en motor på högst 250 W och där motorstödet slutar vid 25 km/h omfattas av maskinreglerna och ska därför vara CE-märkt. Vanligtvis är det cykeltillverkaren som ansvarar för detta eftersom CityBike inte säljer själva cyklarna. Men eftersom CityBike monterar in en egen styrenhet kan det räknas som en så kallad väsentlig ändring. I så fall kan CityBike få samma ansvar som en tillverkare. Från januari 2027 ersätts maskindirektivet av maskinförordningen (EU) 2023/1230. Därför behöver man ta reda på exakt vilket ansvar CityBike har. Det bör kontrolleras tillsammans med en jurist eller ett anmält organ. Ansvarig: Ledningen tillsammans med cykelleverantören. Verifieras med: Icke-funktionellt acceptanstest. Bevis: Cykelleverantörens försäkran om överensstämmelse och en juridisk bedömning som visar om CityBikes montering räknas som en väsentlig ändring.

C2 – EN 15194 för elcyklar

Gäller: Ja. Skäl: EN 15194 är en standard som används för att kontrollera att elcyklar uppfyller säkerhetskraven. Den handlar bland annat om att motorstödet ska sluta vid 25 km/h. Eftersom CityBikes styrenhet är kopplad till cykelns elsystem kan den också påverka vissa delar av testningen. Ansvarig: Cykelleverantören. CityBike ansvarar för att begära in provningsrapporten. Verifieras med: Icke-funktionellt acceptanstest. Bevis: En provningsrapport enligt EN 15194 från cykelleverantören eller ett testlaboratorium.

C3 – Radioutrustningsdirektivet

Gäller: Ja. Skäl: Styrenheten innehåller både ett LTE-M-modem och en GPS-mottagare. Eftersom CityBike säljer den under sitt eget varumärke räknas företaget som tillverkare enligt avsnitt 7. Därför måste produkten följa radioutrustningsdirektivet 2014/53/EU. Det innebär också att cybersäkerhetskraven i artikel 3.3 behöver följas. Ansvarig: Ansvarig för firmware och hårdvara. Verifieras med: Icke-funktionellt systemtest. Bevis: Provningsrapporter som visar att radio, elsäkerhet och EMC uppfyller kraven. Det ska också finnas en EU-försäkran om överensstämmelse och teknisk dokumentation.

C4 – Batterisäkerhet och batteriförordningen

Gäller: Osäkert. Skäl: Batteriet kommer från cykelleverantören och är en del av cykeln. Samtidigt har CityBikes styrenhet en viktig funktion eftersom den mäter batteriets temperatur och ska stoppa laddningen om temperaturen blir högre än 60 °C (K8). Det behöver därför undersökas vem som räknas som producent enligt batteriförordningen (EU) 2023/1542. Det behöver också kontrolleras av ett testlaboratorium om styrenhetens funktion påverkar kraven i EN 50604-1. En jurist bör hjälpa till att reda ut ansvaret. Ansvarig: Ledningen och firmware-ansvarig. Verifieras med: Icke-funktionellt systemtest. Bevis: Batterileverantörens provningsrapport enligt EN 50604-1 och CityBikes egen testrapport som visar att laddningen stängs av vid för hög temperatur.

C5 – Elektromagnetisk kompatibilitet (EMC)

Gäller: Ja. Skäl: Styrenheten får inte störa annan elektronik eller själv påverkas av störningar. Ett exempel är att störningar inte ska kunna göra så att cykelns lås slutar fungera. När det gäller radioutrustning hanteras EMC-kraven genom radioutrustningsdirektivets artikel 3.1 b i stället för EMC-direktivet. Ansvarig: Hårdvaruansvarig. Verifieras med: Icke-funktionellt systemtest. Bevis: En EMC-provningsrapport från ett ackrediterat laboratorium där styrenheten testats monterad i själva cykeln.

Cyber Resilience Act (CRA)
CRA1 – Förteckning över komponenter (SBOM)

Gäller: Ja. Skäl: CityBikes styrenhet har en egen firmware och eftersom företaget räknas som tillverkare behöver man veta vilka programbibliotek och komponenter som används. Det gör det enklare att upptäcka säkerhetsbrister och veta vilka delar som behöver uppdateras. Ansvarig: Firmware-utvecklare. Verifieras med: Icke-funktionellt integrationstest. Bevis: En SBOM-fil som skapas automatiskt varje gång en ny version byggs. Filen ska sparas tillsammans med rätt firmwareversion.

CRA2 – Säkerhetsuppdateringar av firmware

Gäller: Ja. Skäl: Eftersom CityBike kan uppdatera sin firmware trådlöst enligt avsnitt 7 måste företaget kunna skicka ut säkerhetsuppdateringar under hela produktens supportperiod. Det är också viktigt att uppdateringarna är digitalt signerade, så att ingen obehörig kan skicka in falska uppdateringar. Ansvarig: Firmware-utvecklare. Verifieras med: Funktionellt systemtest. Bevis: En testrapport från testutrustningen som visar att en korrekt signerad uppdatering installeras, medan en uppdatering utan giltig signatur stoppas.

CRA3 – Hantering av säkerhetsbrister

Gäller: Ja. Skäl: Det måste finnas ett enkelt sätt för personer att rapportera säkerhetsbrister i produkten. Om det upptäcks sårbarheter som redan används för attacker måste de också rapporteras till rätt myndigheter inom den tidsfrist som gäller. Ansvarig: Säkerhetsansvarig. Verifieras med: Icke-funktionellt acceptanstest. Bevis: En publicerad sida där man kan rapportera säkerhetsbrister, en dokumenterad rutin för hur rapporterna ska hanteras och en logg från en övning där företaget testat hur det går till.

CRA4 – Säker hantering av lösenord

Gäller: Ja. Skäl: I R11 framgår det att CityBike använder SHA-256 utan salt för att spara lösenord. Det är inte tillräckligt säkert. Eftersom API:et används för att låsa upp cyklarna är det viktigt att skydda systemet ordentligt. CRA ställer krav på att produkter ska ha ett bra säkerhetsskydd och säkra inställningar från början. Ansvarig: Backend-utvecklare. Verifieras med: Icke-funktionellt enhetstest. Bevis: Ett enhetstest som visar att två användare med samma lösenord får olika hashvärden. Det ska också gå att visa att systemet använder PBKDF2 eller Argon2. En testrapport från CI ska sparas som bevis.

Spårbarhet
K1 – Batteriet får inte bli varmare än 60 °C vid laddning

Källa: C4 och Krav 1 (Safety) i docs/01-kvalitetsanalys.md. Testfall: Montera styrenheten på en cykel i testutrustningen och starta laddningen. Använd en simulator för temperaturgivaren och höj temperaturen stegvis från 55 °C till 61 °C. Under testet ska man kontrollera när temperaturen går över 60 °C, när laddningen stängs av och när varningen kommer fram till adminpanelen. Testet ska göras 50 gånger för att se att funktionen fungerar varje gång. Godkänt resultat: Laddningen ska stängas av inom 5 sekunder och larmet ska visas i adminpanelen inom 60 sekunder vid samtliga 50 testkörningar. Nivå och testtyp: Systemtest, icke-funktionellt. Resultat som ska sparas: Spara information om vilken firmwareversion som testats, serienummer på styrenheten och batteriet, datum, vem som utförde testet och tidsstämplarna från alla 50 körningar. Det ska också framgå vilka tester som blev godkända och vilka som inte blev det. Teknisk dokumentation: Testrapporten ska sparas som PDF i styrenhetens tekniska dokumentation. Den ska ligga i en egen mapp för den firmwareversion som testats. Rådata från testet sparas som CSV i samma mapp.

K2 – GPS-punkter ska tas bort efter 30 dagar

Källa: G3. Testfall: Börja med att skapa en testdatabas och lägg in 100 GPS-punkter som är 31 dagar gamla och ytterligare 100 punkter som är 29 dagar gamla. Kör sedan gallringsjobbet och kontrollera hur många GPS-punkter som finns kvar i GpsPoints. Godkänt resultat: De 100 punkterna som är äldre än 30 dagar ska vara raderade, medan de 100 nyare punkterna ska finnas kvar. Nivå och testtyp: Integrationstest, funktionellt. Resultat som ska sparas: Spara vilken programversion och vilket commit-id som användes för API:et. Dokumentera även datum, hur många punkter som fanns före och efter gallringen samt resultatet från testkörningen. Teknisk dokumentation: Testrapporten ska sparas automatiskt i CI vid varje bygge. Den ska även kopplas till G3 i förteckningen över personuppgiftsbehandlingar.

Kontrollfrågor
Vem ansvarar för CE-märkningen av styrenheten? Eftersom CityBike säljer styrenheten under sitt eget varumärke, enligt avsnitt 7, räknas företaget som tillverkare. Det gäller även om själva styrenheten har byggts av en underleverantör. Därför är det CityBike som ansvarar för att produkten uppfyller kraven för CE-märkning och att den tekniska dokumentationen finns på plats.
Måste varje ny firmwareversion testas igen? Ja, varje ny firmwareversion behöver testas innan den används. Framför allt är det viktigt att göra regressionstester på de viktigaste funktionerna, till exempel låset, GPS-positioneringen och temperaturavstängningen. Om en uppdatering påverkar radiosignaler eller säkerheten kan det också behövas en ny kontroll av att produkten fortfarande uppfyller kraven. SBOM-filen och den tekniska dokumentationen behöver dessutom uppdateras när det sker ändringar.
Varför är det viktigt att spara testresultaten? Det är viktigt att spara testresultaten eftersom de visar exakt vilken firmwareversion som testades, när testet gjordes och vem som utförde det. Om man inte sparar den informationen blir det svårt att veta om testresultatet faktiskt gäller den version av produkten som används ute på marknaden.