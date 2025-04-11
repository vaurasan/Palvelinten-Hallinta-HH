# h3 Infraa koodina

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

Käyttöjärjestelmä: Windows 11 Pro 24H2

#### Virtuaalikone
Oracle VirtualBox 7 - Debian 12 GNU/Linux (bookworm)<br>
6 Prosessoriydintä - 4GB RAM-muistia - 60GB tallennustilaa

## x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)

#### Karvinen 2014: [Hello Salt Infra-as-Code](https://terokarvinen.com/2024/hello-salt-infra-as-code/)

- Tässä luodaan niin sanottu salt:n "Hello world"
- Aluksi asennetaan salt-minon: **sudo apt-get -y install salt-minion**
- Luodaan kansio "hello" moduulille **sudo mkdir -p /srv/salt/hello/** <-- srv/salt on minionien jaettu kansio, hello/ <-- tulee sisältämään kaikki tähän "hello worldiin" liittyvät tiedostot
- /srv/salt/hello kansioon luodaan ajettava tiedosto "init.sls": **sudoedit init.sls** <-- init.sls sisältää tämän "hello world" projektin koodin, tässä tapauksessa kirjoitetaan tiedostoon:
```
/tmp/hellotero:
  file.managed
```
- Tämän jälkeen voidaan kutsua hello kansion init.sls tiedostoa komennolla **sudo salt-call --local state.apply hello**
- Jos kaikki onnistui, nyt minion on luonut tmp/ kansioon tiedoston "hellotero"
- Idempotenttina käskynä komennon uudelleen ajaminen ei luo uutta tiedostoa, jos semmoinen löytyy jo

#### Salt contributors: [Salt overview](https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml) Kohdat: Rules of YAML, YAML simple structure, Lists and dictionaries - YAML block structures

Rules of YAML
- Salt:ssa usein käytetään YAML renderöintiä, YAML renderöinnillä YAML tietorakenne kootaan Python datarakenteeksi Salt:iin
- Data on strukturoitu **key: value** (avain: arvo) pareina
- Kaksoispiste + välilyönti erottaa avaimen ja arvon toisistaan (": ")
- Avainten arvo voi olla monella eri rakenteella
- Kaikkien avainten ja ominaisuuksien kirjainkoolla on merkitystä
- Tabulaattoria ei sallita YAML:ssä, on käytettävä välilyöntejä
- Kommentit alkavat "#" merkillä




## Otsikko




## Otsikko




##




##



Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html<br>
Pohjana Tero Karvinen 2025: Palvelinten Hallinta - Configuration Management Systems course - 2025 spring, https://terokarvinen.com/palvelinten-hallinta/<br><br>
Kirjoittanut <em>Santeri Vauramo</em> 2025
