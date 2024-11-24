# H5 - Se elää!
|       |   Ympäristö                |
|--------- | ------------------------------- |
| **OS** | Debian 12.7.0  |
| **Browser** | Firefox 128.3.1esr |
| **Hardware** | innotek Gmhb VirtualBox |
| **Network** | Intel PRO/1000 MT Desktop (NAT) |
## a) Lab1. Tutkiminen mikä on ohjelmassa vialla ja miten se korjataan.

Käytin tehtävän ratkaisemisen tukena Low Leveling [youtubevideota](#viitteet). Aloitin kääntämällä koodin gnu debuggerilla ajettavaan muotoon ja avaamalla gdb:n.

![gdb aloitus](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h5-lab1.png)

Lisäsin heti alkuun breakpointin main-funktioon ja lähdin ajamaan ohjelmaa kohta kohdalta, kunnes törmäsin virheilmoitukseen.

![muokattu main-funktio](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h5-lab1.2.png)

Ohjelmassa näyttäisi olevan sellainen vika, että jos tulostettava viesti on NULL-muotoa, ohjelma kaatuu. Tämä voitaisiin ratkaista käärimällä _print_scrambled_-funktion _do while_-koodi tarkistukseen, tyyliä ``if message != NULL``. Näin ohjelma ei kaatuisi, vaikka siihen syöttäisikin NULL-arvon.  

## b) Lab2. Selvitä salasana ja lippu + kirjoita raportti siitä miten aukesi.

Avasin Lab2-kansiosta passtr-kansion ja käänsin passtr.c-tiedoston gnu debuggerille edellisen tehtävän tavoin. Kun avasin gnu:n, salasana ja lippu olivat näkyvillä koodissa ja aloin pohtia, olenko nyt avannut jonkun väärän tiedoston kun ne löytyivät näin helposti. Suoritin koodin ja salasana oli _sala-hakkeri-321_ ja lippu _FLAG{Tero-d75ee66af0a68663f15539ec0f46e3b1}_.

![gdb passtr.c](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h5-lab2.png)

## c) Lab3. Kokeile Nora Crackmes harjoituksia tehtävä 3 ja 4 ja loput vapaaehtoisia. 

### Crackme03

Aloitin tehtävän muodostamalla ja avaamalla crackme03.64-tiedoston, joka pyysi jälleen yhtä argumenttia.

![crackme03](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h5-crackme1.png)

Sen jälkeen menin kääntämään alkuperäisen crackme03.c-tiedoston gnu debuggeriin edellisten tehtävien tavoin ja avasin gdb:n. Koodi aukesi eteeni ja selattuani sitä löysin oikean salasanan kommenttina.

![crackme03](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h5-crackme2.png)

Kokeilin salasanaa, ja se toimi.

![crackme03](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h5-crackme3.png)

### Crackme04

Muodostin ja avasin crackme04.64-tiedoston, joka pyysi yhtä argumenttia. Käänsin ja avasin alkuperäisen crackme04.c-tiedoston gnu debuggerilla. Koodin kommentista paljastui, että ohjelma hyväksyy kaikki salasanat, joiden pituus on 16 ja jonka merkit ovat ASCII-muodossa ja ovat summana 1652.

![crackme03](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h5-crackme4.png)



### Viitteet

Low Level: [GDB is REALLY easy! Find Bugs in Your Code with Only A Few Commands](https://www.youtube.com/watch?v=Dq8l1_-QgAc&ab_channel=LowLevel)

Nora CrackMe: [NoraCodes/crackmes](https://github.com/NoraCodes/crackmes)
