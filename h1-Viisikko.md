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

## Saltin asentaminen Linux-virtuaalikoneelle
1. Käynnistin Linux-virtuaalikoneen ja kirjauduin sisään

       $ vagrant up
       $ vagrant ssh
   
3. Asensin Saltin orjan

       $ sudo apt-get update
       $ sudo apt-get -y install salt-minion
4. Tarkistin, että asennus oli toiminut
   
       $sudo salt-call --version
![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/8cf253fc-448d-4772-a22a-ebd0f3f338b5)

## Saltin 5 tärkeintä tilafunktiota


## Lähteet
https://developer.hashicorp.com/vagrant/install
https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/macos.html
