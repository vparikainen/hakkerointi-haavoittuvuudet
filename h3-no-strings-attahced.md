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
h
## c) Packd. Aja 'packd' paketista ezbin-challenges.zip. Mikä on salasana? Mikä on lippu? (Tämä tehtävä on hieman haastavampi. Kirjaa ylös kokeilemasi lähestymistavat ja keksimäsi hypoteesit. Toivottavasti pääset itse maaliin, mutta jos et, läpikävely paljastuu tunnilla...)
