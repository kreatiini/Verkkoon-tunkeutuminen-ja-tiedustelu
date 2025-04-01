# h1 Sniff

## Tiivistelmä tehtävästä, tehtävänannot ja oman tietokoneen tiedot


### Tehtävänanto:
       x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)
        Karvinen 2025: Wireshark - Getting Started
        Karvinen 2025: Network Interface Names on Linux
    a) Linux. Asenna Debian tai Kali Linux virtuaalikoneeseen. (Tätä alakohtaa ei poikkeuksellisesti tarvitse raportoida, jos sinulla ei ole mitään ongelmia. Jos on mitään haasteita, tee täsmällinen raportti)
    b) Ei voi kalastaa. Osoita, että pystyt katkaisemaan ja palauttamaan virtuaalikoneen Internet-yhteyden.
    c) Wireshark. Asenna Wireshark. Sieppaa liikennettä Wiresharkilla. (Vain omaa liikennettäsi. Voit käyttää tähän esimerkiksi virtuaalikonetta).
    d) Oikeesti TCP/IP. Osoita TCP/IP-mallin neljä kerrosta yhdestä siepatusta paketista. Voit selityksen tueksi laatikoida ne ruutukaappauksesta.
    e) Mitäs tuli surffattua? Avaa surfing-secure.pcap. Tutustu siihen pintapuolisesti ja kuvaile, millainen kaappaus on kyseessä. Tässä siis vain lyhyesti ja yleisellä tasolla. Voit esimerkiksi vilkaista, montako konetta näkyy, mitä protokollia pistää silmään. Määrästä voit arvioida esimerkiksi pakettien lukumäärää, kaappauksen kokoa ja kestoa.
    f) Mitä selainta käyttäjä käyttää? surfing-secure.pcap
    g) Minkä merkkinen verkkokortti käyttäjällä on? surfing-secure.pcap
    h) Millä weppipalvelimella käyttäjä on surffaillut? surfing-secure.pcap
        Huonoja uutisia: yhteys on suojattu TLS-salauksella.
    i) Analyysi. Sieppaa pieni määrä omaa liikennettäsi. Analysoi se, eli selitä mahdollisimman perusteellisesti, mitä tapahtuu. (Tässä pääpaino on siis analyysillä ja selityksellä, joten liikennettä kannattaa ottaa tarkasteluun todella vähän - vaikka vain pari pakettia. Gurut huomio: Selitä myös mielestäsi yksinkertaiset asiat.)
  
### Tietokoneen tiedot: 
- Näytönohjain: Asus GeForce RTX 3070 Ti ROG Strix - OC Edition
- Virtalähde: Corsair 750W SF Series SF750, modulaarinen SFX-virtalähde
- Emolevy: Asus ROG STRIX B550-I GAMING, Mini-ITX -emolevy
- Prosessori: AMD 5800x3D
- RAM: Corsair 32GB (2 x 16GB) Vengeance LPX, DDR4 3600MHz, CL18,
- SSD: Samsung 1TB 980 SSD-levy, M.2 2280, PCIe 3.0 x4, NVMe 1.4, sekä Kingston 1TB A2000 NVMe PCIe SSD-levy, M.2 2280, 2200/2000
- Käyttöjärjestelmä: Edition	Windows 10 Pro Version	22H2
- Virtuaaliympäristö: VirtualBox Version 7.0.14 r161095 (Qt5.15.2)
- Operating System: Kali Linux

## x) Lue ja tiivistä
### Wireshark - Getting Started (Karvinen 2025)
 - Wiresharkissa on mahdollista suodattaa näkyviä paketteja esimerkiksi protokollien tai osoitteiden mukaan.
 - Wiresharkista löytyy myös hyödyllisiä tietoja tiivistelmien muodossa kuten eri hostit joita kyseisessä kaappauksessa on
 - On myös mahdollista tallentaa oma kaappaus ja tarkastella sitä myöhemmin

### Network interface names on Linux (Karvinen 2025)
- Network interface ei tarkoita samaa kuin network card sillä interface ei välttämättä ole fyysinen.
- wl on WLAN, en on Ethernet ja lo on loopback
- ip a ja ip route komennoilla voi katsoa omat network interfacet.

### Lähteet:
- Wireshark getting started (Karvinen 2025) Luettavissa: https://terokarvinen.com/wireshark-getting-started/ Luettu 1.4.2025
- Network Interface names on Linux (Karvinen 2025) Luettavissa: https://terokarvinen.com/network-interface-linux/ Luettu 1.4.2025

## a) Asenna kali

Tässä kohdassa ei ollut haasteita.

