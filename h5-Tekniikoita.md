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
Keräsin keskeisiä ja mielenkiintoisia tietoja koneestani grains.items -toiminnolla.

    $ sudo salt-call --local grains.items
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/e6212b21-fc10-4e73-9acd-5fbecc184dbc)

> Kuva 2. Koneen käyttöjärjestelmä on MacOS.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/dd3bcf92-2b35-4436-bbe0-a489782dcd05)

> Kuva 3. Koneelleni on asennettu saltin versio 3007.0. 

### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/53f5b5c4-7bc6-4888-907f-e86975de4a83)

> Kuva 4. Tietokoneessani on 64-bittinen AMD prosessori.

### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/4be524c3-6c4e-4605-8ece-7e6909f0c1aa)

> Kuva 5. Tämänhetkinen hakemistoni.

## c) Kokeile Saltin file -toimintoa Macilla
## d) CSI Kerava
## e) Komennus
## Lähteet
