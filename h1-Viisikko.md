# Ensimmäinen harjoitus, Viisikko
## x) Lue ja tiivistä
Salt komentojen käyttö paikallisesti
  1. Asenna Saltin herra-orja arkkitehtuuri
  3. Testaa Saltin tärkeimpiä tilafunktiota pkg, file, service, user ja cmd.

Verkkosivun luominen GitHubissa
  1. Kirjaudu tai rekisteröidy GitHubiin
  2. Luo uusi julkinen arkisto, mihin lisäät README tiedoston.
  3. Luo uusi tiedosto käyttämällä MarkDown -merkintäkieltä.

  Raportin kirjoittaminen
  1. Täsmällisyys
      - raportoi kaikki tehtävässä käytettävät komennot ja klikkaukset, sekä mitä niistä tapahtui
      - tehtävän täytyy olla toistettavissa samassa ympäristössä vain raportin pohjalta
      - ongelmat ja virheet ovat nopea havaita ja korjata raportoidusta tekstistä
      - viittaa lähteisiin
  
  2. Helppolukuinen
      - Käytä valiotsikoita ja välejä kappaleiden välissä
      - Käytä samaa aikamuotoa kokoajan (imperfekti)
      - Kirjoita huolellista kieltä
    
## a) Saltin asennus Macille
Lataa macOS -käyttöjärjestelmälle suunniteltu asennustiedosto [Saltin -nettisivuilta](https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/macos.html)
ja suorita tiedosto.  

kesken

## b) Vagrant
Kirjauduin Vagrantiin komennolla

        $ vagrant ssh

![Näyttökuva 2024-3-28 kello 12 11 46](https://github.com/Lambizzzz/infra-as-code/assets/148875838/77a569df-8cbb-408a-b005-b720d7332f78)

## c) Uuden Linux-virtuaalikoneen tekeminen Vagrantilla
Jos sinulla ei ole Vagrantia asennettuna, voit asentaa sen [Vagrantin -sivuilta](https://developer.hashicorp.com/vagrant/install)
1. Tee uusi hakemisto ja nimeä se
   
       $ mkdir h1
2. Vie vagrant tiedosto tekemääsi hakemistoon

       $ cd h1
       $ vagrant innit
   ![Näyttökuva 2024-3-28 kello 12 50 28](https://github.com/Lambizzzz/infra-as-code/assets/148875838/7879f82a-062f-4bdd-95a8-9e1747fa634d)
3. luo vagrant box

       $ vagrant debian/bullseye64

Näitä ohjeita seuraamalla olet luonut uuden Linux-virtuaalikoneen

## d) Saltin asentaminen Linux-virtuaalikoneelle
1. Käynnistin Linux-virtuaalikoneen ja kirjauduin sisään

       $ vagrant up
       $ vagrant ssh
   
3. Asensin Saltin herran ja orjan

       $ sudo apt-get update
       $ sudo apt-get -y install salt-master
   
       $ sudo apt-get update
       $ sudo apt-get -y install salt-minion
5. Tarkistin, että asennus oli toiminut
   
       $sudo salt-call --version
![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/8cf253fc-448d-4772-a22a-ebd0f3f338b5)

## e) Saltin 5 tärkeintä tilafunktiota
1. Tarkistin puun version käyttämällä pkg -tilafunktiota. Pkg -tilafunktiolla voi tarkistaa onko jokin sovellus asennettuna ja mikä asennusversio siitä on.

       $ sudo salt-call --local -l info state.single pkg.installed tree
   
![Näyttökuva 2024-3-28 kello 13 44 23](https://github.com/Lambizzzz/infra-as-code/assets/148875838/dbb96b51-8dff-4e68-bafc-70ddcf25456b)

2. Loin ja poistin tiedoston file -tilafunktiolla, jolla voi hallinnoida tiedostoja.

       $ sudo salt-call --local -l info state.single file.managed /tmp/hellotero
![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/846a91cd-d22c-4eb6-b1b2-0dcd35dd61ed)
![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/5e90d591-3849-4d62-a1cd-066658ec7fba)

3. Käytin service -tilafunktiota uudelleenkäynnistämään ja sulkemaan Apache 2 verkkopalvelimen. Service -tilafunktiolla voi hallinnoida daemoneiden käyttöönottoa.

       $ sudo salt-call --local -l info state.single service.running apache2 enable=True

       $ sudo salt-call --local -l info state.single service.dead apache2 enable=False
   ![Näyttökuva 2024-3-28 kello 16 52 00](https://github.com/Lambizzzz/infra-as-code/assets/148875838/edc85582-25cb-4f36-8715-e0d1725f34a3)
   ![Näyttökuva 2024-3-28 kello 16 53 28](https://github.com/Lambizzzz/infra-as-code/assets/148875838/030bb8d0-f9cb-4f9e-ab67-6a54af49eea2)

4. user -tilafunktiolla voi hallinnoida käyttäjätilejä, eli luoda, poistaa ja muokata. 

       $ sudo salt-call --local -l info state.single user.present terote08

       $ sudo salt-call --local -l info state.single user.absent terote08
   ![Näyttökuva 2024-3-28 kello 17 11 01](https://github.com/Lambizzzz/infra-as-code/assets/148875838/51647088-0c29-436b-a2d2-509dd6e2b567)
   
5. cmd -tilafunktiolla voi hallinnoida itse luotuja komentoja. Käytin tilafunktiota hyväksi luomalla tyhjän tiedoston lisäämällä ehdon, joka luo tiedoston vain jos semmoista tiedostoa jo ei ole olemassa.
     
       $ sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo"
   
      ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/cc02fc2f-820d-4f24-a8a4-0cdd3cb2f89e)

## f) Idempotentti

Idempotentti tietotekniikassa tarkoittaa operaatiota tai toimintoa, joka voi suorittaa saman operaation useita kertoja peräkkäin tuottamatta eri tulosta kuin kerran suoritettaessa. ChatGPT (2024).
Tietokanta kysely voi esimerkiksi olla idempotentti, jos niitä voidaan suorittaa useita kertoja peräkkäin tuottamatta eri tulosta.

## g) Tietoa koneesta
Keräsin Saltin grains.items -tekniikalla kolme mielenkiintoista tietoa virtuaalikoneesta.


## Lähteet
1. https://developer.hashicorp.com/vagrant/install
2. https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/macos.html
