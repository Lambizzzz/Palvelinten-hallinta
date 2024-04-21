# Neljäs harjoitus, Demoni
## x) Lue ja tiivistä
## a) Hello SLS
Tein Hei maailma -tilan kirjoittamalla se tekstitiedostoon /srv/salt/hello/init.sls. Tehtävässä käytin Karvisen -[ohjetta](https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file)(2018).
1. Loin uuden hakemisto polun `srv/salt/hello` ja siirryin sinne.
2. Loin hello -hakemistoon init.sls ja hellomirella.txt -tekstitedostot Karvisen -[ohjeiden](https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh) mukaan.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/240874dc-0f85-4778-be32-4e590963652d)

> Kuva 1. init.sls ja hellomirella -tekstitiedotojen sisällöt.

3. Suoritin tilafunktion orjakoneille.

        $ sudo salt '*' state.apply hello
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/e6e66d00-bcf1-49f7-836d-6b622850eac5)
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/7b4a037f-ebae-4975-be21-9947bcba6e6c)

> Kuvat 2 & 3. Tilan suoritus onnistui.

## b) Top

## c) Apache easy mode
## d) SSHouto
## Lähteet
