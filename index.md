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

Voordat we naar liedjes kijken, verkennen we eerst even Sonic Pi zelf. Probeer de onderstaande voorbeelden door ze in te typen of te kopiëren en druk elke keer op play om het te horen. Maak vervolgens aanpassingen en luister naar wat er verandert. Sonic Pi is het leukst als je ermee experimenteert, maak vooral fouten en luister goed naar wat wel en niet werkt. 


```ruby
    use_synth :piano

    play :c4
```

Druk nu op de play knop. Wat hoor je?  
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
Probeer de onderstaande code eens en druk op play. Hoor je wat je verwacht?

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

Let op dat je met programmeren een punt gebruikt in plaats van een komma. Als je bijvoorbeeld een halve tel wilt wachten in plaats van een hele tel, schrijf je `0.5`.

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






Hieronder staat de code voor dit liedje. We beginnen te bepalen met welke snelheid het liedje gespeeld wordt en met welke klank:

- `use_bpm` bepaalt de snelheid, in dit geval 120 beats-per-minute. Speel eens met de waarde en kijk wat er gebeurd.
- `use_synth` bepaalt de klank, in dit geval piano. Andere klinken vind je

Daarna schrijven we de noten uit de bladmuziek hierboven: 

- `play :g4` speelt een G in de 4e octaaf
- `sleep 0.66` bepaalt de duur van de noot (niet van de klank), in dit geval 0,66 seconden

Beide instructies kunnen op hun eigen regel, maar als ze samen op één regel staan, moet er een ; (punt-komma) tussen.

```ruby
    use_bpm 120
    use_synth :piano

    # Sin - ter
    play :g4; sleep 0.66
    play :g4; sleep 0.33
    # klaas - Ka
    play :a4; sleep 0.66
    play :a4; sleep 0.33
    # poen
    play :g4; sleep 1.0
    # tje,
    play :e4; sleep 1.0
    
    # gooi - wat
    play :g4; sleep 0.66
    play :g4; sleep 0.33
    # in - mijn
    play :a4; sleep 0.66
    play :a4; sleep 0.33
    # schoen
    play :g4; sleep 1.0
    # tje
    play :e4; sleep 1.0
    
    # gooi - wat
    play :f4; sleep 0.66
    play :f4; sleep 0.33
    # in - mijn
    play :f4; sleep 0.66
    play :d4; sleep 0.33
    # laars
    play :f4; sleep 1.0
    # je
    play :f4; sleep 1.0
    
    # dank - u
    play :a4; sleep 0.66
    play :g4; sleep 0.33
    # sin - ter
    play :f4; sleep 0.66
    play :e4; sleep 0.33
    # klaas
    play :d4; sleep 1.0
    # je
    play :c4; sleep 1.0

```
### Kling klokje klingeling

![Kling klokje klingeling](scores/Kling-klokje-klingelingeling.png)

```ruby
    use_bpm 60
    use_synth :piano
    
    # Kling - klok - je
    play :c5; sleep 0.5
    play :a4; sleep 0.25
    play :bb4; sleep 0.25
    
    # klin - ge - lin - ge - ling,
    play :c5; sleep 0.125
    play :d5; sleep 0.125
    play :c5; sleep 0.125
    play :d5; sleep 0.125
    play :c5; sleep 0.5
    
    # kling - klok - je
    play :bb4; sleep 0.5
    play :g4; sleep 0.25
    play :c5; sleep 0.25
    
    # kling
    play :a4; sleep 1
    
    # Laat - de - bood - schap
    play :g4; sleep 0.25
    play :g4; sleep 0.25
    play :a4; sleep 0.25
    play :f4; sleep 0.25
    
    # ho - ren,
    play :a4; sleep 0.5
    play :g4; sleep 0.5
    
    # zin - gen - d'enge - len
    play :bb4; sleep 0.25
    play :bb4; sleep 0.25
    play :c5; sleep 0.25
    play :g4; sleep 0.25
    
    # ko - ren,
    play :bb4; sleep 0.5
    play :a4; sleep 0.5
    
    # voor - die - blij - de
    play :g4; sleep 0.25
    play :g4; sleep 0.25
    play :a4; sleep 0.25
    play :b4; sleep 0.25
    
    # klan - ken
    play :c5; sleep 0.5
    play :g4; sleep 0.5
    
    # wil - len - wij - God
    play :a4; sleep 0.25
    play :d5; sleep 0.25
    play :c5; sleep 0.25
    play :b4; sleep 0.25
    
    # dan - ken
    play :d5; sleep 0.5
    play :c5; sleep 0.5
    
    # Kling - klok - je
    play :c5; sleep 0.5
    play :a4; sleep 0.25
    play :bb4; sleep 0.25
    
    # klin - ge - lin - ge - ling,
    play :c5; sleep 0.125
    play :d5; sleep 0.125
    play :c5; sleep 0.125
    play :d5; sleep 0.125
    play :c5; sleep 0.5
    
    # kling - klok - je
    play :bb4; sleep 0.5
    play :g4; sleep 0.25
    play :c5; sleep 0.25
    
    # kling.
    play :a4; sleep 1
```
## Zelf aan de slag

## Goed gedaan!

Meer muziek: https://www.pianokinderliedjes.nl/index.php  
Tutorial: https://sonic-pi.net/tutorial.html

{{< licentie rel="http://creativecommons.org/licenses/by-nc-sa/4.0/">}}
