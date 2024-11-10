# h3 - No strings attached
|       |   Ympäristö                |
|--------- | ------------------------------- |
| **OS** | Debian 12.7.0  |
| **Browser** | Firefox 128.3.1esr |
| **Hardware** | innotek Gmhb VirtualBox |
| **Network** | Intel PRO/1000 MT Desktop (NAT) |
## a) Strings. Lataa ezbin-challenges.zip Aja 'passtr'. Selvitä oikea salasana 'strings' avulla. Selvitä myös lippu. (Ensisijaisesti katsomatta sorsia, jos osaat.)

Asennettuani ja purettuani ezbin-challenges-zipin siirryin kansioon ja koitin ajaa passtr-tiedoston. Se kysyi heti salasanaa, jota en tietenkään tiennyt.

![passtr1](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h3-passtr1.png)

Ajoin stringsin ja eteen ryöpsähti lista sitä sun tätä, ja oikea salasana ja lippu löytyi tästä listasta.

![passtr1](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h3-passtr2.png)

Kokeilin vielä salasanaa varmistukseksi, ja se toimi.

![passtr1](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h3-passtr3.png)

## b) Tee passtr.c -ohjelmasta uusi versio, jossa salasana ei näy suoraan sellaisenaan binääristä. Osoita testillä, että salasana ei näy. (Obfuskointi riittää.)

Ohjelman korjaus lähti käyntiin avaamalla passtr.c -tiedosto editorissa. Koodista näki suoraan, että ongelma oli siinä, että ehtolauseessa salasanaa verrattiin suoraan merkkijonoversioon salasanasta. 

![passtr1](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h3-passtr4.png)

Googlettelin hieman vaihtoehtoja obfuskoinnille, ja päädyin ottamaan mallia [Yuri Slobodyanyukin blogista](#viitteet). Loin tarkistukselle oman piilotetun merkkijonon, jonka avasin tarkistusta ennen ja suljin sen jälkeen.

![passtr1](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h3-passtr5.png)

Tallennettuani editoidun version koodista ihmettelin hetken, miksi muutokset eivät näkyneet, kun ajoin ``strings passtr`` uudelleen. Hetken googlailtuani tajusin, että c-koodi piti vielä kääntää jotta sen voi suorittaa. Tämä hoitui komennolla ``gcc passtr.c -o passtr``. Nyt ajaessani strings-komennon, salasana ei enää näkynyt suoraan.

![passtr1](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h3-passtr6.png)

## c) Packd. Aja 'packd' paketista ezbin-challenges.zip. Mikä on salasana? Mikä on lippu? (Tämä tehtävä on hieman haastavampi. Kirjaa ylös kokeilemasi lähestymistavat ja keksimäsi hypoteesit. Toivottavasti pääset itse maaliin, mutta jos et, läpikävely paljastuu tunnilla...)

### Viitteet

yurisk.info - [Binary obfuscation - String obfuscating in C](https://yurisk.info/2017/06/25/binary-obfuscation-string-obfuscating-in-C/)
