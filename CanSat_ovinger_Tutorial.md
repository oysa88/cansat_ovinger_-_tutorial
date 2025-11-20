# CanSat Øvinger Tutorial

### @diffs true

## Del 1: @unplugged

### CanSat Øvingsoppgaver @unplugged

I denne veiledningen skal vi gå gjennom grunnleggende funksjoner som dere får bruk for når dere skal programmere en CanSat. 

**Oppgaver dere skal løse er: **

- **1)** Få et LED-lys til å blinke ved koble det til pins på micro:betingelse
- **2)** Lage en teller som teller fra 10 til 0, og som skrur på LED-lyset i 5 sekunder.
- **3)** Bruke en OLED-skjerm, og vise nedtellingen på skjermen.
- **4)** Lege et voltmeter som skriver spenningen til OLED-skjermen.
- **5)** Lese analogverdi fra en TMP36 (Temperatursensor) og konvertere disse til temperaturverdier vi viser på OLED-skjermen.

Lykke til!


## Del 1.1: @unplugged

### Oppgave 1 - Koble LED-lys til CanSat

Koble opp kretsen som vist på bildet under.

NB: Koble pluss på LED til ingangen P0 og minus til jord (GND).

![microbit-ovelse-1-LED.jpg](https://i.postimg.cc/wBXCyNSs/microbit-ovelse-1-LED.jpg)


## Del 1.2:

### Oppgave 1: Få LED-lyset til å skru seg AV og PÅ én gang hvert sekund.

Inni ``||basic: gjenta for alltid||``:

Finn blokken ``||pins: skriv digital til||`` som vi skal bruke for å skru AV og PÅ LED-lyset vi har koblet til CanSat. Sett verdien til 1 for å skru lyset PÅ og 0 for å skru det AV.

Bruk en ``||basic: pause||`` for å si hvor lenge lyset skal være PÅ og AV.

**Ekstra**: Endre hvor fort LED-lyset blinker ved å justere på tiden i ``||basic: pause||``-blokken.

**HINT**: 1000 ms i ett sekund


```blocks
basic.forever(function () {
    pins.digitalWritePin(DigitalPin.P0, 1)
    basic.pause(5000)
    pins.digitalWritePin(DigitalPin.P0, 0)
}
```

## Del 2.1:

### Oppgave 2: Telle fra 10 til 0

**Når man skal lage store koder, er det vanlig å bruke ``||functions: funksjoner||``. Inni funksjonen bygger vi koden for det vi vil den skal utføre, og så kaller vi den opp når vi trenger den.**

Start med å lage ``||functions: Funksjonen||`` nedtelling:

For å kunne telle nedover, trenger vi en variabel som kan huske tallet vår. Lag en ny variabel: ``||variables: teller ||``, og sett den inn i ``||functions: nedtelling||``.

Siden vi skal telle ned fra 10 til 0, bruker vi en ``||loops: FOR-løkke ||`` som lar og gjenta løkken akkurat så mange ganger vi ønsker. 

Sett ``||loops: gjenta for indeks ||`` til å kjøres **fra 0 til 10**.

Inni ``||loops: FOR-løkke ||`` skal vi bruke en ``||basic: vis tall ||`` til å vise ``||variables: teller ||``. Og for hver gang den har vist tallet, ``||variables: endre teller med -1 ||``.

Husk å kalle opp ``||functions: nedtelling||`` fra ``||basic: ved start||``.

```blocks
function nedtelling () {
    teller = 10
    for (let indeks = 0; indeks <= 10; indeks++) {
        basic.showNumber(teller)
        teller += -1
    }
}
let teller = 0
nedtelling()
```

## Del 2.2:

### Oppgave 2: Få LED-lys til å lyse i 5 sek.

Bruk de samme blokkene fra oppgave 1 for å skru på LED i 5 sekunder. Endre ``||basic: pause ||`` LED PÅ og AV til 5000 ms.

```blocks
function nedtelling () {
    teller = 10
    for (let indeks = 0; indeks <= 10; indeks++) {
        basic.showNumber(teller)
        teller += -1
    }
    pins.digitalWritePin(DigitalPin.P0, 1)
    basic.pause(5000)
    pins.digitalWritePin(DigitalPin.P0, 0)
}
let teller = 0
nedtelling()
```

## Del 2.3:

### Bestemme når nedtelling av starte

``||functions: Funksjonen nedtelling||`` lar kjører når vi starter micro:biten. Hvis vi vil at den skal kjøres på nytt, kan vi f.eks. kalle den opp når vi ``||input: trykker på knapp A||``.



```blocks
function nedtelling () {
    teller = 10
    for (let indeks = 0; indeks <= 10; indeks++) {
        basic.showNumber(teller)
        teller += -1
    }
    pins.digitalWritePin(DigitalPin.P0, 1)
    basic.pause(5000)
    pins.digitalWritePin(DigitalPin.P0, 0)
}
input.onButtonPressed(Button.A, function () {
    nedtelling()
})
let teller = 0
nedtelling()
```

## Del 3: @unplugged

### Oppgave 3: Skriv til OLED-skjerm

Nå skal vi se på hvordan vi kan bruke en Kitronik OLED-skjerm for å bedre vise dataene våre. 

Skjermen skal kobles til mellom CanSat og micro:bit.

![Kitronik OLED-skjerm](https://www.lekolar.no/globalassets/inriver/resources/133848_118895.jpg)


## Del 3.1:

### Oppgave 3: Sette opp OLED-skjerm

Fra biblioteket ``||kitronik_VIEW128x64: 128x64 Display||``, hent blokkene ``||kitronik_VIEW128x64: turn AV display||`` og ``||kitronik_VIEW128x64: Set font size to Normal||``. 

Plasser begge blokkene inn i ``||basic: ved start||``, og sett display til ``||kitronik_VIEW128x64: PÅ||`` og sett font til ``||kitronik_VIEW128x64: Big||``.

```blocks
kitronik_VIEW128x64.controlDisplayOnOff(kitronik_VIEW128x64.onOff(true))
kitronik_VIEW128x64.setFontSize(kitronik_VIEW128x64.FontSelection.Big)
```


## Del 3.2: 

### Oppgave 3: Vise nedtelling på OLED-skjermen

Fjern ``||basic: vis tall||`` ``||variables: teller||`` fra ``||functions: nedtelling||``. 

Sett istedet inn ``||kitronik_VIEW128x64: clear display||`` og ``||kitronik_VIEW128x64: show||`` ``||variables: teller||`` ``||kitronik_VIEW128x64: on line 1||``.

Last ned koden for å teste!

```blocks
function nedtelling () {
    teller = 10
    for (let indeks = 0; indeks <= 10; indeks++) {
        kitronik_VIEW128x64.clear()
        kitronik_VIEW128x64.show(teller, 1)
        teller += -1
        basic.pause(1000)
    }
    pins.digitalWritePin(DigitalPin.P0, 1)
    basic.pause(5000)
    pins.digitalWritePin(DigitalPin.P0, 0)
}
input.onButtonPressed(Button.A, function () {
    nedtelling()
})
let teller = 0
kitronik_VIEW128x64.controlDisplayOnOff(kitronik_VIEW128x64.onOff(true))
kitronik_VIEW128x64.setFontSize(kitronik_VIEW128x64.FontSelection.Big)
nedtelling()
```


## Del 4

### Oppgave 4: Lage et voltmeter




```package
pxt-kitronik-128x64display=github:kitronikltd/pxt-kitronik-128x64display
```