## b) Ei voi kalastaa
Tehtävässä piti osoittaa, että laite on irti verkosta. Otin netin pois Kali virtuaalikoneesta ja testasin sekä selailemella että ping komennolla:
![ping](https://raw.githubusercontent.com/kreatiini/Verkkoon-tunkeutuminen-ja-tiedustelu/refs/heads/main/kuvat/h1/ping.png)
![browser](https://raw.githubusercontent.com/kreatiini/Verkkoon-tunkeutuminen-ja-tiedustelu/refs/heads/main/kuvat/h1/browser.png)

## c) Wireshark
Kali Linuxissa on Wireshark valmiiksi asennettuna. Ei siis tarvinnut tehdä asennustoimenpiteitä. 
Käynnistin Wiresharkin ja valitsin "eth0" interfacen. Tämän jälkeen selailin hieman verkossa saadakseni luotua liikennettä. Samalla näin Wiresharkiin ilmestyvän dataa. Liikennettä näkyi joten homma rokkaa:

![wireshark](https://raw.githubusercontent.com/kreatiini/Verkkoon-tunkeutuminen-ja-tiedustelu/refs/heads/main/kuvat/h1/Wireshark1.png)

   
## d) Oikeesti TCP/IP
![TCPIP](https://github.com/user-attachments/assets/6457c3c1-8cc8-4f5e-a382-bd375e7c6c76)

Ylemmässä kuvassa näkyy kaikki 4 kerrosta: 1. Link Layer 2. Internet Layer 3. Transport Layer 4. Application Layer
 - Link Layer: Link Layer kohdassa näkyy destination mac address ja source mac address.
 - Internet Layer: Tässä kohdassa näkyy source ip address ja destination ip address. Eli mihin ip osoitteeseen paketti on matkalla ja mistä se on tulossa.
 - Transport layer: tässä näkyy käytetty protokolla eli TCP. Lähtöportti sekä kohdeportti. 
 - Application Layer: Siitä näkee että kyseessä on HTTP protokolla. Tarkemmista tiedoista löytyy myös palvelin ja data mitä siirretään. 


## e) Mitäs tuli surffailtua?
Tutkailtuani kaappausta ensimmäinen ajatukseni oli, että kyseessä oli kirjautuminen johonkin. Ensin otetaan yhteys itse sivulle ja tämän jälkeen kirjaudutaan sinne sisään. En kuitenkaan ole tästä täysin varma. Itse kaappaus kestää vajaan 8 sekuntia joten ajallisestikin se voisi täsmätä. Vain yksi kone ottaa yhteyttä palvelimille jotka vastailevat. Tässä käytetään TCP protokollaa, TLS protokollaa, ARP protokollaa, DNS protokollaa, IP protokollaa, HTTP protokollaa, UDP protokollaa. Itse kaappaus on aika pieni.



## f) Mitä selainta käyttäjä käyttää?
Selailin pitkään läpi paketteja. En onnistunut löytämään yhtään HTTP pakettia ilman TLS salausta. En siis näe salaamatonta user-agent kenttää josta saisin tiedot tähän. 


## f) Mitä verkkokorttia käyttäjä käyttää?
Kokeilin MAC osoitteella löytää OUI hausta verkkokortin merkkiä. En kuitenkaan saanut tuloksia. 

### Lähteet:
- Tehtävän lähteet tähän

## f) Millä weppipalvelimilla käyttäjä on selaillut?
Ainakin terokarvinen.com, google.com,  




## g) Analyysi
Valitsin tähän 2 tcp kättelyn pakettia.
Ensimmäinen paketti:
![paketti1](https://raw.githubusercontent.com/kreatiini/Verkkoon-tunkeutuminen-ja-tiedustelu/refs/heads/main/kuvat/h1/packet1.1.png)

![paketti1.2](https://raw.githubusercontent.com/kreatiini/Verkkoon-tunkeutuminen-ja-tiedustelu/refs/heads/main/kuvat/h1/packet1.2.png)

 - Ethernet kohta: Siitä näkee Lähde MAC osoitteen ja kohteen MAC osoitteen. 
 - Internet Protocol Version 4: Kertoo että käytössä on IPV4. PAketti on lähtenyt osoitteesta 10.0.2.15 ja kohde on 216.58.209.195. Siinä näkyy myös Time To Live joka on 64. Niin monta ''hyppyä'' paketti tekee ennenkuin se putoaa pois. Siitä näkee myös headerin ja paketin koon. Näkyy myös että paketti tulee TCP protokollan kautta. Checksumin avulla tarkistetaan onko paketti korruptoitunut.
- TCP kohdassa näkyy lähtöportti ja kohdeportti. Siinä näkyy myös sequence number joka kertoo monesko TCP yhteys on kyseessä. Tämä on ensimmäinen.
Tiedoista näkee että tämä keskustelu on kesken eli tässä vaiheessa 3 way handshake on vielä kesken. Sieltä löytyy myös Header osion koko ja liput. Eli nyt on kyseessä SYN pyyntö ennen tiedon siirtoa. Client ja Server varmistuvat siis että tiedonsiirto voi alkaa. 

Toinen paketti:

![paketti2](https://raw.githubusercontent.com/kreatiini/Verkkoon-tunkeutuminen-ja-tiedustelu/refs/heads/main/kuvat/h1/packet2.1.png)

![paketti2.2](https://raw.githubusercontent.com/kreatiini/Verkkoon-tunkeutuminen-ja-tiedustelu/refs/heads/main/kuvat/h1/packet2.2.png)

Toisessa paketissa on kyseessä SYN ACK paketti. 
- Ethernet kentästä näkee taas lähtö ja kohde MAC osoitteet. 
- Internet Protocol kentästä näkyy lähtö ja kohde IP osoitteet. Nyt siis nämä ovat toisinpäin kuin edellisessä paketissa.  TTL kenttä pysyy samana sillä 64 on yleinen oletus TTL.
- TCP kentässä myös portit ovat kääntyneet tietysti toisinpäin. Nyt kyseessä on SYN+ACK. Sequence number pysyy samana sillä kyseessä on edelleen sama kättely. Wireshark kertoo myös että tämä on ACK segment edelliseen pakettiin liittyen. 




## Lähteet:
  -  Tehtävät: Karvinen & Iso-Anttila 2025: Verkkoon tunkeutuminen ja tiedustelu Luettavissa: [https://terokarvinen.com/palvelinten-hallinta/](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/)
