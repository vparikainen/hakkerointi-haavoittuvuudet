# h7 - Uhagre2
## x) Lue/katso/kuuntele ja tiivistä.

- **€ Schneier 2015: Applied Cryptography, 20ed: Chapter 1: Foundations:**
  1.1 Terminology ("Historical Terms" loppuun)

  - Koodi viittaa historiallisesti kryptojärjestelmään, joka toimii kielellisten yksiköiden kautta (sanat, fraasit, lauseet jne).
  - Salakirjoitus (_ciphertext_) on kryptattu viesti, jonka kääntäminen selkeälle kielelle on salauksen purkua (_decryption_).
  - Koodit ovat hyödyllisiä vain tietyissä tarkoituksissa; salakirjoitus on hyödyllistä missä tilanteessa tahansa.
  
  1.4 Simple XOR

  - Yksinkertainen "salakirjoitus" joka toimii ehtona; joko _x_ tai _y_
  - Vain toinen ehdoista voi olla tosi jotta XOR palauttaa arvon _True_.
  - Esimerkiksi ```1 XOR 1 = False.```
  - Helppo murtaa

  1.7 Large Numbers
 
  - Suuria numeroita kuvataan potenssilukuina
  - Esimerkiksi: Todennäköisyys kuolla salamaniskuun (per päivä) on **yksi miljardista**. Tämä luku voidaan esittää potenssilukuna seuraavasti: **2^33**
- **Karvinen 2024: Python Basics for Hackers**

  - Erilaisia vinkkejä miten hakkeroida pythonilla.
  - _REPL: Read-Eval-Print_: pythonissa 'python3', 'ipython3'.
  - _F5 compile_: näyttää ohjelman tuloksen suoraan painamalla 'F5'-näppäintä
  - Python on erinomainen laskin

 ---
|       |   Ympäristö                |
|--------- | ------------------------------- |
| **OS** | Debian 12.7.0  |
| **Browser** | Firefox 128.3.1esr |
| **Hardware** | innotek Gmhb VirtualBox |
| **Network** | Intel PRO/1000 MT Desktop (NAT) |

## Ratkaise CryptoPals Set 1 -haasteet. Tehtävät saa ratkaista millä vain ohjelmointikielellä ja käyttää mitä tahansa tekstieditoria tai IDE:ä.
### a) 1. Convert hex to base64.

Aloitin avaamalla ensimmäisen haasteen auki ja tutkailemalla sitä. Tehtävä on selkeä; muuta heksadesimaali base64:ksi. Päätin ratkaista tehtävän pythonilla, koska sillä on tullut koodattua jonkin verran ja ajattelin, että Karvisen [vinkeistä](#viitteet) voisi olla hyötyä.

![cryptopals challenge 1](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h7-crypto1.png)

Toin ensiksi base64:n koodiin ja tallensin sen jälkeen käyttäjän heksadesimaali-syötteen omaan muuttujaan. Sen jälkeen muunsin heksadesimaalin biteiksi, ja edelleen bitit base64:ksi.

![vscode ratkaisukoodi](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h7-crypto2.png)
 
### b) 2. Fixed XOR.

Seuraava haaste pyysi kirjoittamaan funktion, joka ottaa kaksi samanpituista heksadesimaali merkkijonoa ja tuottaa niiden XOR-yhdistelmän.

![cryptopals challenge 2](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h7-crypto3.png)

Loin funktion _xorifier_ joka ottaa kaksi heksadesimaaliarvoa ja tarkistaa, ovatko ne yhtä pitkät. Jos heksat ovat samanpituiset, funktio muuntaa ne biteiksi ja tuottaa niiden XOR-yhdistelmän, joka palautetaan vielä heksadesimaaliksi ennen tulostusta.

![vscode ratkaisukoodi 2](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h7-crypto4.png)

### c) 3. Single-byte XOR cipher.

Seuraava haaste pyysi löytämään avaimen heksadesimaali merkkijonosta, joka on XOR'd, ja purkamaan viestin.

![cryptopals challenge 3](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h7-crypto5.png)

Mehut loppuivat ratkaista tämä tehtävä joten jätin sen ja seuraavan kesken.

### d) 4. Detect single-character XOR.

### Viitteet

Schneier 2015: Applied Cryptography, 20ed: [Chapter 1: Foundations](https://www.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/08_chap01.html#chap01-sec001)

Karvinen 2024: [Python Basics for Hackers](https://terokarvinen.com/python-for-hackers/)
