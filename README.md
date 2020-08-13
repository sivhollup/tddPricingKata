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
* Registrere

The finished function(s) should be able to handle the following: 
* Register an item (name, unit price)
* Register an item with a discount rule (name, unit price, threshold, discount price at threshold level)
* Connect a checkout with a set of prices 
* Scan an item and return the correct price
* Reject unknown item without adverse effects for already scanned items
* Scan items that trigger a discount
* Print a receipt with items, the amount and cost for each set of items, and a separate line at the bottom with the total sum.


## Solving the kata

Spend time discussing the order in which you want to proceed. You don't get to write any code in the implementation class 
unless you have a test that covers it. Write the test first and verify that it fails before implementing the correct behaviour. 
Refactor as you go when the need arises. 

Write down some notes on which order you want to implement functionality, and why. We will go through the choices each group
has made and the code, as I'm sure each group will solve the problem in a different way. 