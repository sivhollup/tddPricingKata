---?image=flyt_monster_mork_bakgrunn.svg&size=120%
# Testing og TDD

Note:
- bootcamp: serie med aktiviteter for nyutdannede nyansatte, vil foregå utover
  høsten
- første del handler om kodekvalitet: testing/tdd og refaktorering
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
    public void explainBusinessRuleUnderTest() {
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
- lettere å forstå hva som blir ødelagt når testen feiler
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


---

```
//Nope
@Test
public void validAge() {
    Order order = new Order();
    order.set(underAge, drink);
    assertFalse(order.isOfLegalAge);
}

//Better
@Test
public void mustBeAboveLegalAgeToOrderDrinks() {
    Order order = new Order();
    order.set(ungerAge, drink);
    assertFalse(order.isValid());
}
```

Note:
- Dårlig eksempel: teste om person har lov å bestille en cocktail.
  isOfLegalAge er en intern representasjon, implementasjonsdetalj
- Om order.isOfLegalAge byttes ut med noe annet påvirkes ikke den siste
  testen
- isValid() er en public-metode som sjekker order.allowedPurchase-variabelen
- isValid() implementerer gjerne andre forretningsregler også
- kall metodene som andre deler av koden skal konsumere (black-boks-prinsippet)
- tester påvirker hvordan du skriver koden din 
- Tester som tester implementasjonsdetaljer gjør kodeendring vanskelig over tid
  (gir skjør kode (brittle))



--- 

### En god test er dokumentasjon

```
//Nope
@Test
public void testNonValidIdFails() {
    String id = "ab";
    ...
}

//Better
@Test
public void idMustHaveHyphen() {
    String id = "ab";
}
```

Note: 
- tester viser hvordan koden din er ment til å brukes
- nye folk på prosjektet (evt deg selv om et halvt år) kan bruke tester til å
  sette seg inn i prosjektet
- god navngiving på tester gir deg en kort beskrivelse av hvordan systemet
  oppfører seg
- her bør det også være
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

* @size[0.6em](JUnit)
* @size[0.6em](AssertJ)
* @size[0.6em](Hamcrest)
* @size[0.6em](Cucumber)
* @size[0.6em](Karate)
* @size[0.6em](mockito: mock-rammeverk)
* @size[0.6em](jest)
* @size[0.6em](mocha)
* @size[0.6em](sinon: mock-rammeverk)
* @size[0.6em](cypress)

Note:
- OK, tester er fint, men hvordan jobber vi med tester? 
- når har dere skrevet tester? før prodkode? etter? mens? 


---

### Test-drevet utvikling (TDD)

Note:
- TDD er en utviklingsmetodikk
- vi driver utviklingen fremover ved å skrive testene først
- høres enkelt ut, men er en helt annen måte å tenke på 
- koden blir annerledes enn om du skriver impl.-koden først. 
- hvorfor? Fordi du må bruke koden selv. Fører til løsere koblet kode
- Gjort riktig senker det risiko i prosjektet, fordi testene alltid kjøres (du
  vet om noe knekker)


---

### TDD setter fokus på design 

Note: 
- Top down: design før implementasjon, helt ned på detaljnivå for funksjoner
- Ved å skrive testen først, må du tenke gjennom akseptansekriterier (hva du
  skal oppnå) før du begynner å kode
- sammeligne med å tegne huset før du bygger det



---?image=https://jfiaffe.files.wordpress.com/2014/09/redgreenrefacor.png&size=35%

Note:
- bilde red/green/refactor
- TDD red-green-refactor
- 1. Skriv test som feiler. Den kan gjerne bruke kode som ikke finnes ennå, da
  lager du den etterhvert som du trenger. 
- 2. Lag en minimal implementasjon som gjør at testen(e) går gjennom
- 3. Hvis nødvendig, forbedre eksisterende kode, både i test og produksjonskode.  


---

### Test først kjennes tregt ut i begynnelsen

Note:
- Å skrive testen først kjennes ut som feil ende å begynne i
- Test først virker veldig tregt. Har masse av løsningen planlagt i hodet, men
  en tanke er ikke like gjennomarbeidet som det vi tror. 



---

### Test først gjør kursendring enklere

Note: 
- Virkeligheten er kanskje annerledes enn vi trodde, og ved å skrive testen
  først avsløres dette fortere enn om du skrive masse implemetnasjonskode først
- Vanskeligere å skrive om når du allerede har gjort mye. 



---

### Testen skal feile

Note:
- Hvis ikke testen feiler, vet du ikke at du tester det du tror du tester
- Hvis testen er grønn fordi du har gjort en feil i testen, tror du feilaktig at
  du har dekket oppførsel du ønsket å teste
- Hvis du skriver tester for eksisterende kode, gå inn i koden og ødelegg slik
  at du ser at testen feiler på riktig måte


---

### Implementer kun nok til å få testen til å kjøre

Note: 
- Selv om du har ideer om forbedringer, ikke gjør det før testen er grønn
- Grønn == trygg. Når du har en fungerende implementasjon, kan du lage
  forbedringer


--- 

### Forbedringer gjøres når alle testene kjører

Note: 
- forbedringer kan gjøres både på testkode og på produksjonskode
- testkode utgjør lett halvparten av kodebasen! 
- tester kan bli overflødige, slett dem! 


---

### Testkode er også kode

Note:
- testkode har samme krav til kvalitet som produksjonskode
- det blir mange tester, lag hjelpefunksjoner og klasser for å klare å
  vedlikeholde dem (ingen gidder å fikse 500 steder hvis API-et endrer seg)


---

### Demo


---

### Pricing Kata

Note:
- dagens oppgave
