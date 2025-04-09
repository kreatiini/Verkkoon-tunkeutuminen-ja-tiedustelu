# h2 Lempiväri: violetti
## Tiivistelmä tehtävästä, tehtävänannot ja oman tietokoneen tiedot
Osa tehtävistä oli haasteellisia. Aika loppui myös kesken vaikka tein tehtävää useaan otteeseen. Aika loppui kesken g kohdassa. Korjaan lähteet kun saan leikepöydän kuntoon. Teen myös tehtävät loppuun ja merkitsen mitkä on tehty palautksen jälkeen. 

### Tehtävänanto:
       x) Lue ja vastaa lyhyesti kysymyksiin. Tässä alakohdassa x ei tällä kertaa tarvitse lukea artikkeleita kokonaan, ei tarvitse tiivistää niitä, eikä tehdä testejä koneella.
        Selitä tuskan pyramidin idea 1-2 virkkeellä. Bianco 2013: Pyramid of Pain. (Katso eritoten pyramidin kuvaa.)
        Selitä timanttimallin (Diamond Model) idea 1-2 virkkeellä. Tekijä esittelee sen aika juhlallisesti, voit myös etsiä yksinkertaisempia artikkeleita hakukoneella tai kelata suoraan timantin kuvaan. Caltagirone et al 2013: Diamond Model
    a) Apache log. Asenna Apache-weppipalvelin paikalliselle virtuaalikoneellesi. Surffaa palvelimellesi salaamattomalla HTTP-yhteydellä, http://localhost . Etsi omaa sivulataustasi vastaava lokirivi. Analysoi yksi tällainen lokirivi, eli selitä sen kaikki kohdat. (Jos Apache ei ole kovin tuttu, voit tätä tehtävää varten vain asentaa sen ja testata oletusweppisivulla. Eli ei tarvitse tehdä omia kotisvuja tms.)
    b) Nmapped. Porttiskannaa oma weppipalvelimesi käyttäen localhost-osoitetta ja 'nmap -A' päällä. Selitä tulokset. (Pelkkä http-portti 80/tcp riittää)
    c) Skriptit. Mitkä skriptit olivat automaattisesti päällä, kun käytit "-A" parametria? (Näkyy avoimien porttinumeroiden alta, http-blah, http-blöh...).
    d) Jäljet lokissa. Etsi weppipalvelimen lokeista jäljet porttiskannauksesta (NSE eli Nmap Scripting Engine -skripteistä skannauksessa). Löydätkö sanan "nmap" isolla tai pienellä? Selitä osumat. Millaisilla hauilla tai säännöillä voisit tunnistaa porttiskannauksen jostain muusta lokista, jos se on niin laaja, että et pysty lukemaan itse kaikkia rivejä?
    e) Wire sharking. Sieppaa verkkoliikenne porttiskannatessa Wiresharkilla. Huomaa, että localhost käyttää "Loopback adapter" eli "lo". Tallenna pcap. Etsi kohdat, joilla on sana "nmap" ja kommentoi niitä. Jokaisen paketin jokaista kohtaa ei tarvitse analysoida, yleisempi tarkastelu riittää.
    f) Net grep. Sieppaa verkkoliikenne 'ngrep' komennolla ja näytä kohdat, joissa on sana "nmap".
    g) Agentti. Vaihda nmap:n user-agent niin, että se näyttää tavalliselta weppiselaimelta.
    h) Pienemmät jäljet. Porttiskannaa weppipalvelimesi uudelleen localhost-osoitteella. Tarkastele sekä Apachen lokia että siepattua verkkoliikennettä. Mikä on muuttunut, kun vaihdoit user-agent:n? Löytyykö lokista edelleen tekstijono "nmap"?
    i) Hieman vaikeampi: LoWeR ChEcK. Poista skritiskannauksesta viimeinenkin "nmap" -teksti. Etsi löytämääsi tekstiä /usr/share/nmap -hakemistosta ja korvaa se toisella. Tee porttiskannaus ja tarkista, että "nmap" ei näy isolla eikä pienellä kirjoitettuna Apachen lokissa eikä siepatussa verkkoliikenteessä. (Tässä tehtävässä voit muokata suoraan lua-skriptejä /usr/share/nmap alta, 'sudoedit'. Muokatun version paketoiminen siis rajataan ulos tehtävästä.)
    j) Vapaaehtoinen, vaikea: Invisible, invincible. Etsi jokin toinen nmap:n skripti, jonka verkkoliikenteessä esiintyy merkkijono "nmap" isolla tai pienellä. Muuta nmap:n koodia niin, että tuo merkkijono ei enää näy verkkoliikenteessä.
  
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

