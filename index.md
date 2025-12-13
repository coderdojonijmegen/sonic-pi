---
title: "Sonic Pi - december"
date: 2025-12-06T14:29:01+01:00
draft: false
toc: true
headercolor: "teal-background"
onderwerp: SonciPi 
---

Met Sonic Pi kun je muziek programmeren als code! In deze instructie gaan we wat muziek maken, passend in de maand december.

<!--more-->

## Introductie

Sonic Pi is een programma geschreven door Sam Aaron en het Sonic Pi Core team. Je kunt er muziek in programmeren en zelfs
live muziek in aanpassen terwijl het speelt!

In deze instructie leren we hoe je muziek kunt maken in Sonic Pi op basis van bladmuziek van eenvoudige liedjes passend
in de maand december. We maken Sinterklaas Kapoentje en Klink klokje klingelingeling. Je leert ook hoe je zelf op basis
van bladmuziek muziek kunt programmeren.

## Wat heb je nodig?

{{< include file="/installatie/sonic-pi" >}}

## Hoe je code schrijft in Sonic Pi

Voordat we naar liedjes kijken, verkennen we eerst even Sonic Pi zelf. Probeer de onderstaande voorbeelden door ze in te typen of te kopiëren en druk elke keer op run om het te horen. Maak vervolgens aanpassingen en luister naar wat er verandert. Sonic Pi is het leukst als je ermee experimenteert, maak vooral fouten en luister goed naar wat wel en niet werkt. 


```ruby
    use_synth :piano

    play :c4
```

Druk nu op de run knop. Wat hoor je?  
Deze code selecteert een piano geluid en speelt de toon C. De 4 geeft aan hoe hoog de C moet zijn. Probeer daar eens een 3 of 5 van te maken en luister naar het verschil. Maak van de C een andere letter zoals G of D en luister naar het verschil. Je kunt ook andere geluiden gebruiken dan piano, probeer eens :saw of :fm en luister naar het verschil. Andere klanken vind je

<details>
<summary>hier</summary>
<pre>
    :dull_bell
    :pretty_bell
    :beep
    :sine
    :saw
    :pulse
    :subpulse
    :square
    :tri
    :dsaw
    :dpulse
    :dtri
    :fm
    :mod_fm
    :mod_saw
    :mod_dsaw
    :mod_sine
    :mod_beep
    :mod_tri
    :mod_pulse
    :tb303
    :supersaw
    :hoover
    :prophet
    :zawa
    :dark_ambience
    :growl
    :hollow
    :mono_player
    :stereo_player
    :blade
    :piano
    :pluck
    :sound_in
    :noise
    :pnoise
    :bnoise
    :gnoise
    :cnoise
    :basic_mono_player
    :basic_stereo_player
    :basic_mixer
    :main_mixer
</details>

### Meer noten
Probeer de onderstaande code eens en druk op run. Hoor je wat je verwacht?

```ruby
    use_synth :piano

    play :c4
    play :e4
    play :g4
```

Er spelen drie noten tegelijk! Dit noemen we een akkoord. Probeer eens hoe het klinkt als je hier de toon van elke noot aan past. Wat klinkt mooit en wat klinkt niet mooi?

Tot nu toe hebben we geluid, maar nog geen muziek. Om een melodie te maken, moet Sonic Pi even wachten tussen elke noot. Dat doen we zo:

```ruby
    use_bpm 120
    use_synth :piano

    play :c4
    sleep 1
    play :e4
    sleep 1
    play :g4
    sleep 1
    play :e4
    sleep 1
    play :c4
```

Met de sleep commando zeg je tegen Sonic Pi dat het 1 tel moet wachten. Hoe lang een tel duurt, wordt bepaald door je bpm: Beats Per Minute, oftewel tellen per minuut. Door dit getal hoger of lager te maken gaat je muziek sneller of langzamer. Kun je de muziek 2x zo snel maken? Of 2x zo langzaam? En wat gebeurt er als je sleep een hoger getal geeft? Of een lager getal?

Let op dat je met programmeren een punt gebruikt in plaats van een komma. Als je bijvoorbeeld een halve tel wilt wachten in plaats van een hele tel, schrijf je `0.5`

### Programmeren in Sonic Pi

Nu dat je de basis kent, is het tijd om het wat interessanter te maken. Probeer dit eens:

```ruby
    use_bpm 120
    use_synth :piano

    live_loop :melodie do
        play :c4
        sleep 1
        play :e4
        sleep 1
        play :g4, decay: 1
        sleep 2
    end
```

Dit bevat wat nieuwe elementen:

