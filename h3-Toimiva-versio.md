# Kolmas harjoitus, Toimiva versio
## x) lue ja tiivistä
### What is Git? ([Chacon and Straub 2014](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F))

### 'git add . && git commit; git pull && git push'

### Varaston loki

## a) Online
Loin uuden varaston GitHubiin. Lisäsin varastoon README.md ja GNU General Public License 3 -tiedostot.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/4b871267-46a4-438d-a01b-238a9123a4dd)



> Kuva 1. Uuden varaston luomisnäkymä.

## b) Dolly
Kloonaa juuri tehty varasto itsellesi, tee muutoksia ja puske palvelimelle, jotta ne näkyvät webbipalvelimessa. Varaston kloonauksen tarvittava url on kopioitavana varaston webbipalvelimelta.

1. Kopioi varaston ssh-url
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/43a924f6-5c52-43bd-8691-2a93e9d47934)

> Kuva 2. 
2. Kloonasin varaston. Terminaalissa kloonaus suoritetaan alla olevalla komennolla, jonka perään laitetaan varaston yksilöllinen ssh-url.

    $ git clone <ssh-url>
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/66f6162d-8d89-4cb9-8ac3-310f16c65c68)

> Kuva 3. Varaston kloonaus onnistui
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/3517196f-0268-41e1-adf7-ae1a40394401)

> Kuva 4. Varastossa ei vielä ole muita tiedostoja kuin README.md ja lisenssi.
3. Loin varastoon uuden tekstitiedoston. Lisäsin siihen markdownin.

    $ micro Mee-töihin.md
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/d1eca7cc-f2c1-4758-b5f0-262be6f75b57)

> Kuva 5. Microlla tehty tekstitiedosto, johon lisäsin sisältöä
Jotta muutokset tulevat näkyviin webbipalvelimeen, on käytettävä komentoa, joka kertoo gitille tallennettavista muutoksista.

4. Selitin tehdyt muutokset engalnniksi käskymuodossa.

    $ git add . && git commit; git pull && git push
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/6781f1e6-e663-40b0-948c-505d8a322525)

> Kuva 6. Lisäsin tekstin "Add new file" ja tallensin tiedoston.
Nyt muutokset ovat valmiit ja ne pitäisivät olla näkyvissä webbipalvelimessa.

5. Tarkistin, että uusi luotu tiedosto ja siihen tehdyt muutokset näkyvät webbipalvelimessa.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/b08998bc-b1b7-46f6-87c0-2ec22185e2bc)
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/3ed0eb9a-d8ba-4bd4-b6c3-72765828c6da)

> Kuvat 7 & 8. Muutokset onnistuivat.

## Doh!
Tein turhan muutokset gittiin ja en tallentanut niitä. Tuhosin muutokset  ‘git reset --hard’ -komennolla.
1. Loin uuden tiedoston.
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/8f7ffa99-802c-460c-b066-9bc6a7ba45ec)

> Kuva 9. Uusi luotu tiedosto.
2. Ideksoin uuden tiedoston ja tarkistin nykyisen työskentelytilan vaiheen.

    $ git add opiskele.md
    $ git status
    
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/4562a082-819b-43dd-bc58-3e7b58f40d33)

> Kuva 10. Tiedosto lisätty.
3. Tuhosin muutokset ja tarkistin, että muutokset oli tuhoutuneet.

    $ git reset --hard
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/362715f6-a868-4e41-b380-b3a4a4ee4bc4)

> Kuva 11. Turhat muutokset ovat tuhottu.

Edellä tehdyt turhat muutokset saatiin helpolla tavalla tuhottua, mutta tuhottuja muutoksia ei saa enään peruutettua.

## Tukki
Tarkastelin varastoni lokia. Lokeista voin nähdä tehnyt muutokset, niiden ajankohdat, tekijät ja commmit -viestin.

### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/14c9f3cd-cada-4482-ba14-0c1811ee284f)

> Kuva 12. Lokissa näkyy kaksi muutosta.

Lokin mukaan varastoon on tehty vain kaksi muutosta, varaston luominen ja tiedoston lisääminen. Tiedosto, jonka loin ja tuhosin ei näy lokissa ollenkaan. 
### ![image](https://github.com/Lambizzzz/infra-as-code/assets/148875838/21929631-903d-4eb8-9f61-969920db11b8)

> Kuva 13. Tiedostoon tehnyt muutokset näkyvät myös webbipalvelimessa.

Olen aikaisemmin lisännyt nimeni ja sähköpostin gittiin käyttämällä alla olevia komentoja. Ne näkyvät lokissa.

    $ git config --global user.email "<sähköposti>"
    $ git config --global user.name "<nimi>"

## Suolattu rakki