## x) Lue ja vastaa lyhyesti kysymyksiin
 a) Selitä tuskan pyramidi lyhyesti kahdella virkkeellä(Bianco 2013: Pyramid of Pain):
 - Tuskan pyramidi esittää eri merkit joista voidaan tunnistaa hyökkääjän toimintaa ja kuinka paljon eri alueiden estäminen aiheuttaa päänvaivaa hyökkääjälle.
 b) Selitä timanttimallin idea 1-2 virkkeellä.
 - Timanttimallissa tarkastellaan hyökkääjän, keinojen ja uhrin välisiä suhteita. 

### Lähteet:
- Tehtävän lähteet tähän

## a) Apachen lokit
Aloitin asentamalla Apachen ``sudo apt-get update `` ``sudo apt-get install apache2`` ``sudo systemctl start apache2`` ja avasin ``http://localhost`` etusivun. Vastaan tuli Apachen oletussivu. Tämän jälkeen ryhdyin lokien metsästykseen. Siirryin lokeihin ``cd /var/log/apache2`` ja listasin lokit ``cat access.log``. Tämän jälkeen valitsin ensimmäisen http pyynnön:
``127.0.0.1 - - [09/Apr/2025:01:40:35 -0400] "GET / HTTP/1.1" 200 3383 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0"``
Ensin tulee pyynnön esittänyt ip osoite eli tässä tapauksessa ``127.0.0.1``. Seuraavana olevan viivan kohdalla olisi RFC1413 tunniste mutta Apachen dokumentaation mukaan sen ei tulisi olla päällä koska se on yleensä todella epätarkka. 

Seuraavana olevan viivan kohdalla olisi ``userid`` mikäli käyttäjä olisi tunnistettu käyttäjä. En kuitenkaan ole joten siinäkin on vian viiva. 

``[09/Apr/2025:01:40:35 -0400]`` on kellonaika jolloin pyyntö on tehty muodossa päivä/kuukausi/vuosi:tunnit:minuutit:sekunnit aikavyöhyke.

``"GET / HTTP/1.1"`` Kertoo että kyseessä on ``GET`` pyyntö. Pelkän kauttaviivan kohdalla näkyisi mitä käyttäjä on pyytänyt esim ``/favicon.ico``. Tässä tapauksessa se on kuitenkin tyhjä. Viimeinen osa ``HTTP/1.1`` kertoo mitä protokollaa on käytetty ja sen version. 

``200`` Tarkoittaa statuskoodia. 200 tarkoittaa OK. Siinä voisi myös esim olla 404 eli not found jolloin sivun lataus on epäonnistunut.

``3383`` Kertoo paljonko dataa on lähetetty käyttäjälle. Tässä ei ole mukana headereita. 

``"-"`` Kohdassa näkyisi miltä sivulta käyttäjä on siirtynyt sivulle jota pyydetään. Eli esim klikkailemalla alavalikoita sivulla ja vaihtamalla samalla sivustolla tässä näkyisi lähtösivu. 
``"Mozilla 5.0 (X11; Linux x86_64; rv:128.0)`` Kertoo selaimen ja selaimen version, Käyttöjärjestelmän sekä user-agentin. Sama näkyy myös lopussa eli ``Gecko/20100101 Firefox128.0``.