* De `live_loop` zorgt ervoor dat de muziek zich blijft herhalen
* De `decay` zorgt ervoor dat de noot iets langer wordt aangehouden. Probeer ook eens decay met de andere tonen. En speel eens met het getal achter decay en de sleep die erop volgt.
* De laatste sleep duurt langer dan de eerste twee, bij elkaar opgeteld kom je tot 4. Als je muziektheorie kent, herken je een 4/4 (vier kwarts) maatsoort. Hier komen we straks op terug.

De live loop is het hart van Sonic Pi. Je kunt meerdere live_loops gebruiken om je muziek gelaagd te maken. Let op dat je niet tussendoor op stop hoeft te klikken, de muziek blijft in de maat:

```ruby
    use_bpm 120
    use_synth :piano

    live_loop :melodie do
        play :c4
        sleep 1
        play :e4
        sleep 1
        play :g4, decay: 1
        sleep 2
    end

    live_loop :beat do
        sync :melodie
        sample :bd_fat
        sleep 2
        sample :sn_dub
        sleep 1
        sample :bd_fat
        sleep 1
        sample :bd_fat
        sleep 2
        sample :sn_dub
    end
```

Het begin is nog hetzelfde, maar nu hebben we twee live loops: een melodie en een beat. De beat gebruikt samples om een soort drumstel te maken. Elke loop heeft een naam, die we kunnen gebruiken om te syncen. Sync zorgt ervoor dat de loops gelijk blijven. Wat gebeurt er als je die regel weg haalt? En wat gebeurt er als je meer sleeps of meer samples in de tweede loop zet?

Ter afsluiting, laten we nog een effect eronder gooien. Laat je code hetzelfde en voeg deze code eronder toe:

```ruby
    live_loop :bass do
        sync :melodie
        sleep 1
        sample :bass_dnb_f
    end
```

Deze sample heeft wel power! Begrijp je alle code tot nu toe? Je kunt nog andere samples verkennen in de Help van Sonic Pi. Er is vanalles, wat je muziek echt tot leven brengt!

Speel hier nog even mee door, of ga verder met deze tekst, want nu weet je genoeg over de code om liedjes te gaan maken!


## Twee voorbeelden

We hebben 2 voorbeelden uitgewerkt voor gebruik in Sonic Pi.  
De voorbeelden komen beide van https://www.pianokinderliedjes.nl. 

### Sinterklaas Kapoentje

![Sinterklaas Kapoentje](scores/Sinterklaas%20Kapoentje.png)

Als je bladmuziek kan lezen, heb je misschien al een idee hoe je dit naar Sonic Pi kan overschrijven. Zo niet, dan helpen we je nog even op weg:

![Uitleg bladmuziek](scores/Uitleg%20Sinterklaas%20Kapoentje.png)

Wat we hier uit halen:

- De maatsoort is 3/4, dat betekent dat er drie tellen in de maat zijn en elke tel is een kwart noot (1/4)
- Een kwart noot kun je dus noteren als `sleep 1`
- Een halve noot kun je noteren als `sleep 2`
- Een rust betekent nog een extra tel wachten voordat de muziek verder gaat, dus in dit geval `sleep 3`
- We hebben handig de toonhoogtes in letters erboven geschreven, de G toon in Sonic Pi is dus `play :g4`

Nu zou je het hele liedje moeten kunnen schrijven in Sonic Pi. Misschien vind je dat nog moeilijk, dus kun je hier onder spieken hoe wij dat hebben gedaan. Voordat je verder leest, probeer het toch maar even

Nog één opmerking voordat we alles uit de kast trekken: we vinden 3 tellen per maat best wel langzaam, dus kiezen wij ervoor om 1 tel per maat te nemen. Dat combineert ook leuker met de beat van de vorige oefening. Om dat te doen moeten we rekenen: elke kwart noot delen we door drie.

Dit is hoe wij het hebben gedaan, er zitten een paar nieuwe trucjes in die we nog niet verteld hebben:

```ruby
    use_bpm 120
    use_synth :piano

    kwart_noot = 1.0 / 3
    halve_noot = kwart_noot * 2
    hele_maat = kwart_noot * 3

    live_loop :melodie do
        2.times do
            # Sin - ter
            play :g4; sleep halve_noot
            play :g4; sleep kwart_noot
            # klaas - Ka
            play :a4; sleep halve_noot
            play :a4; sleep kwart_noot
            # poen
            play :g4, decay: halve_noot
            sleep hele_maat
            # tje,
            play :e4, decay: halve_noot
            sleep hele_maat
        end
        
        # gooi - wat
        play :f4; sleep halve_noot
        play :f4; sleep kwart_noot
        # in - mijn
        play :f4; sleep halve_noot
        play :d4; sleep kwart_noot
        # laars
        play :f4, decay: halve_noot
        sleep hele_maat
        # je
        play :f4, decay: halve_noot
        sleep hele_maat
        
        # dank - u
        play :a4; sleep halve_noot
        play :g4; sleep kwart_noot
        # sin - ter
        play :f4; sleep halve_noot
        play :e4; sleep kwart_noot
        # klaas
        play :d4, decay: halve_noot
        sleep hele_maat
        # je
        play :c4, decay: halve_noot
        sleep hele_maat
    end
```

