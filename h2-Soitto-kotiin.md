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






- Luo orjalla tekstitiedosto, mihin kirjoitat herran ip-osoitteen
  
![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/d31fdece-bab7-4172-ac42-0364c8cd1bea)
