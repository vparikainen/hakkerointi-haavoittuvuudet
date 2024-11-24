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



### Viitteet

Low Level: [GDB is REALLY easy! Find Bugs in Your Code with Only A Few Commands](https://www.youtube.com/watch?v=Dq8l1_-QgAc&ab_channel=LowLevel)

Nora CrackMe: [NoraCodes/crackmes](https://github.com/NoraCodes/crackmes)
