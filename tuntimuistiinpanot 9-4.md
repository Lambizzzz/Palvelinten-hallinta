# Oppitunninmuistiinpanot
## 9.4
1. asenna git

       $ sudo apt-get -y install git
2. Kerro gitille nimi ja sähköposti

       $ git config --global user.email "sähköposti"
       $ git config --global user.name "etunimi sukunimi"
3. Luo avaimet

       $ ssh key-gen
4. kopioi julkinen avain /home/vagrant/.ssh/id_rsa.pub -hakemistosta ja kopioi se githubiin. Github - asetukset - ssh key - add new key.
      
       $ cat id_rsa.pub
5. Kopioi Githubista kurssin reposition ssh linkki
![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/468a6534-4ff2-4fb1-85aa-49e0b535e465)

       $ git clone git@github.com:Lambizzzz/infra-as-code.git
Nyt github on linkitetty päätteeseen. Saa muokattua jo tehtyjä tiedostoja ja luoda uusia.

### Tärkeitä komentoja 

git add . && git commit; git pull && git push
