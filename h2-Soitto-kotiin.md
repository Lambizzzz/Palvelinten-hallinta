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

## Kaksi virtuaalikonetta samassa verkossa
Loin kahden koneen virtuaaliverkon Vagrantin avulla. Jos Vagrantia ei ole asennettuna, ohjeet siihen löytyy Vagrantin [sivuilta](https://developer.hashicorp.com/vagrant/install).
Kaikki toiminnot ja komennot tein koneen terminaalissa.
1. Loin uuden hakemiston ja menin siihen hakemistoon.

       $ mkdir twohost/; cd twohost/
2. Loin hakemistoon uuden tekstitiedoston nano -tekstiedittorilla.

       $ nano Vagrantfile
3. Lisäsin tekstitiedostoon Tero Karvisen valmiin [skriptin](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/#vagrantfile).

![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/609eb8de-75cf-43d6-a23b-6262773a3c96)

Skriptin koodi luo valmiiksi kaksi virtuaalikonetta samaan verkkoon, luo niille hakemistopolut ja asentaa niihin tree -ohjelman. Koneille luodaan myös omat isäntänimet ja yksityiset ip-osoitteet.

| kone  |t001|t002|
|---|----|----|
|ip|192.168.88.101|192.168.88.102|

4. Suoritin `$ vagrant up` -komennon, joka käynnisti luodun vagrant-ympäristön muutamassa minuutissa.
5. Testasin, että molemmat koneet toimivat ja pystyn pingaamaan koneet toisiinsa. Pingaaminen on tapa, millä testataan kahden samassa verkossa olevan koneen välistä yhteyttä. Pingaamiseen käytetään toisen koneen ip-osoitetta.

        $ vagrant ssh t001
   
![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/446008e6-078b-4179-a715-608f7fb42e5e)
        
        $ ping -c 1 192.168.88.102
![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/c288d094-9e3e-4901-8d98-3ea3f16f6f3a)


        $ exit
        $ vagrant ssh t002
        
![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/8a680632-d6c3-4eaa-ae10-d648622b3857)

        $ ping -c 1 192.168.88.101

![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/65070897-f569-479b-a1ad-880296a5400e)

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
![Näyttökuva 2024-4-6 kello 11 20 04](https://github.com/Lambizzzz/infra-as-code/assets/148875838/ee478200-270d-4bdc-b6b1-3a884bda1ea2)








- Luo orjalla tekstitiedosto, mihin kirjoitat herran ip-osoitteen
  
![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/d31fdece-bab7-4172-ac42-0364c8cd1bea)
