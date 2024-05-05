# Kuudes harjoitus, Benchmark
## x) Lue ja tiivistä ([saltstack](https://docs.saltproject.io/en/latest/topics/windows/windows-package-manager.html))
Suosituimmat käyttökohteet Saltin paketinhallintatyökaluille:
- Listaa asennetut paketit
- Tarkista tietyn paketin versio
- Asenna paketti
- Poista paketti
  
## a) Paketti Maccia
Tein tehtävän Mac koneella, johon minulla on asennettuna homebrew. Minun ei tarvinnut tehdä lisä asennuksia tai muutoksia asentaakseni paketteja saltin pkg.installed -funktiolla, koska asennukseen käytettiin brew-paketinhallintaa.
1. Asensin uuden paketin.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/88879940-5438-40dc-a1e3-82c98df00786)

> Kuva 1. Uuden paketin asentaminen saltin avulla onnistui.
## b) Benchmark
### Kristian Koponen - Oma Terraria palvelin ([2020](https://kopkr.github.io/task-palhal/pages/h7.html))
Riippuvuudet: Xubuntu (virtuaalikone)

Asennetut ohjelmat: unzip, Saltstack, Tmux

Kiinnostavaa: Asennusohjeita voi soveltaa muidenkin pelipalvelimien asennuksiin.

Muuta: Lähes kaikki komennot ja tekniikat on käyty [Teron Palvelinten hallinta -kurssilla](https://terokarvinen.com/2024/configuration-management-2024-spring/) ja niitä oli onnistuneesti sovellettu omaan moduuliin.
### Georgios Piperides - Hyödyllisten ohjelmien asennusta ja konfigurointia ([2020](https://jorilinux.wordpress.com/palvelinten-hallinta-viikkotehtava-7/))
Riippuvuudet: Xubuntu (virtuaalikone)

Asennetut ohjelmat: Saltstack, Phpmod, Apache, Cowsay, Cmatrix, Git

Kiinnostavaa: Moduuli on helppo soveltaa muillekin käyttöjärjestelmille.
### Janne Mustonen - Uusien pakettien asennus valmiiksi konfiguroituna ([2020](https://jannelinux.design.blog/2020/05/19/oma-moduuli-h7/))
Riippuvuudet: Ubuntu

Asennetut ohjelmat: Atom, Apache2, Stacer, Git ,SSH, Chromium

Kiinnostavaa: Moduulin avulla työmäärä vähenee selkeästi, jos käytössä on paljon orja koneita, joille asennetaan samat paketit.

Muuta: Konfiguroinnit täytyy tehdä eka herra koneelle, jotta uudelle orja koneelle voi asentaa uusia paketteja valmiiksi konfiguroituna.
## c) Testbench
Valitsin Janne Mustosen moduulin itselleni testattavaksi. Koin sen olevan hyödyllisin minun tarpeisiini ja raportti oli kirjoitettu helposti seurattavaksi. En kuitenkaan asentanut yhtä monta ohjelmaa kuin raportissa oli mainittu. 

1. Loin Apache2 kansion ja lisäsin sinne init.sls tiedoston ohjeiden mukaisesti.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/f47632ff-10de-4773-a78d-ae119a5072f6)

> Kuva 1. Apachen init.sls tiedosto.

2. Loin SSH kansion ja lisäsin sinne init.sls tiedoston ohjeiden mukaisesti.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/c767315d-4166-4366-856a-a19e6487aef0)

> Kuva 2. SSH:n init.sls tiedosto.

Yritin kokeilla terminal muokkauksia, mutta en löytänyt `terminalrc` -tiedostoa tai hakemistoa mistä se olisi pitänyt löytyä. En myöskään onnistunut jäljentämään bash promptin muokkaksia ohjeiden mukaisesti.

Lopuksi oli tarkoitus kokeilla moduulia uudelle virtuaalikoneelle. Raportissa ei oltu selitetty miten uuden virtuaalikoneen voi lisätä herra-orja arkitehtuuriin, vaan siinä oli linkki Tero Karvisen ohjeisiin. 
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/6f18016f-dd0b-4724-b626-a4cba45e612e)

> Kuva 3. Tarvittavaa työkalua ei saa sásennettua.

## d) Viisi ideaa
Viisi ideaa omalla moduulille:
- Oma Minecraft palvelin
- 

## Lähteet
https://terokarvinen.com/2024/configuration-management-2024-spring/

https://kopkr.github.io/task-palhal/pages/h7.html

https://jorilinux.wordpress.com/palvelinten-hallinta-viikkotehtava-7/

https://jannelinux.design.blog/2020/05/19/oma-moduuli-h7/
