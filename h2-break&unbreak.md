# H2 - Break & Unbreak
x) Lue/katso/kuuntele ja tiivistä. 
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
