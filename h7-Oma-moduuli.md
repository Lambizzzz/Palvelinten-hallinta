# Seitsemäs harjoitus, oma moduuli
## Palvelinten hallinta kurssin edelliset tehtävät
#### [H1 Viisikko](https://github.com/Lambizzzz/infra-as-code/blob/main/h1-Viisikko.md)
#### [H2 Soitto Kotiin](https://github.com/Lambizzzz/infra-as-code/blob/main/h2-Soitto-kotiin.md)
#### [H3 Toimiva versio](https://github.com/Lambizzzz/infra-as-code/blob/main/h3-Toimiva-versio.md)
#### [H4 Demoni](https://github.com/Lambizzzz/infra-as-code/blob/main/h4-Demoni.md)
#### [H5 Tekniikoita](https://github.com/Lambizzzz/infra-as-code/blob/main/h5-Tekniikoita.md)
#### [H6 Benchmark](https://github.com/Lambizzzz/infra-as-code/blob/main/h6-Benchmark.md)

## Kuvaus projektista
Oman moduulin tavoitteena on luoda herra-orja arkkitehtuuri, jossa herra kone on oma koneeni ja orja on virtuaalikone. Herra koneella voin antaa määräyksiä orjalle. Aion toteuttaa tavoitteen luomalla virtuaalikoneen, asentamalla saltin molemmille koneille ja luomalla koneiden välille yhteyden.

### Työskentely-ympäristö
Oma kone
- OS: MacOS Monterey versio 12.6.6
- Prosessori arkkitehtuuri: x86_64 (AMD64)

Virtuaalikone:
- OS Debian 12 (bullseye)

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

## Orja koneen luominen
Aion luoda virtuaalikoneen Vagrantin avulla. Minulla on asennettuna Virtualbox ja Vagrant, joita tarvitaan virtuaalikoneiden luomiseen.
- [Virtualbox asennus ohjeet](https://www.virtualbox.org/wiki/Downloads)
- [Vagrantin asennus ohjeet](https://developer.hashicorp.com/vagrant/install)
  
1. Loin uuden virtuaalikoneen ja käynnistin sen.

       $ vagrant init debian/bullseye64
       $ vagrant up
       $ vagrant ssh

2. Asensin salt minionin

       $ sudo apt-get update
       $ sudo apt-get install salt-minion

### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/13bb5375-0f6a-4f4a-99c8-0866d1acc673)

> Kuva 4. Salt on asennettu.

3. Siirryin `/etc/salt/minion` tekstitiedostoon ja lisäsin sinne herra koneen ip-osoitteen ja minionin id:n [Saltin ohjeiden mukaisesti](https://docs.saltproject.io/en/latest/topics/tutorials/walkthrough_macosx.html#step-3-connecting-master-and-minion). Tallensin muutokset.

### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/73890989-9eec-4d92-8d95-9d4b2d93179f)

> Kuva 5. Salt minionin konfigurointi tiedosto.

4. Uudelleenkäynnistin salt minionin

       $ sudo systemctl restart salt-minion

Orja kone on valmis.

## Herra kone
Suunnitelmani oli tehdä mac koneesta herra kone, jolla voi antaa määräyksiä orja koneille. Asensin koneelleni Saltin, ohjelmiston omien [nettisivujen tarjoamien ohjeiden](https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/macos.html#macos) mukaan.

1. Tarkistin asennuksen onnistumisen

       $ sudo salt-call --version

### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/d6735053-cf77-47d6-9886-21c07df019c4)

> Kuva 3. Saltin asennus onnistui.

2. Menin hyväksymään orja koneen salt avaimen.

       $ sudo salt-key
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/4af29390-2cec-48b4-8f02-06585fc207b2)

> Kuva 4. Yhtäkään avainta ei ole hyväksyttävänä.

Jostain syystä orja kone ei ole ottanut yhteyttä herra koneeseen. Aloin tutkimaan, jos tulimuuri mahdollisesti estää yhteyden. Saltin herra-orja kommunikaatio käydään `4505/tcp` ja `4506/tcp` porttien kautta. Kokeilin kymmenien nettisivujen ohjeiden mukaisesti avata tcp portteja tuloksetta. Tutkin myös, että toimiiko salt herra koneella.

### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/a33b9e52-4bbf-4169-813e-70ff94ee485f)

> Kuva 5. Salt on asennettu, asennus on luonut konfigurointi tiedostoja ja saltin tilafunktion ajo onnistuu.

Salt toimii herra koneella. Ongelma on todennäköisesti palomuurissa.

## Lähteet

https://brew.sh

https://gist.github.com/michaellihs/b6d46fa460fa5e429ea7ee5ff8794b96#shortcuts

https://www.virtualbox.org/wiki/Downloads

https://developer.hashicorp.com/vagrant/install

https://docs.saltproject.io/en/latest/topics/tutorials/walkthrough_macosx.html#step-3-connecting-master-and-minion

https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/macos.html#macos
       

