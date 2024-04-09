# Oppitunninmuistiinpanot
## 9.4
Asensin gitin Linuxin virtuaalikoneelle ja omalle mac -tietokoneelle.
1. asenna git

       $ sudo apt-get -y install git
2. Kerro gitille nimi ja sähköposti

       $ git config --global user.email "sähköposti"
       $ git config --global user.name "etunimi sukunimi"
3. Luo avaimet

       $ ssh key-gen                      #Linux komento
       $ ssh-keygen                       #Mac komento 
5. kopioi julkinen avain /home/vagrant/.ssh/id_rsa.pub -hakemistosta ja kopioi se githubiin. Github - asetukset - ssh key - add new key. Mac -koneella /Users/mirellasiponen/.ssh/id_rsa.pub -hakemisto.
      
       $ cat id_rsa.pub
6. Kopioi Githubista kurssin reposition ssh linkki
![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/468a6534-4ff2-4fb1-85aa-49e0b535e465)

       $ git clone git@github.com:Lambizzzz/infra-as-code.git
Nyt github on linkitetty päätteeseen. Saa muokattua jo tehtyjä tiedostoja ja luoda uusia.

### Tärkeitä komentoja 

git add . && git commit; git pull && git push
