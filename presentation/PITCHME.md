---?image=flyt_monster_mork_bakgrunn.svg&size=120%
# Testing og TDD

Note:
- presentasjonsrunde (navn, kontor, bakgrunn)
- Hvorfor tester vi? (5 min)
- Hva forbinder dere med testing? (5 min)



--- 

### Testing er dobbel bokføring

Note:
- hver gang et nytt innslag i et regnskap føres, skal summen gå inn på en konto
  og ut fra en annen
- en konto krediteres, en debeteres. Hvis du kjøper inn kontorrekvisita,
  debeteres kontorrekvisita-kontoen i regnskapet, mens du krediterer bank-konto
  (som du har betalt fra). Summen blir null
- dette kalles dobbel bokføring, og brukes for å redusere antall feil i
  regnskapet og for å gi bedre kontroll over regnskapet
- testing er dobbel bokføring i kodeforstand


---

### Testing er verifisering

Note: 
- "test" er et dårlig navn, det vi driver med er verifikasjon
- verifikasjon av at koden gjør det vi tror at den gjør, også etter vi har
  endret den i etterkant
- finnes mange ulike typer tester, som tester systemet på ulike nivåer
- tester er et sikkerhetsnett


---

### Tester reduserer risiko

Note: 
- øke trygghet hos kunder og utviklere
- øke vedlikeholdbarhet
- senke risiko ved produksjonssetting
- gjør det enklere å eksperimentere
- reduserer mengden konsepter utvikleren trenger å ha i hodet samtidig
- produksjonskode beskriver hvordan en oppgave løses
- testkode beskriver hvordan en løsning skal oppføre seg, og om mulig hvorfor
- idag skal vi begrense oss til å snakke om automatiske tester (enhet,
  regresjon, integrasjon o.l.)


---

### Testanatomi

```
public class WhatWeWantToVerifyTest {

    @Test
    public void assumptionForTestAndExpectedOutcome() {
       //Given
       ThingToTest ttt = new ThingToTest();
       Result expected = new Result().withExpectedValues();

       //When
       Result result = ttt.methodToBeTested();

       //Then
       assertEquals(expectedValue, result);
    }
}
```


Note: 
- vis en test i kode -- forklar hva de ulike delene skal gjøre
- annotasjon: denne testen skal kjøres automatisk
- navn: forretningsforklaring! Dette er dokumentasjon. testnavn forklarer
  hvordan virker (spesifikke forretningsregler). Forklare hensikt
- Given: Hvordan ser verden ut når du starter testen? Også kalt precondition (arrange, precondition)
- When: Oppførselen du tester (act)
- Then: Verifisere at resultatet av det du har gjort gir korrekt resultat (assert, postcondition)



---

### En god test er begrenset

Note:
- test et konsept om gangen
- lett å forstå hva testen tester og få oversikt
- viser hvilken kode som er nødvendig for å oppnå det ene konseptet
- letter å forstå hva som blir ødelagt når testen feiler
- kortere å navngi testen



---

### En god test tester oppførsel

Note:
- tester oppførsel, ikke implementasjonsdetaljer (med mindre det er en del av
  oppførselen som er kritisk). Tenk på systemet du tester som en svart boks, du
  har kun mulighet til å gi inn input og få output tilbake. Alt på "innsiden" av
  boksen skal du ikke teste.
- Eks: ikke test verdier på interne variabler i en klasse, kun det du får
  tilbake.
- Dårlig eksempel: order.set(age, drink) etterfulgt av order.allowedPurchase,
  der allowedPurchase er private member.
- Godt eksempel: order.set(age, drink) etterfulgt av order.isValid(), der
  isValid() er en public-metode som sjekker order.allowedPurchase-variabelen
- Om order.allowedPurchase byttes ut med noe annet påvirkes ikke den siste
  testen
- Tester som tester implementasjonsdetaljer gjør kodeendring vanskelig over tid
  (gir skjør kode (brittle))



--- 

### En god test er dokumentasjon

Note: 
- tester viser hvordan koden din er ment til å brukes
- nye folk på prosjektet (evt deg selv om et halvt år) kan bruke tester til å
  sette seg inn i prosjektet
- god navngiving på tester gir deg en kort beskrivelse av hvordan systemet
  oppfører seg
- eksempel: testNonValidIdFails() { String id = "ab"; } vs
  testIdWithoutHyphenIsRejected() { String id = "ab"; } (her bør det også være
  med en test som viser hva en gyldig id er
- mer spesifikt:
- viser hvilke parametre som trengs for å utføre en oppgave
- viser hvilken type parametrene skal være (evt ikke være)
- viser hva som er gyldige verdier, og ikke gyldige
- viser hva slags returverdier du kan få
- viser hva som er tiltenkt feilhåndtering
- gjem vekk alt annet enn det som er kritisk for testen (kan være funksjoner som
  hjelper deg med å sette opp inputdata osv)



---

### En god test avslører antagelser

Note: 
- Eks: nettbutikk. Du velger det du vil kjøpe og skal sende det. Når systemet først
  lages finnes det bare en måte å sende pakken på, og du må taste inn et sett
  med informasjon. Seks mnd etterpå finnes det fire ulike måter å sende pakker
  på, og testene må reflektere dette
- testnavn kan i utgangspunktet være: validAddressInformation(), men hvis ulike
  firma krever ulik informasjon trenger du testnavn (og tester) som reflekterer
  dette. Første testnavn er tvetydig, for det sier ikke noe om hvilken
  informasjon som er viktig og for hvilken shippingmetode det er viktig

--- 

### Tester gjør deg til din første bruker

Note: 
- gir "kundefokus" når du utvikler. 
- hvem er kunden? Deg og andre utviklere. 

---

### Vanlige testrammeverk dere kommer borti

* @size[0.6em](AssertJ)
* @size[0.6em](Hamcrest)
* @size[0.6em](Cucumber)
* @size[0.6em](Karate)
* @size[0.6em](mockito: mock-rammeverk)
* @size[0.6em](jest)
* @size[0.6em](mocha)
* @size[0.6em](sinon: mock-rammeverk)
* @size[0.6em](cypress)

---

### TDD er en utviklingsmetodikk

Note: 
- Top down: design før implementasjon, helt ned på detaljnivå for funksjoner
- Ved å skrive testen først, må du tenke gjennom akseptansekriterier (hva du
  skal oppnå) før du begynner å kode
- sammeligne med å tegne huset før du bygger det?


---

### Testen skal feile

Note:
- Hvis ikke testen feiler, vet du ikke at du tester det du tror du tester
- Hvis testen er grønn fordi du har gjort en feil i testen, tror du feilaktig at
  du har dekket oppførsel du ønsket å teste
- Hvis du skriver tester for eksisterende kode, gå inn i koden og ødelegg slik
  at du ser at testen feiler på riktig måte
- Når testene går gjennom (blir grønne), kan man forbedre koden (refaktorere
  koden)
- Denne syklusen kalles red-green-refactor



---?image=https://jfiaffe.files.wordpress.com/2014/09/redgreenrefacor.png&size=35%

Note:
- ved å skrive testen først 

---

### Pricing Kata

Note:
- dagens oppgave
