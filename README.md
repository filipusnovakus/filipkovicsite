# filipkovicsite
jedu speedrun podle sebe gg
-------------------------------------------------------------------------------------------------------
10.Windows Server
-------------------------------------------------------------------------------------------------------
10. Windows Server
-struktura Windows Serveru
-Popište strukturu serveru. Vysvětlete funkci HAL, jádra, služeb, GUI.o Co je třeba uvážit před počátkem instalace?
Jadro - kernel - jadro operacniho systemu, pri bootovani je mu prevedeno vedeni 
HAl - HARDWARE ABSTRRACTION LAyer - hardwarova abstrakcni sluzba - vytvari jednotne rozhrani ovladajici
ruzne fungujici hardware
zajistuje komunikaci mezi hardwarem a jadrem
GUI - uzivatelske rozhrani ktere umoznuje ovladat pc 
pred zacatkem instalace bychom meli uvazit zda pocitac splnuje technicke pozadavky a financni moznosti klienta

-Jaký je rozdíl mezi jednotlivými edicemi serveru (essentials, standard, datacenter...)?
essentials - omezeny pocet uzivatelu, omezeni 64gb , neobsahuje cal
standart - nad ramec male firmy, mozne pripojeni je 250 uzivatelu, podporovane jsou role - ad dns dhcp iis,
 obsahuje cal, 4tb
datacenter - pro virtualizace - podpora 2- 64 procesoru - neomezena licencni prava pro virtualizaci obsahuje cal, 4tb


-Jaké jsou možnosti ovládání Windows Serveru?
GUI - CMD - DALKOVE PRIPOJENI
-role, funkce, služby; jejich instalace a konfigurace
-Vysvětlete, co jsou u WS role a funkce, jaký je jejich vztah ke službám?
Role - sada softwarovych programu, ktere v pripade spravne instalace a konfigurace mohou plnit urcite funkce 
Funkce - nejsou primo soucast roli ale mohou je rozsirovat nebo podporovat
Sluzby - zajistuji spravny chod rolí, bezi na pozadi.

-Jako příklad nainstalujte roli DHCP server. Vysvětlete všechna dílčí nastavení.

--------------------------------------------------------------------------------------------------------------------
12. Active Directory
-------------------------------------------------------------------------------------------------------------------
-struktura Active Directory
fyzicka - site
	- domain controlers (servery starajici se o domenu)
logicka - forest  - bezpecnostni hranice a objekty sdilene v ramci AD

-Co je Active Directory a k čemu slouží?
Active directory je adresarova sluzba od microsoftu
Slouzi pro spravu uzivatelu, uctu a pocitacu, plus overovani


-Jaké typy objektů v AD existují, vysvětlete funkci jednotlivých organizačních jednotek, vytvořených po instalaci AD
OU - organization unit - nejmensi jednotka, muzeme je do sebe vnorovat a nebo pridavat nova opravneni
Conntainer - organizacni jednotka - muzeme tvorit skupiny
Computers - overovani udaju pocitace
users - overovani prihlasovani uzivatele 
shared folders - sdilene slozky
printers - tiskarny
Groups - seskupuji uzivatele. pocitace a skupiny

-Operation master roles
Naming master - stara se o pridavani domen
Infrastructure master - vyuziva global catalog, stara se o vztahy mezi objekty z jinzch domen
RID master - sprava rid identifikatoru (RID identifikatory slouzi pro generovani sid)
PDC master - kompabilita se starsimy systemy
Schema master - stara se o databaze AD

-Místní a cestovní profil uživatele
Mistni profil - pouze na jednom PC
Cestovni profil - pro vsechny pc

-Co jsou zděděná oprávnění? Jak je v případě potřeby odstranit?
zdedena opravneni jsou opravneni ktera uzivatel dedi podle skupiny

-Zařazení do skupin, změna zařazení, výchozí skupina
mistni domenove skupiny - uzivatele v ramci mistni domeny, mohou obsahovat uzivatele z jinych domen- ale prava se 
nastavuji pouze pro uzivatele dane domeny
globalni skupiny - uzivatele pouze v ramci domeny v niz je definovana, obsahuje pouze uzivatele dane domeny, ale meni
prava v ramci domenove struktury
univerzalni skupiny - uzivatele z jinych domen, pridelovani prav v ramci domenovych struktur


--------------------------------------------------------------------------------------------------------------------
13. DNS WINDOWS
-------------------------------------------------------------------------------------------------------------------
-K čemu slouží DNS server?
DNS - DOMAIN NAME SERVICE - domenova sluzba pro mapovani ip adres na jmene nazvy a obracene
			  - ma stromovou strukturu
			  - cte se z prava doleva
			  - vyuziva rekurzivni vyhledavani 

-S jakými protokoly DNS server pracuje?
TCP UDP 53

