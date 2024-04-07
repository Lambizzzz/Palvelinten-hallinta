# Toinen harjoitus, Soitto kotiin
## x) Lue ja tiivistä
### Two Machine Virtual Network With Debian 11 Bullseye and Vagrant ([Karvinen 2021](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/))
- Luo kahden koneen virtuaaliverkko Debianille Vagrantin avulla
    - Asenna Vagrant 
    - Luo uusi hakemisto, mihin laitat Vagrantfile -tiedoston
    - Luo tekstitiedosto nanolla, mihin lisäät valmiiksi tehdyn [scriptin](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/#vagrantfile)
- Voit tuhota koneen nopeasti yhdellä komennolla `$ vagrant destroy`

### Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux ([Karvinen 2018](https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux))
- Asenna saltin herra ja orja
- Luo herran ja orjien välille yhteys
- Testaa yhteyttä kokeilemalla komentoja orjille
  
### Hello Salt Infra-as-Code ([Karvinen 2014](https://terokarvinen.com/2024/hello-salt-infra-as-code/))
- Asenna Salt
- Luo kansio, johon luot tekstitiedostoon koodia
- Suorita koodi

## a) Kaksi virtuaalikonetta samassa verkossa
Loin kahden koneen virtuaaliverkon Vagrantin avulla. Jos Vagrantia ei ole asennettuna, ohjeet siihen löytyy Vagrantin [sivuilta](https://developer.hashicorp.com/vagrant/install).
Kaikki toiminnot ja komennot tein koneen terminaalissa.
1. Loin uuden hakemiston ja menin siihen hakemistoon.

       $ mkdir twohost/; cd twohost/
2. Loin hakemistoon uuden tekstitiedoston nano -tekstiedittorilla.

       $ nano Vagrantfile
3. Lisäsin tekstitiedostoon Tero Karvisen valmiin [skriptin](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/#vagrantfile).

### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/609eb8de-75cf-43d6-a23b-6262773a3c96)

> Kuva 1. Skripti liitettynä nanolla luotuun tekstitiedostoon nimeltä Vagranfile.

Skriptin koodi luo valmiiksi kaksi virtuaalikonetta samaan verkkoon, luo niille hakemistopolut ja asentaa niihin tree -ohjelman. Koneille luodaan myös omat isäntänimet ja yksityiset ip-osoitteet.

| kone  |t001|t002|
|---|----|----|
|ip|192.168.88.101|192.168.88.102|

4. Suoritin `$ vagrant up` -komennon, joka käynnisti luodun vagrant-ympäristön muutamassa minuutissa.
5. Testasin, että molemmat koneet toimivat ja pystyn pingaamaan koneet toisiinsa. Pingaaminen on tapa, millä testataan kahden samassa verkossa olevan koneen välistä yhteyttä. Pingaamiseen käytetään toisen koneen ip-osoitetta.

        $ vagrant ssh t001
   
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/446008e6-078b-4179-a715-608f7fb42e5e)

> Kuva 2. Kirjautuminen t001 koneelle toimii.
        
        $ ping -c 1 192.168.88.102
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/c288d094-9e3e-4901-8d98-3ea3f16f6f3a)

> Kuva 3. t001 koneelta saa onnistuneesti otettua yhteyttä t002 koneeseen.

        $ exit
        $ vagrant ssh t002
        
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/8a680632-d6c3-4eaa-ae10-d648622b3857)

> Kuva 4. Kirjautuminen t002 koneelle toimii.

        $ ping -c 1 192.168.88.101

### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/65070897-f569-479b-a1ad-880296a5400e)

> Kuva 5. t002 koneelta saa onnistuneesti otettua yhteyttä t001 koneeseen.

