# Seitsemäs harjoitus, oma moduuli
## Palvelinten hallinta kurssin edelliset tehtävät
#### [H1 Viisikko](https://github.com/Lambizzzz/infra-as-code/blob/main/h1-Viisikko.md)
#### [H2 Soitto Kotiin](https://github.com/Lambizzzz/infra-as-code/blob/main/h2-Soitto-kotiin.md)
#### [H3 Toimiva versio](https://github.com/Lambizzzz/infra-as-code/blob/main/h3-Toimiva-versio.md)
#### [H4 Demoni](https://github.com/Lambizzzz/infra-as-code/blob/main/h4-Demoni.md)
#### [H5 Tekniikoita](https://github.com/Lambizzzz/infra-as-code/blob/main/h5-Tekniikoita.md)
#### [H6 Benchmark](https://github.com/Lambizzzz/infra-as-code/blob/main/h6-Benchmark.md)

## Kuvaus projektista
Työn lopputulos ja hyödyt,
Tiivistelmä miten päästään lopputulokseen

### Työskentely-ympäristö
Host koneen tiedot:
- OS: MacOS Monterey versio 12.6.6

Virtuaalikoneet:
- OS Ubuntu 

### Asennetut paketit:
- Homebrew: Paketinhallinta Macille, jolla voi asentaa, päivittää ja hallita erilaisia ​​sovelluksia ja työkaluja.
- Tmux: multiplekseri, jolla voi hallita usempaa terminaalia samassa ikkunassa.
- VirtualBox: Virtuaalikoneohjelmisto, joka mahdollistaa esimerkiksi Linux, Windows ja MacOS käyttöjärjestelmien luomisen.
- Vagrant: Virtuaalisten kehitysympäristöjen hallintatyökalu

## Homebrew ja Tmux
Aloitan moduulin tekemisen asentamalla Homebrew paketinhallintajärjestelmän. Homebrew sisältää tarpeellisia paketteja ja kehitystytyökaluja, joita macOS koneista puuttuu. Asensin Homebrew:n [nettisivun ohjeiden mukaisesti](https://brew.sh). 
1. Kopioin nettisivuilta homebrew asennus komennon ja liitin sen macOS terminaaliin.

       $ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

2. Testasin homebrewin asennusta asentamalla sen avulla Tmux paketin. Komennolla homebrew aluksi tarkistaa tarviiko paketinhallintajärjestelmää päivittää ja suorittaa tarvittavat päivitykset. Sen jälkeen haluttu paketti asennetaan.

       $ brew install tmux

### ![Näyttökuva 2024-5-12 kello 13 45 22](https://github.com/Lambizzzz/infra-as-code/assets/148875838/369e6dd4-e489-4f1f-800e-577095050a1a)

> Kuva 1. Tmux asennus onnistui brew:lla.

3. Käynnistin tmuxin komennolla `tmux`, joka avasi uuden istunnon. Kokeilin tmuxia painamalla `ctrl+b` ja `%`, joka jakaa ikkunan pytysuorassa ja lisää uuden istunnon edellisen istunnon viereen.

### ![Näyttökuva 2024-5-12 kello 17 42 30](https://github.com/Lambizzzz/infra-as-code/assets/148875838/b085fc50-67ad-4652-89e3-3de24d529779)

> Kuva 2. Tmux näyttää kahta istuntoa vierekkäin.

Lisää tmuxin näppäinoikotie ohjeita löytyy esimerkiksi [githubista](https://gist.github.com/michaellihs/b6d46fa460fa5e429ea7ee5ff8794b96#shortcuts) (2016). Itse koin haasteita näppäinoikoteitä käyttäessä ja luulin ettei ne toimineet minulla. Pitkään kokeiltuani ja netistä tietoa etsiessäni löysin vastauksen ongelmaani. Olin painanut `ctrl`, `b` ja `%` näppäimiä kaikkia saman aikaisesti. Täytyykin huomioida, että `ctrl` ja `b` näppäimiä painetaan eka yhdessä, vapautetaan ne ja painetaan `%` näppäintä erikseen. 

## Herra kone
Suunnitelmani oli tehdä mac koneesta herra kone, jolla voi antaa määräyksiä orja koneille. Asensin koneelleni Saltin, ohjelmiston omien [nettisivujen tarjoamien ohjeiden](https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/macos.html#macos) mukaan.

1. Tarkistin asennuksen onnistumisen

       $ sudo salt-call --version

### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/d6735053-cf77-47d6-9886-21c07df019c4)

> Kuva 3. Saltin asennus onnistui.

## Orja koneiden luominen
Aion luoda kahden koneen virtuaaliverkon Vagrantin avulla. Minulla on asennettuna Virtualbox ja Vagrant, joita tarvitaan virtuaalikoneiden luomiseen.
- [Virtualbox asennus ohjeet](https://www.virtualbox.org/wiki/Downloads)
- [Vagrantin asennus ohjeet](https://developer.hashicorp.com/vagrant/install)
  
1. Loin terminaalissa uuden hakemiston, johon loin uuden Vagrantfile tekstitiedoston. Liitin tekstitiedostoon [Teron skriptin](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/#vagrantfile). Skripti luo valmiiksi kaksi virtuaalikonetta samaan verkkoon, luo niille hakemistopolut ja asentaa niihin tree -ohjelman. Koneille luodaan myös omat isäntänimet ja yksityiset ip-osoitteet.

| kone  |t001|t002|
|---|----|----|
|ip|192.168.88.101|192.168.88.102|

### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/af6c17be-d275-4e5d-80cf-096f45175f9f)

