<img width="541" alt="image" src="https://github.com/user-attachments/assets/213b7767-54b8-4618-873d-06769afa78e5"># H2 - Break & Unbreak
## x) Lue/katso/kuuntele ja tiivistä. 
- OWASP: OWASP Top 10: A01 Broken Access Control
  - Pääsynvalvonta rakoilee siten, että dataa voi päästä lukemaan, muokkaamaan ja poistamaan sellainen käyttäjä, jolla ei pitäisi olla siihen oikeuksia. Tämä voi tapahtua esim. URL:ia muokkaamalla.
  - Ongelmaa voi ehkäistä mm. estämällä oletuksena käyttäjän pääsy muihin kuin julkiseen dataan sekä varmistamalla, ettei verkkosivujen juuressa ole tiedostojen metadataa tai varmuuskopiotiedostoja.
- Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf
  - Fuff on verkkotyökalu, jonka avulla voi löytää mm. piilotettuja hakemistoja sekä POST parametrejä.
  - Työkalu toimii siten, että se kokeilee verkkosivulle sanakirjasta yleisiä verkkopolkuja ja listaa vastaukset. Listalta voi sitten filtteröidä vastauksia yhteisten piirteiden perusteella, ja siten mahdollisesti löytää piilotettuja hakemistoja.
- PortSwigger: Access control vulnerabilities and privilege escalation
  - Pääsynvalvontaa on mm.
      - *vertical access controls* (Eri käyttäjillä on pääsy erilaisiin sovelluksen toiminnallisuuksiin)
      - *horizontal access controls* (Rajoitetaan pääsy eri resursseihin tietyille käyttäjille)
      - *context-dependent access controls* (Pääsy toiminnallisuuksiin ja resursseihin perustuu sovelluksen tilaan tai käyttäjän vuorovaikutuseen sen kanssa; käyttäjää estetään tekemästä asioita ns. väärässä järjestyksessä)
  - Haavoittuvuus voi syntyä esim. jos
      - käyttäjä pääsee käsiksi toimintoon, johon hänellä ei pitäisi olla oikeuksia (esim. ei-admin käyttäjä pääsisi poistamaan muita käyttäjiä)
      - admin-oikeudet on linkattu adminin kotisivulle muttei muiden käyttäjien sivuille, mutta niihin pääsee käsiksi oikean URL:in avulla
      - käyttäjän pääsyoikeudet määritellään sisäänkirjautumisen yhteydessä ja tallennetaan esim. välimuistiin
- Karvinen 2006: Raportin kirjoittaminen
  - Raportointi tehdään samaan aikaan tehtävän kanssa, kertomalla tarkkaan mitä tehtiin ja mitä tapahtui.
  - Raportoinnin on oltava toistettavaa, täsmällistä, helppolukuista ja lähteisiin on viitattava.

---
|       |   Ympäristö                |
|--------- | ------------------------------- |
| **OS** | Debian 12.7.0  |
| **Browser** | Firefox 128.3.1esr |
| **Hardware** | innotek Gmhb VirtualBox |
| **Network** | Intel PRO/1000 MT Desktop (NAT) |

## a) Murtaudu 010-staff-only

Saatuani asennettua vaatimukset ja ladattua ja purettua tehtäväpaketin sekä avattua oikean tehtävän, kokeilin tunnillakin mainittua element pickeriä ja klikkasin PIN koodin kirjoituskenttää ja poistin kohdan, jossa syötteelle asetettiin tyypiksi numero.

![input type poisto](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h2-staff-only1.png)

Sen jälkeen kokeilin kirjoittaa syötekenttään erilaisia SQL-lauseita (tyyliä SELECT password FROM pins WHERE pin='' OR 1=1--) mutta onnistuin saamaan vain Internal Server Error 500. Jäin vähän jumiin enkä tiennyt miten edetä, joten menin etsimään apua PortSwiggerin SQL Injection sivuilta. Löysin sieltä seuraavanlaisen koodinpätkän: 
``` ' UNION SELECT username, password FROM users--```
jota sovelsin sivulle.

