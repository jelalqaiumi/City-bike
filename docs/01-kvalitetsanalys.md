# Kvalitetsanalys CityBike

## 1. Observationer och egenskaper

### K1
Egenskap: Performance efficiency
Delegenskap: Time behaviour
Motivering: Kartan är för långsam under belastning (9 sekunder för 300 användare).

### K2
Egenskap: Functional suitability 
Delegenskap: Functional correctness 
Motivering: Kunden får betala två gånger för samma resa, alltså blir resultatet fel. Det händer vid dålig täckning så det har också med Reliability att göra.

### K3
Egenskap: Reliability 
Delegenskap: Fault tolerance 
Motivering: Resan ska inte avbrytas bara för att styrenheten tappar täckning, positionerna ska skickas när den är uppkopplad igen.

### K4
Egenskap: Interaction capability 
Delegenskap: Learnability 
Motivering: Nya kunder hittar inte avsluta-knappen och det blir 40 samtal i veckan till kundtjänst.

### K5
Egenskap: Security 
Delegenskap: Confidentiality 
Motivering: Man kan se någon annans resa bara genom att byta id i adressen.

### K6
Egenskap: Maintainability 
Delegenskap: Modularity 
Motivering: Prisberäkningen och bokningen ligger i samma klass så ingen vågar ändra något, det borde vara uppdelat. Modifiability passar också.

### K7
Egenskap: Flexibility 
Delegenskap: Adaptability 
Motivering: Adminpanelen funkar inte på teknikernas surfplattor eftersom den inte anpassar sig till mindre skärmar. Kan också ses som Interaction capability.

### K8
Egenskap: Safety 
Delegenskap: Fail safe 
Motivering: Ett batteri över 60 grader kan börja brinna, så laddningen måste brytas automatiskt och teknikerna få ett larm.

### K9
Egenskap: Compatibility 
Delegenskap: Interoperability 
Motivering: API:et måste förstå data från både de gamla och de nya styrenheterna fast de skickar olika format.

### K10
Egenskap: Flexibility 
Delegenskap: Adaptability 
Motivering: För att lägga till en ny stad måste man ändra koden på tolv ställen, det borde gå att ställa in istället. Maintainability passar också.

## 2. De fyra viktigaste egenskaperna för CityBike

1. Safety: om laddningen inte stängs av när batteriet blir för varmt kan det börja brinna och folk kan skadas, se K8 och avsnitt 7. CityBike räknas som tillverkare av styrenheten och har därför ansvaret om något händer.

2. Security: kunder kan se varandras resor och var de har åkt, se K5. Enligt R2 i avsnitt 6 sparas alla positioner tills vidare, så det går att se exakt var någon har åkt. Det kan ge skadestånd och sanktionsavgift enligt GDPR.


3. Functional suitability: om kunder får betala dubbelt tappar de förtroendet och CityBike måste betala tillbaka, se K2 och prisreglerna P1 till P3 i avsnitt 2.


4. Reliability: om resor och positioner försvinner när täckningen bryts blir priset fel och cyklarna går inte att hitta, se K3 och avsnitt 4 där styrenheten skickar position var 15:e sekund.

## 3. Mätbara krav

### Krav 1: 
Krav: När batteriet går över 60 °C ska laddningen stängas av inom 5 sekunder och teknikerna få larm inom 60 sekunder, i alla testfall. 
Mått: tid från att temperaturen går över 60 °C tills laddningen är avstängd och larmet har kommit fram 
Gränsvärde: 5 sekunder för avstängning, 60 sekunder för larm 
Mätmetod: test där vi låtsas att temperaturgivaren visar över 60 °C, 50 gånger, och kollar tidsstämplarna 
Hänvisning: K8, avsnitt 7

### Krav 2: 
Krav: Om en inloggad kund försöker öppna någon annans resa genom att byta id ska 0 av 1 000 försök visa resan, svaret ska vara HTTP 403 eller 404. 
Mått: antal försök där en annan kunds resa visas 
Gränsvärde: 0 av 1 000 
Mätmetod: automatiskt test mot API:et med två testkonton 
Hänvisning: K5 avsnitt 5 (tabellerna Trips och GpsPoints) och R2 i avsnitt 6

### Krav 3: 
Krav: Om samma betalning skickas 2 till 5 gånger inom 10 minuter ska kunden bara dras pengar 1 gång, i alla 500 testfall. 
Mått: antal dragningar per resa 
Gränsvärde: 1 dragning per resa, 0 dubbla av 500 Mätmetod: integrationstest som skickar samma betalning flera gånger mot betaltjänstens testläge 
Hänvisning: K2, avsnitt 2 och avsnitt 4


### Krav 4: 
Krav: Efter ett avbrott i täckningen på upp till 30 minuter ska minst 99,9 procent av positionerna komma fram till servern inom 2 minuter efter att uppkopplingen är tillbaka. Mått: andel positioner som kommer fram och hur lång tid det tar 
Gränsvärde: minst 99,9 procent inom 2 minuter 
Mätmetod: test där vi stänger av mobilnätet i 5, 15 och 30 minuter under en resa och jämför med serverns logg 
Hänvisning: K3, avsnitt 4 och avsnitt 7

### Tillgänglighet 99,7 procent
30 dagar = 720 timmar = 43 200 minuter Nedtid som är tillåten = 0,3 procent av 43 200 = 0,003 × 43 200 = 129,6 minuter Svar: max 129,6 minuter nedtid på 30 dagar, ungefär 2 timmar och 10 minuter.

## 4. Skillnad mot ett annat par