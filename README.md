# Kata: Kassesystem

Jobb i par når dere løser denne. 

Du skal bygge et enkelt kassesystem som kan scanne varer. En vare har et navn, en pris. I tillegg kan varen har en rabatt, der du oppgir 
et antall du må kjøpe for at rabatten skal slå inn, og en rabatt i prosent. Varer skal kunne scannes, og scanne-metoden 
returnerer hvor mye du har handlet for (sum). Hvis dere får tid kan dere også lage en kvitteringsfunksjon som skriver ut 
alle varene på hver sin linje (samle flere varer av samme type på samme linje sammen med evt rabatt), samt en linje til slutt 
som viser totalsummen. 

Dere skal løse denne ved hjelp av test-drevet utvikling. Testen skal skrives før implementasjonskoden! Bruk gjerne litt 
tid på å tenke gjennom teknisk design (klasser og funksjoner), samt i hvilken rekkefølge dere skal implementere testene. 
Prøv å implementere slik at dere legger på litt og litt funksjonalitet for hver test. Begynn med det enkleste dere kan se for dere. 



## Spesifikasjon

Kassesystemet (en eller flere klasser) skal kunne gjøre følgende: 
* Registrere en eller flere varer gitt ved navn og pris på en enhet
* Registrere en eller flere varer med rabatt, gitt ved navn, pris, antall enheter som må kjøpes for at rabatten skal slå inn, samt rabatt i prosent
* Koble sammen kasse med vareliste
* Registrere en vare og gi rett pris for denne
* Ignorere ukjente varer
* Registrere en vare som utløser rabatt
* Skrive ut en kvittering for varene. En linje pr vare, kostnad for varen, antall kjøpt, og en separat linje til slutt med totalsum. 


## Løse kataen

### Del 1: design

Lag et API-design som dekker alle kravene. Diskutér hvilken rekkefølge dere skal løse de ulike kravene i, slik at dere kan
implementere litt og litt etterhvert som dere legger til tester. Noter ned designvalg og hvorfor dere velger denne rekkefølgen. 

### Del 2: implementasjon

Implementér systemet ved hjelp av testdrevet utvikling. Dere får ikke lov å skrive noe produksjonskode før dere har en test!
Skriv koden i testen, og når du får en kompileringsfeil på grunn av manglende klasser eller metoder, lag rammeverket som trengs
men la selve løsningen være til testen har feilet. Dette gjør at dere vil bytte mellom test- og implementasjonsklasse ofte. 

Når dere har fungerende tester og kode kan dere refaktorere om det er nødvendig. 

Dersom vi får tid går vi gjennom løsningene til de ulike gruppene for å se hvilke løsninger dere har valgt. 


### Bakgrunn

Denne kataen er løst basert på [denne](http://codekata.com/kata/kata09-back-to-the-checkout/).
