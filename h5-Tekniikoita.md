# Viides harjoitus, Tekniikoita
## x) Lue ja tiivistä
### Using Salt with Windows - Tuomas Valkamo ([2022](https://tuomasvalkamo.com/CMS-course/week-5/))
- Luo uusi tekstitiedosto
- Kerää tietoja koneesta ja kirjoita ne luotuun tekstitiedostoon
- Tarkista onko TCP portti auki
  
## a) Asenna Salt Macille
Minulla oli jo Salt asennettuna Mac-konelleni, joten testasin Saltin toimivuutta alla olevalla komennolla.

    $ sudo salt-call --local state.single pkg.installed tree
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/1240609a-bdd8-48ba-83b7-a2f1fd8211ac)

> Kuva 1. Puu-paketin asennus onnistui eli salt toimii.

## b) Kerää Mac-koneesta tietoa grains.items -toiminnolla
## c) Kokeile Saltin file -toimintoa Macilla
## d) CSI Kerava
## e) Komennus
## Lähteet
