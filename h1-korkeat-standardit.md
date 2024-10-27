# h1 - Korkeat Standardit

a) Tutustu kurssin sanastoon, joka on määritelty SFS-EN ISO/IEC 27000:2020:en standardissa, kappaleessa 3. Terms and Definitions. Selvitä seuraavien kappaleiden määritteet ja selitä omin sanoin mitä ne tarkoittavat: 3.2, 3.31, 3.56, 3.58, 3.77.
- **3.2:** _hyökkäys (attack)_. Pyrkimys vahingoittaa luvattomasti jotakin tietojärjestelmää tai sen ominaisuutta.
- **3.31:** _tietoturvapoikkeama (information security incident)_. Yksittäinen tai useampi, odottamaton tai ei-toivottu tapahtuma, jolla on suuri todennäköisyys heikentää elinkeinotoimintaa sekä vaarantaa tietoturvaa.
- **3.56:** _vaatimus (requirement)_. Tarve tai odotus, joka on yleisesti oletettu tai vaadittu.
- **3.58:** _arviointi (review)_. Toiminta, jolla määritellään arvioitavan kohteen soveltuvuutta ja tehokkuutta saavuttaa tavoitteet.
- **3.77:** _haavoittuvuus (vulnerability)_. Heikkous ohjelmistossa, joka altistaa vahingoille.

b) Tutustu standardiin ISO 27034-1 - 5. Selvitä mistä standardi kokonaisuudesta on kyse.
- Kyseessä on sovelluksen tietoturvaan liittyvä standardi, jonka tarkoituksena on avustaa kaikenkokoisia ja -tyyppisiä yrityksiä käyttöjärjestelmien turvallisuuteen vaikuttavien tekijöiden (datan, teknologioiden, sovelluskehityksen elinkaaren yms) turvaamisessa. Standardi toimii ISO/IEC 27000 standardin alla.

c) Kuuntele podcast: Meurman 2021: Laatulöpinät 30: Tietoturvallisuus ohjelmistokehityksessä (jakson mp3, Laatolöpinät RSS-syöte). Mitä mieltä olet podcastin väittämistä?
1. Mikään ohjelmisto ei ole täysin tietoturvallinen.
   - Samaa mieltä. Kuten podcastin vierailija Joona Kokkola sanoi, absoluuttista tietoturvaa ei ole olemassa. Ohjelmistoja tekee ja käyttää ihmiset, joten inhimillisiä virheitä on aina mahdollista tapahtua. Lisäksi 
2. Hallinnollinen tietoturva on teknisen tietoturvan onnistumisen edellytys.
   - Samaa mieltä. Ei yhtä ilman toista; tekninen tietoturva toimii parhaiten silloin, kun sitä rakennetaan hallinnollisen tietoturvan tunnistamien riskien kautta.
3. Automaatiotestaus on ohjelmiston tietoturvan kannalta erittäin tärkeää.
   - Samaa mieltä. Testauksen automatisointi helpottaa ja nopeuttaa ongelmien havaitsemista ja korjaamista. Vaikka automatisointi lisää resursseja eikä välttämättä ole sopiva jokaisen komponentin kohdalla, sille on paikkansa, kunhan se ei ole ainoanlaatuista testausta, jota ohjelmistolle tehdään.
4. Ohjelmistoa suunniteltaessa voidaan tehdä paljonkin auttamaan käyttäjää toimimaan tietoturvallisesti. Usein nämä toimenpiteet kuitenkin vaikuttavat negatiivisesti käytettävyyteen.
   - Samaa mieltä. Esimerkiksi kaksivaiheinen tunnistus lisää tietoturvaa huomattavasti, mutta usein lisää käyttäjälle tehtävää ja voi siten olla turhauttavaa. Mitä enemmän toimenpiteitä tietoturvan lisäämiseksi vaaditaan, sitä ärsyttävämpää ohjelmiston käyttäminen voi käyttäjän puolesta olla.
5. Ohjelmiston tietoturvallisuuden suunnitteluun vaikuttaa paljolti se, kuinka arkaluonteisia tietoja ohjelmistolla on tarkoitus käsitellä.
   - Samaa mieltä. Jos ohjelmistolla käsitellään henkilötietoja, niiden tietoturvan suojaamiseen on määrätty lakeja, joten silloin suunnitteluvaiheessa tietoturva on eri tavalla läsnä kuin jos ohjelmistolla käsitellään vaikkapa säätietoja. Tästä huolimatta tietoturva on aina tärkeää ottaa huomioon suunnitteluvaiheessa.
6. Ohjelmistokehittäjät näkevät omat ohjelmistonsa aina merkittävästi riskialttiimpina, kuin muiden tekemät ohjelmistot.
    - Samaa mieltä. Oman ohjelmiston kokonaisuus on helpompi hahmottaa, ja siten tietoturvariskit ovat selvemmin esillä kuin muiden ohjelmistoja tarkastellessa.

d) Asenna Debian 12-Bookworm virtuaalikoneeseen. Päivitä kaikki ohjelmat.
- Asennus onnistui.

## Viitteet
Meurman 2021: laatulöpinät 30: [Tietoturvallisuus ohjelmistokehityksessä](https://www.arter.fi/podcast/laatulopinat-podcast-tietoturvallisuus-ohjelmistokehityksessa-tarkastele-kokonaisuutta-ja-hyodynna-viitekehykset/).
