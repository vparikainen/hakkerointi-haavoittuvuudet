# H5 - Se elää!
|       |   Ympäristö                |
|--------- | ------------------------------- |
| **OS** | Debian 12.7.0  |
| **Browser** | Firefox 128.3.1esr |
| **Hardware** | innotek Gmhb VirtualBox |
| **Network** | Intel PRO/1000 MT Desktop (NAT) |
## a) Lab1. Tutkiminen mikä on ohjelmassa vialla ja miten se korjataan.

Aloitin tehtävän ratkaisemisen kääntämällä koodin gnu debuggerilla ajettavaan muotoon ja avaamalla gdb:n.

![gdb aloitus](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h5-lab1.png)

Lisäsin heti alkuun breakpointin main-funktioon ja lähdin ajamaan ohjelmaa kohta kohdalta, kunnes törmäsin virheilmoitukseen.

![muokattu main-funktio](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h5-lab1.2.png)

Ohjelmassa näyttäisi olevan sellainen vika, että jos tulostettava viesti on NULL-muotoa, ohjelma kaatuu. Tämä voitaisiin ratkaista käärimällä _print_scrambled_-funktion _do while_-koodi tarkistukseen, tyyliä ``if message != NULL``. Näin ohjelma ei kaatuisi, vaikka siihen syöttäisikin NULL-arvon.  

## b) Lab2. Selvitä salasana ja lippu + kirjoita raportti siitä miten aukesi.

## c) Lab3. Kokeile Nora Crackmes harjoituksia tehtävä 3 ja 4 ja loput vapaaehtoisia. 

### Viitteet

Nora CrackMe: [NoraCodes/crackmes](https://github.com/NoraCodes/crackmes)