![union select](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h2-staff-only3.png)

## b) Korjaa 010-staff-only haavoittuvuus lähdekoodista. Osoita testillä, että ratkaisusi toimii.

Koodin korjaaminen lähti käyntiin avaamalla lähdekoodi esille (challenges-kansiosta tiedosto staff-only.py) ja tutkimalla sitä. SQL-kysely on toteutettu koodissa siten, että käyttäjän syöte tallennetaan muuttujaksi, joka annetaan suoraan GET-metodille. Tämä altistaa haavoittuvuudelle, jossa käyttäjä kirjoittaa SQL-koodia syötekenttään.

![lähdekoodi](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h2-staff-only4.png)

Koitin korjata koodia ensin lisäämällä kysymysmerkin sql-kysely kohtaan 
```"SELECT password FROM pins WHERE pin='"+pin+"';"```
ennen pin-koodia toimimaan placeholderina pinille, mutta se ei toiminut. Googlailin ratkaisua, mutta lopulta päädyin katsomaan mallia hack'n fix -sivulta ja muokkasin koodia seuraavanlaisesti:

![korjaus](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h2-staff-only5.png)

Tämän jälkeen kun testasin syöttää UNION SELECT:iä sivulle, sivu vain päivittyi joten korjaus oli onnistunut.

## c) Ratkaise dirfuzt-1 artikkelista Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf. Tämä auttaa 020-your-eyes-only ratkaisemisessa.

Aloitin ratkaisemaan tehtävää dirfuzt-0 ohjeen mukaisesti. Luulin saaneeni ffufin ladattua ja lukemaan hakemiston sanakirjan verkkopolkujen avulla, mutta kun vertasin vastaustani esimerkkiin, en nähnyt itselläni esimerkiksi kokoa missään, ja ffuf vastauksessani oli paljon virheitä.

![ffuf](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/ffuf-1.png)

Kokeilin silti filtteröidä hack'n fix-sivun mallin mukaisesti, ja sain hakemistot näkyviin. En olisi osannut löytää oikeaa filtteröintiä omasta versiostani.

![ffuf2](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/ffuf-2.png)

![flag1](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/ffuf-3.png)

![flag2](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/ffuf-4.png)

## d) Murtaudu 020-your-eyes-only. Ks. Karvinen 2024: Hack'n Fix

Saatuani testi serverin pyörimään ja sivun auki, tehtävänäni oli löytää tieni administrative consoleen. Etusivulla oli näkyvillä kaksi painiketta ('Show my personal data' sekä 'Admin dashboard') joita molempia klikkaamalla päätyi kirjautumissivulle. Etusivun oikeassa yläkulmassa oli myös tie kirjautumis- ja rekisteröitymissivuille.

![h2-your-eyes-only-frontpage](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h2-your-eyes-only2.png)

Koska edellisen tehtävän tuli auttaa tämän ratkaisemisessa, fuzzasin sivun heti alkuun edellistä tehtävää mukaillen. Sieltä löytyi heti polku 'admin-console', mutta edessä oli yhä kirjautumisongelma, sillä vaikka tiesinkin osoitteen mihin mennä, en päässyt sinne ilman, että eteen lävähti kirjautumissivu.

![fuzzaus](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h2-your-eyes-only3.png)

Kokeilin rekisteröityä sivulle luomalla tunnuksen 'user' salasanalla 'testi123'. Sain auki henkilökohtaisen datan sivun. Klikkaamalla admin dashboardia eteen tuli '403 Forbidden' -sivu. Kokeilin laittaa 'admin-console'-endpointin kun olin kirjautunut sisään, ja pääsin kielletylle sivulle.

![ratkaisu](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h2-your-eyes-only4.png)

### Viitteet
Portswigger: [SQL injection](https://portswigger.net/web-security/sql-injection)

Karvinen 2024: [Hack'n Fix](https://terokarvinen.com/hack-n-fix/)