## b) Herra-orja arkkitehtuuri verkon yli
Tavoitteena on luoda asetelma, jossa herra ja orja ovat eri virtuaalikoneilla. Herra antaa komentoja orjalle verkon yli ja orja pystyy vastaamaan niihin. Loin asetelman Karvisen ([2023](https://terokarvinen.com/2023/salt-vagrant/)) ohjeen mukaan. Tämän ohjeen mukaisesti luotu asetelma tulee sisältämään yhden herran ja kaksi orjaa. Ohjeesta poiketen käytin nano -tekstieditoria micron sijasta. Käytin tehtävään Vagrantia. 
1. Loin uuden hakemiston ja loin sinne tekstitiedoston nanolla.

       $ mkdir saltdemo; cd saltdemo
       $ nano Vagrantfile   
2. Kopioin Karvisen ohjeesta [skriptin](https://terokarvinen.com/2023/salt-vagrant/#ready-made-vagrantfile-for-three-computers) ja liitin sen tektitiedostoon. Skripti luo valmiiksi kolme virtuaalikonetta, yhden herran ja kaksi orjaa. Kaikilla luoduilla virtuaalikoneilla on omat nimet ja ip-osoitteet.
   
|Kone|tmaster|t001|t002|
|---|-------|----|----|
|ip|192.168.12.3|192.168.12.100|192.168.12.102|
|rooli|herra|orja|orja|

4. Suoritin `$ vagrant up` -komennon, joka käynnisti luodun vagrant-ympäristön noin viidessä minuutissa.
5. Jotta herran ja orjien välinen yhteys toimii, on kirjaututtava herra -koneeseen ja hyväksyttävä orjien lähettämät avaimet.
   
       $ vagrant ssh tmaster
       $ sudo salt-key -A
### ![Näyttökuva 2024-4-6 kello 11 20 04](https://github.com/Lambizzzz/infra-as-code/assets/148875838/ee478200-270d-4bdc-b6b1-3a884bda1ea2)

> Kuva 6. Avaimet ovat hyväksytty.

Nyt tavoiteltu asetelma pitäisi olla luotuna. Testasin vielä, että yhteys toimii.

6. Otin herra koneella yhteyttä orja koneisiin Saltin luoman suojatun kanavan kautta.

       $ sudo salt '*' test.ping
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/608a4014-80c2-4cf2-924a-75c98d75b3dd)

> Kuva 7. Yhteys toimii.

## c) Shell-komennon ajaminen orjalla verkon yli
Shell-komennon voi antaa yhdelle, usealle tai kaikille koneille samanaikaisesti. 
1. Testasin herra koneella antaa komentoja orja koneille.
   
          $ sudo salt '*' cmd.run 'hostname -I'
Komento kysyy orja koneilta niiden ip-osoitteita.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/926df7d6-c424-47c5-8537-160c064563cd)

> Kuva 8. Molemmat orja koneet ilmoittavat ip-osoitteensa herralle.

2. Testasin antaa vain yhdelle orja koneelle komennon

          $ sudo salt 't001' cmd.run 'ls -la /home'
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/71fd1584-1f13-4dc0-a565-e2b43e3c2af9)

> Kuva 9. t001 kone listaa hakemistot ja tiedostot home -hakemistosta.

## d) Idempotentti (state.single) komentojen ajaminen verkon yli.
Orja koneille voi myös antaa idempotentti komentoja, jossa kuvataan haluttu lopputulos ja muutoksia tehdää vain jos sille on tarvetta.

1. Kokeilin antaa kaikille orja koneille komennon käyttäen pkg -tilafunktiota. Komento kuvaa lopputuloksen, jossa kaikilla orja koneilla on apache2 asennettuna. 

          $ sudo salt '*' state.single pkg.installed apache2

### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/32d1c373-20f4-4aa7-bae3-f9996527c092)

> Kuva 10. Apache2 asennettiin t002 koneelle.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/a3e90b9a-5498-4c4a-ba42-a53af9274e84)

> Kuva 11. Apache2 asennettiin t001 koneelle.

2. Testasin, että Apache2 on käynnissä.

          $ sudo salt '*' state.single service.running apache2
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/59ad85c2-1f5f-43dc-bc83-91be4a8f87a9)

> Kuva 12. Apache2 on käynnissä molemmilla orja koneilla.

3. Kokeilin vielä file -tilafunktiota

          $ sudo salt '*' state.single file.managed '/tmp/see-you-at-terokarvinen-com'
   
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/991a4f32-6a18-4ddc-ba6f-a537cb243d08)

> Kuva 13. Uusi tiedosto on luotu t001 koneelle.

### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/223017f5-a0d1-4d5b-ad7c-b4d27d866781)

> Kuva 14. Uusi tiedosto on luotu t002 koneelle.

## e) Teknisten tietojen kerääminen orjista verkon yli (grains.item)
1. Katsoin orjien tämän hetkisen hakemiston.

         $ sudo salt '*' grains.item cwd
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/6b0b7125-fbb5-4869-a7a5-a61045c2ab17)

> Kuva 15. Molemmat orjat ovat juuressa.
2. Katsoin orjien käyttöjärjestelmät.

        $ sudo salt '*' grains.item os
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/c65de15a-caa7-4ce2-8333-543d3424daa9)

> Kuva 16. Molemmissa orja koneissa on Debian käyttöjärjestelmä.

## f) Infraa koodina
Seurasin Karvisen (2024) [ohjetta](https://terokarvinen.com/2024/hello-salt-infra-as-code/). 
1. Loin uuden hakemistopolun ja menin polun viimeiseen hakemistoon.
   
        $ sudo mkdir -p /srv/salt/hello/
        $ cd /srv/salt/hello/

2. Avasin tekstieditorilla tekstitiedoston nimeltä init.sls ja kirjoitin sinne idempotentti koodia.

        $ sudoedit init.sls

        /tmp/hellotero:
          file.managed
3. Suoritin komennon tarkistaakseni hello -hakemiston tilan.

        $ sudo salt-call --local state.apply hello
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/3b29d5ff-7dd4-4d00-9127-e53c64131599)

> Kuva 17. Uusi tiedosto /tmp/hellotero on onnistuneesti luotuna.
4. Ajoin tilan orjille

        $ sudo salt '*' state.apply hello
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/e755f0a4-0bf8-433e-a995-98a7f4298b83)

> Kuva 18. Ajo onnistui.

## Lähteet
1.  https://terokarvinen.com/2024/configuration-management-2024-spring/
