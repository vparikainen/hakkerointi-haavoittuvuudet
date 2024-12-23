# h6 - Sulaa hulluutta
|       |   Ympäristö                |
|--------- | ------------------------------- |
| **OS** | Debian 12.7.0  |
| **Browser** | Firefox 128.3.1esr |
| **Hardware** | innotek Gmhb VirtualBox |
| **Network** | Intel PRO/1000 MT Desktop (NAT) |
## a) Tutki tiedostoa h1.jpg jo opituilla työkaluilla. Mitä saat selville?

Aloitin tiedoston tarkastelemisen kokeilemalla ``file``-komentoa. Tiedostosta sai selville sen olevan JPEG kuvatiedosto jonka resoluutio on 1024x1024.

![file h1.jpg](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h6-jpg1.png)

``cat``-komento näytti vain kasan sekavia merkkejä.

![cat h1.jpg](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h6-jpg4.png)

## b) Tutki tiedostoa h1.jpg binwalk:lla. Mitä tietoja löydät nyt tiedostosta? Mitä työkalua käyttäisit tiedostojen erottamiseen? (Huomaa, että binwalk versio 2.x ja 3.x toimivat eri tavalla.)

Aloitin asentamalla binwalkin, jonka jälkeen ajoin komennon ``binwalk`` h1.jpg-tiedostolle. JPEG ja TIFF -kuvadatan lisäksi tiedostossa näyttäisi olevan myös paljon Zip archive dataa joka muodostaa jonkinlaisen word xml-tiedoston.

![binwalk h1.jpg](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h6-jpg2.png)

Ajoin ``binwalk -e``-komennon avatakseni zip-tiedostot, siirryin uuteen kansioon ja löysin sieltä _[Content_Types].xml_-tiedoston. Kansiossa oli myös muita kansioita; _docProps_, __rels_ sekä _word_. Näiden sisältä löytyi lisää kansioita ja tiedostoja, mutta en saanut yhtään tiedostoa auki.

![zipin sisältö](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h6-jpg3.png)

En ole varma, miten tiedostoja olisi paras tapa lähteä avaamaan.

## c) FOSS (Free Android OpenSource). Tutustu Android-sovelluksiin Offan (2024) listalta: Android FOSS. Valitse listalla itsellesi mielenkiintoisin applikaatio ja mene sen GitHubiin. Lataa ohjelman APK itsellesi ja käytä seuraavia työkaluja tutustuaksesi, miten APK:n voi avata.

Valitsin listalta sovelluksen [FreePaint](#viitteet)

- ZIP

Purin _app-release.apk_-tiedoston kansioon _drawing_app_ ja katsoin, mitä sen sisällä on.

![zip apk](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h6-foss1.png)

- JADX

Latasin jadx:n ja avasin sillä _app-release.apk_-tiedoston. Jadx raksutti hetken, ja sitten pääsin käsiksi apk:n lähdekoodiin.

![jadx apk](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h6-foss2.png)

- Bytecode-viewer

Latasin bytecode-viewerin ja avasin _app-release.apk_-tiedoston sillä.

![bytecode apk](https://github.com/vparikainen/hakkerointi-haavoittuvuudet/blob/main/pics/h6-foss3.png)

### Viitteet

Android FOSS: [FreePaint](https://github.com/pastthepixels/FreePaint)