### Lähteet:
- [Apache Docs](https://httpd.apache.org/docs/2.4/en/logs.html)

## b) nmapped
Seuraavana oli tarkoitus porttiskannata oma palvelin. Otin Kalin pois verkosta varmuuden vuoksi tätä tehtävää varten. Tämän jälkeen avasin nmapin ja ajoin ``nmap -v -A 127.0.0.1/80``

Tulos näytti tältä: 
nmaplocal

- Alkuun selviää että host is up eli palvelin on päällä.
- Portti 80/tcp on auki ja siellä on Apache2 httpd 2.4.63 (Debian) eli versio ja käyttöjärjestelmä johon tehty.
- Nähdään että tukee seuraavia http metodeja: GET POST OPTIONS HEAD
- Nähdään http otsikko ja palvelimen headeri.
- Laitteen tyyppi tässä tapauksessa vain general purpose.
- Linux versio eli 2.6.X|5.X
- CPE OS eli Common Platform Enumeration käyttöjärjestelmän tiedoista. o: jälkeen tulee tietoja käyttöjärjestelmästä.
- Linux kernelin versio
- Uudestaan lisää tietoa käyttöjärjestelmästä
- Arvaus siitä kauanko palvelin on ollut päällä. Tämä on käyttöjärjestelmäriippuvainen ja voi olla paljonkin pielessä.
- Etäisyys palvelimeen eli montako hyppyä. Tässä tapauksessa 0 sillä kyse on samasta laitteesta.
- TCP sequence prediction. Eli jos TCP sequence luonti on heikkoa voisi olla mahdollista arvata seuraava numero ja lähettää paketteja. Tässä tapauksessa se on todella vaikeaa. Asteikko on easy,medium,formidable, worthy challenge ja good luck!.
- IP ID Sequence generation kertoo ID:n luontialgoritmista. 

### Lähteet:
- Nmap documentation https://nmap.org/book/osdetect-usage.html

## c) Skriptit
En ihan ymmärtänyt tätä. Tarkoitetaanko tässä ``http-methods`` ``http-title`` ja ``http-server-header`` kohtia?

### Lähteet:
- Tehtävän lähteet tähän
   
## d) Jäljet lokissa
Menin takaisin Apachen lokeihin ``cd var/log/apache2`` ja ``cat access.log``. 
Lokissa on useita rivejä joissa lukee ``compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)"`` . Näillä tunnistaa selvästi mitkä pyynnöt on tehty nmapilla.
Nmap kokeilee erilaisia keinoja GET POST UOXB PROPFIND. Se kokeilee löytyykö palvelimelta esim tiedostoja tai pystyykö palvelimelle syöttämään komentoja. 
Jos kyseessä olisi iso lokitiedosto käyttäisin ``grep -i "nmap" access.log``. Jättäisin myös ``-i`` lipulla kirjainkoon huomioimatta. 
eli esim:

GREPKUVA

### Lähteet:
- Tehtävän lähteet tähän

## e) Wiresharking 
Käynnistin wiresharkin ja kaappasin lo liikenteen. Tämän jälkeen suodatin paketit joissa on sana nmap.
![image](https://github.com/user-attachments/assets/93976388-c84b-46b6-81d2-730dad7f1f9b)

Näistä en osaa juurikaan kertoa enempää kuin aiemmassa analyysissa. Eli nmap lähettää erilaisia pyyntöjä selvittääkseen eri asioita palvelimesta ja avoimista porteista. 
Näissä näkyy pyynnön lähettäjä ja kohdeip. Tarkemmista tiedoista löytyy esim. user-agent josta löytyy myös nmap. 
### Lähteet:
- Tehtävän lähteet tähän

## f) netgrep
Availin uuden terminaalin ja aloitin kaappauksen ``sudo ngrep -d lo 'nmap'`` :

![image](https://github.com/user-attachments/assets/7741a19c-7399-4f45-874d-6b73c206b028)

Jostain syystä leikepöytä lakkasi toimimasta joten en saa myöskään lähteitä kopioitua. Laitan lähteet kuntoon kun saan sen toimintaan.
### Lähteet:
- ngrep - network grep. 

## g) Agentti
Seuraavana lähdin perehtymään nmapin user-agentin vaihtoon. Kokeilin ajaa ``sudo nmap -v -A 127.0.0.1/80 http.useragent="MozillaVaan"`` testinä mutta en saanut sitä toimimaan. Ryhdyin pläräämään läpi nmapin skriptejä. Tässä kohtaa alkoi aika loppumaan joten joudun palauttamaan tehtävän keskeneräisenä. Korjaan leikepöydän, lisään kuvat ja lähteet sekä viimeiset osiot ennen luentoa. Tietysti selvästi merkittynä mitkä on tehty palautusajan jälkeen myöhempänä muokkauksena.

### Lähteet:
- Tehtävän lähteet tähän

## tehtävä5

### Lähteet:
- Tehtävän lähteet tähän

## Lähteet:
  -  Tehtävät: Karvinen & Iso-Anttila 2025: Verkkoon tunkeutuminen ja tiedustelu Luettavissa: [https://terokarvinen.com/palvelinten-hallinta/](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/)