-Propojení DNS serverů, nadřazené DNS servery- zóna a typ DNS záznamu
3 typy serveru - autoritativni, korenove a cashovaci, kazdy server se stara o urcitou cast stromu
korenove jsou nadrazenejsi k autoritativnim protoze protoze debile
2zony - dopredna - mapuje jmenne nazvy na ip adresy - SOA, A , AAAA, CNAME , MX , NS
      - zpetna - mapuje ip adresy na jmenne nazvy - SOA , PTR , CNAME

- Typy záznamů v DNS serveru
A - mapuje - pro ipv4
AAAA - mapuje pro ipv6
CNAME - alias - jiny nazev 
NS - naming server - udava dns servery dane domeny
MX - ridi tok elektronicke posty 
PTR mapuje - nejvysssi domeny - ipv4 - in-addr.arpa, ipv6 - ip6.arpa
SOA start of authority - oznacuje zacatek zony - obsahuje: serial number
							   retry
							   refersh
							   expire
							   ttl

-autoritativní servery, rekurzivní vyhledávání, cachovací DNS Server
 autoritativni servery - staraji se o urcitou cast dns stromu
 cashovaci servery - vyhledava zda jiz tuto stranku nema v zaznamu, optimalizuje vykon, pozadavky ukladaji do cache
 korenove servery - obluhuji korenovou domenou oznacenou teckou, maji zaznamy o domenach prvniho stupne - top level
			domain, korenovych serveru je 13 aby se i s dotazem vesly do jednoho udp paketu (irl jich 
			je vic), dotaz je smerovan pomoci anycastu na ostatni servery - optimalizace vykonu
-------------------------------------------------------------------------------------------------------------------
DHCP WINDOWS
-------------------------------------------------------------------------------------------------------------------
-Co je DHCP server, k čemu slouží?
DHCP je rozsireni puvodniho bootp protokolu
ctyrfazovy proces pro pridani ip adresy pro klienta 


-Co je obor adres? Definujte!
Obor adres je skupina ktera lze nastavit a stara se o site v urcite podsiti 
Range - rozsah adres 

-Jak probíhá přidělení IP adresy, popište průběh komunikace
ctyrfazovy proces 
1.klient posle DHCP DISCOVER pomoci broadcastu aby zjistil zda se v okoli nenachazi nejaky server
2. V pripade ze se server najde, server odpovi DHCP OFFER, obsahuje mac adresu klienta, ip adresu, masku klienta
a cas zapujceni 
3. klient v pripade zajmu odpovi DHCPREGUESTEM, pomoci broadcastu a v pripade ze se serveru ozve vice, klient
si vybere vzdy prvni server
4.server nazpatek posila DHCPACK s dobou zapujceni a ostatnima konfiguracnima parametrama

DHCP RELEASE - KLIENT informuje ze adresu nepotrebuje
DHCPNACK - server zamitne pozadavek klienta (kdyz klient zada adresu z jineho subnetu nebo vyprsela doba zapujcky apod.)
DHCP DECLINE - klient informuje server ze adresa je jiz pridelena jinemu pc
DHCP INFORM - klient informuje server ze adresu jiz ma, ale potrebuje ostatni konfiguracni parametry

-K čemu a kdy se používají rezervace?
v pripade ze chci pridelit ip adresu na urcity pc mohu udelat rezervaci, pro tuto konfiguraci musim znat mac adresu pc
klienta

-K čemu a kdy se používají výjimky?
pokud zarizeni potrebuje statickou ip adresu na zacatku se vytvori vyjimka roszahu ip adres kterou nebude DHCP vyuzivat
pro klinenty

-Co je doba zapůjčení?
Doba zapujceni je doba do kdy je ip adresa pridelena zarizeni, v polovine zapujcky klient zazada server o prodlouzeni a 
ihned serveru posila DHCP REQUEST (pouze dve faze)

- množina oborů - K čemu slouží
mnozina oboru seskupuje obory adres do jednoho objektu ktery spravuje vice adres z vice podsiti

-------------------------------------------------------------------------------------------------------------------
EXCHANGE SERVER
-------------------------------------------------------------------------------------------------------------------
-popište funkce, instalaci a konfiguraci Exchange Serveru 2013
pozadavky k instalaci: AD, IIS, DHCP,DNS
Exchange server slouzi pro spravu sdilenych slozek, elektronicke posty, ukoly a kalendare - groupwarove sluzby

ÏMAP4 - internet messsage acces protocol - je to sluzba pro prijmani emailu klientovi, pracuje na portech 143 (nezabezpeceny)
, 993 (zabezpeceny tls) - lepsi jak pop3 - stahuje pouze zahlavi a zbytek se stahne po otevreni emailu

POP3 - post office protocol - sluzba opet pro prijem elektonicke posty - porty: 110 nezabezpeceny, 995 tls, je horsi
jak imap protoze je narocnejsi na uloziste, stahuje ihned celou zpravu 

SMTP - system mail transport protocol - protokol pro prenos elektronicke posty 
odesilatel posle zpravu na svuj smtp server a ten posle pomoci smtp relay zpravu na smtp server prijemce, ten tepr posila
zpravu prijemci

repicients - mailove adresy a uzivatele
		- mailboxes - nastavovani mailovych stranek











