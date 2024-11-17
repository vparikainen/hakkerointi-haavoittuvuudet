# h4 - Kääntöpaikka
## x) Lue/katso/kuuntele ja tiivistä
- Hammond 2022: Ghidra for Reverse Engineering (PicoCTF 2022 #42 'bbbloat')
  - ltrace ja strace ovat käteviä työkaluja kirjastojen ja järjestelmäkutsujen jäljittämiseen, objdump toimii ohjelman purkamiseen.
  - Ghidra on työkalu käänteismallinnukseen. Sitä käytetään luomalla uusi projekti johon avataan tiedosto jota halutaan analysoida.
  - Ghidran avulla on helppo löytää binääri- tai assemblykoodista mm. funktioita tai eri muuttujia, ja oppia ymmärtämään, miten ohjelma toimii.
  - Pythonilla voi vaivattomasti muuttaa heksadesimaaleja desimaaleiksi.

 ---
|       |   Ympäristö                |
|--------- | ------------------------------- |
| **OS** | Debian 12.7.0  |
| **Browser** | Firefox 128.3.1esr |
| **Hardware** | innotek Gmhb VirtualBox |
| **Network** | Intel PRO/1000 MT Desktop (NAT) |

## a) Asenna Ghidra.

Asennus onnistui.

## b) rever-C. Käänteismallinna packd-binääri C-kielelle Ghidralla. Etsi pääohjelma. Anna muuttujielle kuvaavat nimet. Selitä ohjelman toiminta. Ratkaise tehtävä binääristä, ilman alkuperäistä lähdekoodia. ezbin-challenges.zip

Koitin ratkaista tehtävää hyvin pitkälti alustavan tehtävän videota mukaillen. Avasin Ghidran ja loin siellä uuden projektin, jossa avasin packd-tiedoston CodeBrowserilla ja analysoin sen. Avasin Defined Strings-ikkunan ja lähdin etsimään main-funktiota, jonka löysin suht nopeasti. 

![codebrowser näkymä](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h4-packd1.png)

Tutkailin koodia jonkin aikaa, ja nimesin muuttujat ja funktiot mielestäni järkevällä tavalla. Miten ymmärsin ohjelman toimivan oli seuraavanlainen: Alussa luodaan kaksi muuttujaa, salasanaa kuvaava kokonaisluku sekä käyttäjän syöte salasanalle. Ohjelma sitten heittää salasanan kokonaisluvun jonkinlaiseen funktioon, jossa oletettavasti siitä muodostuu salasanan merkkijono. Sitten ohjelma heittää käyttäjän syötteen johonkin funktioon. Sen jälkeen salasana-muuttuja muutetaan funktion kautta arvoksi, joka määrittää millainen viesti käyttäjälle näytetään ('Sorry, no bonus.' tai 'Correct' yms.).

![muokattu main-funktio](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h4-packd4.png)

Koittaessani avata funktioita, niiden sisällöstä ei saanut paljoa irti, joten sen suhteen arvaukseni ohjelman toiminnasta jäävät pitkälti juuri niiksi, arvauksiksi. 

![funktioiden sisältö](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h4-packd3.png)

Jäin vähän umpikujaan tehtävän kanssa, sillä tiesin, että salasanan voisi ratkaista salasana-muuttujan numeron avulla muuttamalla se merkkijonoksi funktiolla, jonka toiminnasta en kuitenkaan saanut kiinni.

## c) Jos väärinpäin. Muokkaa passtr-ohjelman binääriä (ilman alkuperäistä lähdekoodia) niin, että se hyväksyy kaikki salasanat paitsi oikean. Osoita testein, että ohjelma toimii.

Avasin passtr-tiedoston edellisen tehtävän tavoin Ghidrassa. Tiesin, että tehtävän suoritus onnistuu, kunhan saisin muokattua ``if (iVar1 == 0)`` -kohtaa siten, että muuttaisin **==** muotoon **!=**. Klikkasin muokattavaksi haluamaani kohtaa decompilerissa, jotta se korostuisi listingissä. Siellä sain muokattua patch instructionin avulla binääriä, mutta ongelmaksi osoittautui, kun en tiennyt, mitä minun pitäisi muokkauseen laittaa jotta ohjelma toimisi haluamallani tavalla.

![funktioiden sisältö](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h4-passtr1.png)

Googlailtuani ([Quora](#viitteet)) sain selville, että JZN tarkoittaa binäärissä _jump if not zero_ eli jos ehtolause ei anna arvoksi True, sen yli hypätään. Muokkasin sen JZ:ksi, joka on päinvastainen _jump if zero_.

Ongelmaksi osoittautui, kun en saanut muokkaamaani binääriä auki. En tiedä johtuiko se siitä, etten uskaltanut päällekirjoittaa alkuperäistä passtr-tiedostoa, vai jostakin ghidran pään vaiheesta jota en hoksannut, mutta yrittäessäni avata tiedostoa, se valitti "permission denied". 

![funktioiden sisältö](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h4-passtr2.png)

## d) Nora CrackMe: Käännä binääreiksi Tindall 2023: NoraCodes / crackmes. Lue README.md: älä katso lähdekoodeja, ellet tarvitse niitä apupyöriksi. Näissä tehtävissä binäärejä käänteismallinnetaan. Binäärejä ei muokata, koska muutenhan jokaisen tehtävän ratkaisu olisi vaihtaa palautusarvoksi "return 0".

Kloonasin repositorion README.md:ssä olleen tutoriaalin mukaan. Sain luotua crackme01 ongelmitta.

![crackme01 luonti](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h4-crackme1.png)

## e) Nora crackme01. Ratkaise binääri.

Ensimmäinen crackme ilmoitti suorittaessaan näin: **Need exactly one argument.**. Avasin tiedoston ghidralla ja oikea arvo löytyi oikeastaan ihan vahingossa kun avasin defined strings -ikkunan ja listan pohjalla oli epäilyttävä **password1**.

![crackme01 strings](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h4-crackme2.png)

Kokeilin sitten tätä suoraan ja sehän oli oikea ratkaisu.

![crackme01 strings](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h4-crackme3.png)

## e) Nora crackme01e. Ratkaise binääri.

Tämäkin crackme pyysi yhtä arvoa. Avasin tiedoston Ghidralla ja tälläkin kertaa defined strings näytti oikean vastauksen.

Mutkiakin oli tosin matkassa, sillä tällä kertaa merkkijonon eteen piti laittaa hipsut, ettei komentokehote yritä suorittaa olematonta !paas.k -kehotetta. Hipsujen kanssa ratkaisu kuitenkin tuli esille.

![crackme01 strings](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h4-crackme5.png)

## f) Nora crackme02. Nimeä pääohjelman muuttujat käänteismallinnetusta binääristä ja selitä ohjelman toiminta. Ratkaise binääri.

Edellisten crackme-tehtävien tavoin tämäkin pyysi yhtä arvoa. Avasin tiedoston Ghidralla decompilerissa.  Jos ensimmäinen parametri == 2, suoritetaan arvon tarkistus, jolloin kaksi alkuperäisistä muuttujista määritellään arvoilla 'p' ja 0.

![crackme01 strings](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h4-crackme6.png)

Tuijotin koodia aika pitkään, kunnes lopulta päädyin tällaiseen lopputulemaan sen toiminnasta:
1. Ohjelman main-funktiosta näkee, että se saa arvona kaksi parametriä, ja funktion alussa määritellään neljä muuttujaa (cVar1, cVar2, uVar3 ja lVar4). Jos funktion ensimmäinen parametri on arvoltaan kaksi, mennään 'salasanan' tarkistuslooppiin. 
2. Tarkistusloopissa cVar määritellään 'p':ksi ja lVar4 0:ksi. Sen jälkeen cVar1 määritellään toisen parametrin mukaan seuraavasti: ``cVar1 = *char *)*( long *)(param_2 + 8) + lVar4);``.
3. Jos ``cVar1 =='\0'``, loopin suoritus katkeaa. Jos ``cVar2 + -1 != (int)cVar1``, 'salasana' on väärä.
4. cVar2 määritellään "password1"[lVar4 +1], jonka jälkeen lVar4:sta tulee 1.
5. Jos ``cVar != '\0'``, salasana on oikea. uVar3:sta tulee nolla.

Päädyin nimeämään muuttujat seuraavanlaisesti:

![crackme01 strings](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h4-crackme7.png)

Tässä kohtaa en oikein osannut tulkita, miten oikea 'salasana' muodostuu. Katsoin apua Nora Crackme:n [ohjeesta](#viitteet), ja tajusin, että ohjelma muuttaa merkkijonoa 'password1' loopissa siten, että joka kierroksella yksi indeksin osa vähenee yhdellä, eli periaatteessa p:stä tulee o jne. Näin ollen ASCII:n mukaan oikea salasana on **o`rrvnqc0**

![crackme01 strings](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h4-crackme8.png)

### Viitteet

Hammond 2022: [Ghidra for Reverse Engineering (PicoCTF 2022 #42 'bbbloat'](https://www.youtube.com/watch?v=oTD_ki86c9I&ab_channel=JohnHammond)

[Quora](https://www.quora.com/What-is-the-difference-between-the-JZ-and-JNZ-instructions-in-assembly-language)

Nora CrackMe: [Käännä binääreiksi Tindall 2023: NoraCodes / crackmes](https://github.com/NoraCodes/crackmes)