Dit zijn de nieuwe trucjes:

- Met `kwart_noot = 1.0 / 3` definiëren we een variabele, met een berekening van hoe lang een kwart noot duurt.
- De halve_noot en hele_maat zijn ook variabelen, hoe lang ze duren hangt af van hoe lang de kwart_noot duurt. Als je dus de timing wilt veranderen, hoef je alleen de kwart_noot te veranderen!
- `2.times do` zorgt ervoor dat het eerste stukje twee keer gespeeld wordt.
- De `;` zorgt ervoor dat we play en sleep op 1 regel kunnen zetten.

Probeer nu eens een beat eronder te zetten, kun je een mooie remix maken?

## Zelf aan de slag

Ben je klaar om zelf een liedje om te schrijven? Om in de kerst sfeer te komen, hebben we voor het volgende liedje ook alle tonen erboven geschreven.

### Kling klokje klingeling

![Kling klokje klingeling](scores/Kling-klokje-klingelingeling.png)

Probeer dit nu zelf om te schrijven. Je kunt weer spieken hoe wij het hebben gedaan, maar probeer het eerst zelf. Verken de Help van Sonic Pi om te ontdekken wat je nog meer kan gebruiken.

Tip: zoek op in de Help hoe je een functie definiëert. Omdat de eerste regel zich herhaalt in het lied, kun je de functie later weer aan roepen om die regel niet 2x uit te hoeven schrijven.

<details>
    <summary>Klap dit uit om onze versie te zien</summary>

```ruby
    use_bpm 180
    use_synth :piano

    kwart_noot = 1.0
    achtste_noot = kwart_noot / 2
    halve_noot = kwart_noot * 2
    hele_maat = kwart_noot * 4

    define :eerste_regel do
        # Kling - klok - je
        play :c5, decay: halve_noot
        sleep halve_noot
        play :a4; sleep kwart_noot
        play :bb4; sleep kwart_noot
        
        # klin - ge - lin - ge - ling,
        play :c5; sleep achtste_noot
        play :d5; sleep achtste_noot
        play :c5; sleep achtste_noot
        play :d5; sleep achtste_noot
        play :c5, decay: halve_noot
        sleep halve_noot
        
        # kling - klok - je
        play :bb4, decay: halve_noot
        sleep halve_noot
        play :g4; sleep kwart_noot
        play :c5; sleep kwart_noot
        
        # kling
        play :a4, decay: halve_noot
        sleep hele_maat
    end

    live_loop :melodie do
        eerste_regel
        
        # Laat - de - bood - schap
        play :g4; sleep kwart_noot
        play :g4; sleep kwart_noot
        play :a4; sleep kwart_noot
        play :f4; sleep kwart_noot
        
        # ho - ren,
        play :a4, decay: halve_noot
        sleep halve_noot
        play :g4, decay: halve_noot
        sleep halve_noot
        
        # zin - gen - d'enge - len
        play :bb4; sleep kwart_noot
        play :bb4; sleep kwart_noot
        play :c5; sleep kwart_noot
        play :g4; sleep kwart_noot
        
        # ko - ren,
        play :bb4, decay: halve_noot
        sleep halve_noot
        play :a4, decay: halve_noot
        sleep halve_noot
        
        # voor - die - blij - de
        play :g4; sleep kwart_noot
        play :g4; sleep kwart_noot
        play :a4; sleep kwart_noot
        play :b4; sleep kwart_noot
        
        # klan - ken
        play :c5, decay: halve_noot
        sleep halve_noot
        play :g4, decay: halve_noot
        sleep halve_noot
        
        # wil - len - wij - God
        play :a4; sleep kwart_noot
        play :d5; sleep kwart_noot
        play :c5; sleep kwart_noot
        play :b4; sleep kwart_noot
        
        # dan - ken
        play :d5, decay: halve_noot
        sleep halve_noot
        play :c5, decay: halve_noot
        sleep halve_noot
        
        eerste_regel
    end
```
</details>


## Goed gedaan!

Meer muziek: https://www.pianokinderliedjes.nl/index.php  
Tutorial: https://sonic-pi.net/tutorial.html

{{< licentie rel="http://creativecommons.org/licenses/by-nc-sa/4.0/">}}
