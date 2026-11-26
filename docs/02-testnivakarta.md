estnivåkarta CityBike
T1

Nivå: enhet Motivering: PriceCalculator räknar bara ut ett pris från en tid, det finns ingen databas eller nätverk med så fråga fyra gäller.

T2

Nivå: enhet Motivering: Samma sak som T1, det är ren logik i PriceCalculator som testar taket i P3 och inget annat behöver startas.

T3

Nivå: integration Motivering: API:et körs i en testserver ihop med en riktig SQL Server-databas så flera delar samverkar, men det är inte hela kedjan i en driftlik miljö, så fråga tre gäller.

T4

Nivå: enhet Motivering: Upplåsningsklienten är ersatt med en testdubbel så bara BookingService testas för sig, då blir det fråga fyra.

T5

Nivå: system Motivering: Hela kedjan går från kundappen via API:et till en styrenhet, alltså flera systemdelar tillsammans, så fråga två gäller.

T6

Nivå: acceptans Motivering: Det är projektledaren som godkänner resultatet efter att riktiga pilotkunder testat, så fråga ett gäller direkt.

T7

Nivå: integration Motivering: Repositoryt pratar med en riktig SQL Server-databas, så koden och databasen testas tillsammans enligt fråga tre.

T8

Nivå: system Motivering: Kartan hämtas av 500 användare mot en driftlik testmiljö där hela systemet är igång, så fråga två gäller.

T9

Nivå: enhet Motivering: Dagens datum skickas in som parameter så AgeValidator inte behöver något utifrån, det är ren logik och fråga fyra gäller.

T10

Nivå: acceptans Motivering: Ekonomiansvarig är beställare och bestämmer om kvittot är godkänt, så fråga ett gäller.

T11

Nivå: integration Motivering: Testet går genom en riktig HTTP-stack i samma process men resten av systemet startas inte, så det blir fråga tre.

T12

Nivå: system Motivering: Hela resflödet från registrering till betalning körs i testmiljön genom alla delar, så fråga två gäller.

T13

Nivå: enhet Motivering: EmailValidator kollar bara en textsträng utan databas eller nätverk, så fråga fyra gäller.

T14

Nivå: acceptans Motivering: Kundtjänst är användare av adminpanelen och skriver under ett protokoll om att det är godkänt, så fråga ett gäller.

T15

Nivå: integration Motivering: StationService och databasen testas tillsammans för att se att antalet lediga cyklar blir rätt, det är två delar som samverkar så fråga tre gäller.

T16

Nivå: system Motivering: Firmwaren skickas ut till 20 riktiga styrenheter i en testrigg och sen kollas upplåsning och position, så flera systemdelar körs i en miljö som liknar driften enligt fråga två.

Sammanställning

Enhet: 5 Integration: 4 System: 4 Acceptans: 3

Summa: 16. Fördelningen är ganska jämn medan pyramiden på bild 6 har mycket fler enhetstester längst ner än tester högre upp, i ett riktigt projekt borde det finnas betydligt fler enhetstester än system- och acceptanstester.

Eget testfall

Krav: Krav 1: Safety i docs/01-kvalitetsanalys.md Givet: en cykel står och laddar i testriggen och temperaturgivaren är kopplad till en simulator När: simulatorn sätter batteritemperaturen till 61 °C Då: laddningen är avstängd inom 5 sekunder och teknikerna har fått ett larm inom 60 sekunder Nivå: system Testtyp: icke-funktionellt, svartlåda

Kontrollfrågor
Felet hittas billigast på enhetsnivå eftersom det är ett fel i själva prisberäkningen och ett enhetstest går att köra på någon sekund. T1 ligger närmast eftersom det testar vad PriceCalculator tar betalt för en viss tid, man skulle kunna lägga till ett liknande fall för 61 sekunder.
T16 var svårast. Jag tvekade mellan integration och system eftersom det bara är firmwaren och styrenheterna som testas, men jag valde system för att det är riktig hårdvara i en testrigg som liknar driften.