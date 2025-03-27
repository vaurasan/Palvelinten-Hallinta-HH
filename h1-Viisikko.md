# h1 Viisikko

#### Oma Host kokoonpanoni:

| Komponentti | Kuvaus | Lisätiedot |
| :---        |    :----:   |          ---: |
| Emolevy | MSI B550-A PRO | ATX, AM4 |
| Prosessori   | AMD Ryzen 9 5900X | 12-Core 3.70 GHz |
| RAM   | G.Skill  Ripjaws V |  32GB (4x8GB) DDR4 3600MHz, CL 16, 1.3  |
| Näytönohjain   | Sapphire PULSE AMD Radeon RX 7900 GRE        | 16GB     |
| Kovalevy   | Kingston 1TB        | A2000 NVMe PCIe SSD M.2      |
| Kovalevy   | Crucial 512GB        | MX100 SSD     |
| Kovalevy   | Crucial 256GB        | MX100 SSD     |
| Virtalähde   | Asus 750W TUF Gaming Gold        | ATX 80 Plus      |
| Kotelo   | Phanteks Enthoo Pro       |  Full Tower      |

Käyttöjärjestelmä: Windows 11 Pro 23H2

#### Virtuaalikone
Oracle VirtualBox 7 - Debian 12 GNU/Linux (bookworm)<br>
6 Prosessoriydintä - 8GiB RAM-muistia - 60GB tallennustilaa

## x) Lue ja tiivistä:

##### Karvinen 2023: [Run Salt Command Locally](https://terokarvinen.com/2021/salt-run-command-locally/)
> - Salt-komentoja voidaan ajaa paikallisesti testimielessä
> - Samat komennot toimivat sekä Linuxissa, että Windowsissa
> - Tärkeimmät funktiot ovat: pkg, file, service, user ja cmd
> - Normaalisti Saltia käytetään ohjaamaan useita orjia verkon yli
##### Karvinen 2018: [Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux](https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/)
> - Saltilla voidaan ohjata jopa tuhansia tietokoneita
> - Ainoastaan master-koneella täytyy olla julkinen osoite, orjat voivat olla "piilossa"
> - Orjat voivat olla NAT:n ja palomuurin takana, tuntemattomassa verkossa
> - Jos masterilla on palomuuri, tulee tehdä reiät palomuurin 4505/tcp ja 4506/tcp portteihin
> - Orjan tulee tietää, missä master on, orjille voi antaa oman id:n, jokaisella orjalla täytyy olla oma id
##### Karvinen 2006: [Raportin kirjoittaminen](https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/)
> - Raportista tulee ilmetä mitä on tehty, sekä mitä seurauksia teoilla on ollut
> - Raporttia kannattaa kirjoittaa suoraan sähköisesti samalla kun tekee tehtäviä
> - Ongelmien tutkimisessa on hyvä kirjoittaa itselle muistiinpanoja, tämä selkeyttää asioita
> - Ympäristö tulee raportoida myös, jotta raportin tulos olisi toistettavissa. Eli siis testikokoonpano
> - Ole täsmällinen raportoidessa
> - Kirjoita selkeää tekstiä
> - Muista merkitä lähteet
> - Älä sepitä, vaan kerro rehellisesti mitä olet tehnyt, älä plagioi
##### WMWare Inc: [Salt Install Guide: Linux (DEB)](https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html) (poimi vain olennainen osa)
> - Varmistetaan, että keyrings-kansio on olemassa
> - Ladataan Salt Projectin julkinen avain ja luodaan asetukset, jolla voidaan ladata ja asentaa Salt Project repositorystä **apt-get**:llä
> - Päivitetään metadata **sudo apt update**
> - Asennetaan salt-minion, salt-master, sekä muut Salt-komponentit
> - STS:ää ei suositella tuotantokäyttöön, Salt Project suosittelee LTS-julkaisuja tuotantoympäristöihin

## a) Asenna Debian 12-Bookworm virtuaalikoneeseen. (Poikkeuksellisesti tätä alakohtaa ei tarvitse raportoida, jos siinä ei ole mitään ongelmia. Mutta jos on ongelmia, sitten täsmällinen raportti, jotta voidaan ratkoa niitä yhdessä.)
Minulla oli jo valmiiksi Oraclen Virtual Box ja siinä useampi Debian 12-Bookworm-käyttöjärjestelmällä oleva virtuaalikone. 

Pari päivää sitten käynnistelin pienen tauon jälkeen Virtual Boxin ja sepä ei enää toiminutkaan, virtuaalikoneita ei pystynyt enää käynnistämään.

Lueskelin Oraclen foorumeilta tietoja ja muillakin oli samanlaisia ongelmia.

Poistin asennuksen ja asensin uudelleen pääkäyttäjänä, sama ongelma jatkui.

Lopulta poistin asennuksen, latasin toiseksi uusimman version 7.1 https://www.virtualbox.org/wiki/Download_Old_Builds ja se lähti toimimaan normaalisti.

Loin vielä uuden Debianilla varustetun virtuaalikoeen ja tein perus alkuasetukset

## b) Asenna Salt (salt-minion) Linuxille (uuteen virtuaalikoneeseesi)
Tässä tulee kyseeseen X-kohdassa mainittu sivu https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html

- Varmistan, että "keyrings" kansio löytyy komennolla **mkdir -p /etc/apt/keyrings**
- Ladataan Salt Projectin julkinen avain **curl -fsSL https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public | sudo tee /etc/apt/keyrings/salt-archive-keyring.pgp**
- Luodaan konfigurointi repositorylle **curl -fsSL https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources | sudo tee /etc/apt/sources.list.d/salt.sources**
- Päivitetään pakettilista **sudo apt-get update**

Nyt siirryn Karvisen (2021) ohjeeseen [https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/](https://terokarvinen.com/2021/salt-run-command-locally/)

Sekä Karvisen (2018) https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/

- Asennetaan salt-minion komennolla **sudo apt-get -y install salt-minion**
- Testaan, että minulla on salt **sudo salt-call --version**, palautuu: "salt-call 3007.1 (Chlorine)", voidaan olettaa, että asennus onnistui

## c) Viisi tärkeintä. Näytä Linuxissa esimerkit viidestä tärkeimmästä Saltin tilafunktiosta: pkg, file, service, user, cmd. Analysoi ja selitä tulokset.




Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html<br>
Pohjana Tero Karvinen 2025: Palvelinten Hallinta - Configuration Management Systems course - 2025 spring, http://terokarvinen.com<br><br>
Kirjoittanut <em>Santeri Vauramo</em>, 2025
