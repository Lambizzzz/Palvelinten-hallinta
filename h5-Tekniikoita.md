# Viides harjoitus, Tekniikoita
## x) Lue ja tiivistä
### Using Salt with Windows - Tuomas Valkamo ([2022](https://tuomasvalkamo.com/CMS-course/week-5/))
- Luo uusi tekstitiedosto
- Kerää tietoja koneesta ja kirjoita ne luotuun tekstitiedostoon
- Tarkista onko TCP portti auki
  
## a) Asenna Salt Macille ([Saltproject](https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/macos.html#))
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
Katsoin viimeisimmäksi muokatut tiedostot koneeltani find -toimintoa käyttäen. Tehtävässä käytin apuna Karvisen [ohjeita](https://terokarvinen.com/2018/04/03/apache-user-homepages-automatically-salt-package-file-service-example/)(2018). 

1. Siirryin kotihakemistoon ja ajoin alla olevan komennon.

       $ find -printf "%T+ %p\n"|sort
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/e245ed11-4871-4f23-9648-a9015cb505bb)

> Kuva 6. Suoritin komennon kotihakemistossa find-toimintoa käyttäen.

Komento ei antanut minulle haluttua tulosta ja ilmoittaa komennon olevan laiton. En löytänyt vastausta saadulle tulokselle ohjeista tai Saltin omilta nettisivuilta.

Yritin samaa komentoa vielä `/etc/` -hakemistossa. 
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/39d08702-be67-45e7-98f0-7187d6758934)

> Kuva 7. Suoritin komennon `/etc/` -hakemistossa find-toimintoa käyttäen.

Tulos oli sama.
## e) Komennus
Loin uuden komennon virtuaalikoneelleni yhden herran ja kahden orjan ympäristössä. 
1. Menin `/usr/local/bin/` -hakemistoon ja loin sinne uuden tekstitiedoston.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/9f2722c3-4e8a-468b-94ab-7c84878955f5)

> Kuva 8. Uuden tekstitiedoston sisältö.

2. Lisäsin kaikille ajo-oikeuden luotuun tiedostoon.

       $ sudo chmod ugo+x foo.sh
3. Loin `init.sls` tiedoston 
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/bb7f7605-9897-4bb7-892f-48af1524a289)

> Kuva 9. init.sls tiedoston sisältö.

4. Ajoin salt-tilan

       $ sudo salt '*' state.apply foo.sh
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/f956ca94-3984-4b8c-ade8-4db584dc092a)

> Kuva 10. Komennon tuloste.

Kokeilin tehtävää Karvisen vinkkien avulla, koska en löytänyt ohjetta tehtävään. En ymmärtänyt mitä tein tai mitä jätin tekemättä tehtävässä, joten sen epäonnistuminen on ymmärrettävää. 

## Lähteet
https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/macos.html#

https://terokarvinen.com/2024/configuration-management-2024-spring/

https://tuomasvalkamo.com/CMS-course/week-5/
