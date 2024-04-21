# Neljäs harjoitus, Demoni
## x) Lue ja tiivistä
## a) Hello SLS
Tein Hei maailma -tilan kirjoittamalla se tekstitiedostoon /srv/salt/hello/init.sls. Tehtävässä käytin apuna Karvisen -[ohjetta](https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file) (2023).
1. Loin uuden hakemisto polun `srv/salt/hello` ja siirryin sinne.
2. Loin hello -hakemistoon init.sls ja hellomirella.txt -tekstitedostot Karvisen -[ohjeiden](https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh) (2018) mukaan.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/240874dc-0f85-4778-be32-4e590963652d)

> Kuva 1. init.sls ja hellomirella.txt -tekstitiedotojen sisällöt.

3. Suoritin tilafunktion orjakoneille.

        $ sudo salt '*' state.apply hello
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/e6e66d00-bcf1-49f7-836d-6b622850eac5)
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/7b4a037f-ebae-4975-be21-9947bcba6e6c)

> Kuvat 2 & 3. Tilan suoritus onnistui.

## b) Top
### Käsin
Tein tämän tehtävän samassa ympäristössä kuin edellisen tehtävän. 
1. Loin `/srv/salt/` -hakemistoon top.sls -tekstitiedoston.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/b9004335-2817-4741-935e-d5351444673d)

> Kuva 4. top.sls -tektisiedoston sisältö.

2. Suoritin tilafunktion orjakoneille.

        $ sudo salt '*' state.apply hello
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/c6c8a74f-19d2-4e92-b4fb-1d8b3707a14e)

> Kuva 5. Tilan suoritus onnistuu automaattisesti kaikille koneille.
## c) Apache easy mode
Testasin apachen käyttöä ja testisivun tekemistä ensiksi käsin.
1. Asensin Apachen ja testasin yhteyttä.

        $ sudo apt-get update
        $ sudo apt-get install apache2
        $ wget http://localhost/
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/0e28bcae-b145-4bf0-853f-a4ca75f4065c)

> Kuva 6. Yhteys toimii.

2. Menin hakemistoon `/home/vagrant/` ja loin sinne uuden kotisivu -tekstitiedoston.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/92ce6f91-8e63-4fe8-8715-48ca713c7ff9)

> Kuva 7. Kotisivun sisältö.

3. Menin hakemistoon `/etc/apache2/sites-available` ja loin sinne Mirella.conf -tekstitiedoston. 
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/5c12c482-a31b-493c-8c36-5296515c045a)

> Kuva 8. Mirella.conf tiedoston sisältö.

4. Vahdoin hakemistoon `/etc/apache2/sites-enabled` ja loin sinne symbolisen linkin Mirella.conf tiedostoon.
   
        $ sudo ln -s ../sites-available/Mirella.conf .
5. Potkasin daemonia uudelleen käynnistämällä Apachen. Tarkistin myös statuksen ja testasin curlilla, että kotisivu näkyy. 

        $ sudo systemctl restart apache2
        $ sudo systemctl status apache2
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/39b31db1-8785-4420-abc2-343a722bbc4d)
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/1c05bed0-85bd-486d-95fc-a7b07eef840c)

> Kuva 9 & 10. Testi onnistui.
### Automaattisesti
Tässä tehtävässä käytin tunnilla tehtyä skriptiä. 
1. Loin uuden hakemistopolun `/srv/salt/apache/`. Lisäsin sinne init.sls tiedoston, johon kopioin tunnilla tehdyn skriptin.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/7f0a9844-4549-4a9a-979e-480cb6b61ffc)

> Kuva 11. Skripti.

2. Loin testisivun `/home/vagrant/publicsites/` -hakemistoon skriptin mukaisesti.
3. Ajoin `sudo salt-call --local -l info state.apply apache` -komennnon. Muut toiminnot onnistuivat, mutta sain virhekoodin `service.running` -funktion kohdalle. Yritin ottaa selvää ongelmaan ja korjata sitä, mutta en ymmärrä miten virheen voi korjata.

### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/e2c5e91b-8d74-475c-bf78-dfbc4befab55)
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/99c78983-6c45-473a-8f1e-e463f7c82672)

> Kuvat 12 & 13. Virhekoodit.


## d) SSHouto
## Lähteet
