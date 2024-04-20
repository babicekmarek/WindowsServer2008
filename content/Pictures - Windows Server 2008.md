Úvodní okno Initial Configuration Task se spouští automaticky nebo příkazem OOBE přes tlačítko START

![[Pasted image 20240420110115.png]]

Zjištění dynamické adresy serveru:

START -> Command Propmpt-> IPCONFIG -> zjistí se IP serveru 192.168.153.130  (IPv4 Address) v okně Initial Configuration Task -> Configure Networking ->

![[Pasted image 20240420110131.png]]

Odškrtnout IPv6 -> pak IPv4 -> Properties -> doplní se IP serveru a maska

![[Pasted image 20240420110144.png]]

Z dynamické adresy serveru se tak stane statická -> OK -> Close -> Close -> x -> Enable automatic update and feedback -> Enable Remote Desktop -> 2. volba - Allow… -> OK

![[Pasted image 20240420110155.png]]

-> Apply -> OK

Vypnutí firewallu: -> Configure Windows Firewall ->

![[Pasted image 20240420110242.png]]

Turn Windows Firewall on or off -> Turn off (2x) -> OK -> x

![[Pasted image 20240420110254.png]]

Provide computer name and domain -> Change -> změní se Computer name

![[Pasted image 20240420110308.png]]

OK -> OK -> Close -> Restart now -> Hardware Maintenance (Planned) -> OK

Přihlásit se jako Administrator – heslo Abc1234 (bude-li vyžadována změna hesla, změnit na Abc12345)

Spustí se Server Manager – ikona vedle tlačítka Start

![[Pasted image 20240420110320.png]]

->Roles -> Add Roles -> Next -> 2.volba vpravo Active Directory Domain Services

![[Pasted image 20240420110336.png]]

->Add Required Features -> Next -> Next -> Install -> Close

![[Pasted image 20240420110349.png]]

Start -> DCPROMO -> Next ->  zaškrtnout Automatically correct… -> Next -> Create a new domain… -> Next ->

libovolné jméno - “cokoliv.cz” -> Next -> POZOR Forest function level -> Windows Server 2008 R2  -> Next ->

Next -> YES -> Next -> password stejné jako pro administrátora (8 znaků Abc12345 místo Abc1234, pokud nebylo změněno) -> Next -> Next  -> zaškrtnout Reboot on completion….. po restartu se přihlásit jako administrator.

Spustí se Server Manager – ikona vedle tlačítka Start -> Roles -> Add Roles -> Next ->

DHCP server -> Next -> Next

![[Pasted image 20240420110404.png]]

Next -> do okna “Preffered DNS server IPv4 address“ se uvede místo 127.0.0.1 IP adresa serveru -> Validate

![[Pasted image 20240420110420.png]]

Next -> Next -> Add -> v okně Add Scope se definuje rozsah IP adres přidělovaných klientům

![[Pasted image 20240420110434.png]]

OK ->

![[Pasted image 20240420110445.png]]

Next -> Next -> Next -> Next -> Install -> Close

V  Server Manageru bude v položce ROLES tento stav:

![[Pasted image 20240420110500.png]]

Restart -> po přihlášení vypnout firewall

![[Pasted image 20240420110511.png]]

V konfiguraci sítě pro IPv4 nastavit DNS server – opíše se IP adresa serveru místo 127.0.0.1

![[Pasted image 20240420110523.png]]

OK -> Close –> Close -> RESTART

Server manager -> Roles -> Add Roles -> Next -> File Services, Print and Document Services, Remote Desktop Services -> Next -> Next -> x Remote Desktop Session Host -> Install Remote Desktop Dervices Host anyway … -> Remote Desktop Licensing -> Next -> Next -> Don’t require network level authentication -> Next -> Configure later ->         Next -> Next -> Next -> Next -> Next -> …Print server beze změny… -> Next -> Next -> … File server beze změny…         -> Next -> Install -> Close -> RESTART -> … po něm se dokončí instalace

![[Pasted image 20240420110537.png]]

Close

V Server Manageru v položce ROLES by měl být následující stav:

![[Pasted image 20240420110557.png]]

Rozdělení domény na více částí (organizačních jednotek) a definice uživatelů v jednotkách :

Start -> Administrative Tools -> Active Directory Users and Computers -> … klik na název domény, pravé tlačítko -> New Organizational Unit -> … zadá se část organizace, může se jich zadat i více -> OK

![[Pasted image 20240420110623.png]]

Pravé tlačítko na organizační jednotku -> New -> User

![[Pasted image 20240420110634.png]]

Next -> … pozor na checkboxy

![[Pasted image 20240420110645.png]]

Next -> FINISH  Podobně se přidají další uživatelé ….viz. výše…. :

![[Pasted image 20240420110657.png]]

Definice sdíleného prostoru na disku serveru pro klienty v doméně:

Průzkumník -> Computer -> C: -> New Folder -> (např. ZZZ) -> … pravé tlač. … -> Properies -> Sharing -> Share… -> 

v seznamu vlevo vybrat EVERYONE -> změnit READ na READ/WRITE -> vybrat v seznamu vlevo FIND PEOPLE… -> napsat část přihlašovacího jména nebo celé -> CHECK NAMES -> OK -> změnit READ na READ/WRITE (opakovat FIND PEOPLE… atd. tolikrát, kolik je uživatelů) -> CLOSE

Z karty Properties -> Sharing zkopírovat do schránky položku Network Path:

![[Pasted image 20240420110711.png]]

Start -> Administrative Tools -> Group Policy Management

![[Pasted image 20240420110723.png]]

Pravé tlačítko na název domény -> Create a GPO in this domain ... -> do okna NEW GPO se napíše název nové politiky -> OK -> na pravém panelu se objeví nová politika -> pravým tlačítkem -> EDIT -> objeví se nové okno a v levém panelu po rozbalení ve Folder Redirection se nastaví přesměrování uživatelských složek (např. Desktop a Documents) na server přes pravé tlačítko a Properties:

![[Pasted image 20240420110742.png]]

![[Pasted image 20240420110749.png]]

Do Root Path se vloží cesta ke sdílené složky ze schránky  viz. výše.

Vyplní se záložka Settings:

![[Pasted image 20240420110810.png]]

Apply -> OK Předchozí postup se zopakuje pro všechny složky určené k přesměrování (Desktop, Documents).

RESTART -> přihlásit se jako administrator, spustí se VMWARE a spustí se Windows7.

PC s Windows 7:

Po 1. spuštění by měla proběhnout komunikace s nastavením místní sítě

![[Pasted image 20240420110821.png]]

Home Network -> x Documents

![[Pasted image 20240420110836.png]]

Next

![[Pasted image 20240420110845.png]]

Next …. Proklikat, heslo neopisovat

V Ovládacích panelech:
- V nastavení sítě vypnout IPv6 a v IPv4 nastavit v DNS IP adresu serveru.
- Vypnout Firewall.

- System -> Change settings -> karta Computer Name -> Change -> změnit Computer Name a místo      WORKGROUP zvolit DOMAIN – zapsat svou doménu -> uzavřít všechna okna -> RESTART -> SWITCH USER -> přihlásit se jako uživatel domény.

- IP adresa by měla být dána DHCP serverem – ZKONTROLOVAT v nastavení sítě PC a v SERVER MANAGERU na serveru. Měl by fungovat příkaz PING ze serveru na PC a naopak. V případě, že nefunguje, je nutno zkontrolovat vypnutí firewallu na obou stranách.

- Na serveru v nasdílené složce by se měly objevit složky uživatelů s podsložkami DESKTOP a DOCUMENTS. Pokud se vytvoří soubory na ploše nebo ve složce Documents na PC s Windows7, měly by se objevit na serveru ve sdílené složce uživatelů. Nejjednodušší způsob je přes pravé tlačítko v každé složce NEW -> TEXT DOCUMENT. Pokud ne, je nutné na PC provést START -> GPUPDATE, případně restart serveru a kontrolu v GPO na serveru.

Mapování síťové jednotky:

- Computer -> Computer -> pravé tlačítko Map network drive … -> Drive – vybere se písmeno -> Folder - Browse … -> vybere se sdílená složka na serveru -> OK nechá se RECONNECT AT LOGON -> FINISH

Server - přístup na vzdálenou plochu:

- Control panel -> System ->  Remote Settings ->  karta REMOTE ->  nechat Allow connections from computers ->  Select users ->  Add ->  vyberou se uživatelé s volbou CHECK NAMES včetně administrátora ->  OK  -> Apply ->  OK Control Panel ->  System and Security ->  Firewall ->  Allow a program or feature through Window Firewall ->  zaškrtnou se volby Remote administration a další – vše, co začíná REMOTE (celkem 8) a navíc Routing Remote Access, Windows Firewall Remote Management a Windows Remote Management – vždy se označí všechny 4 checkboxy:

![[Pasted image 20240420111038.png]]

![[Pasted image 20240420111045.png]]

OK

PC s WINDOWS 7 - přihlásit se jako administrátor PC tj. PCname\USER

Start -> Computer -> Properties -> Remote settings -> karta Remote -> Allow connections … -> Select Users -> Add -> administrátor domény -> Check Names -> nutno zadat domain_name\administrator  -> OK -> Apply  -> OK.

FIREWALL  -> zkontrolova vypnutí -> Allow a program or feature …  -> Change Settings -> 7x Remote… + Routing and Remote Access + Windows Firewall Remote Management a Windows Remote Management – vždy se označí všechny 4 checkboxy -> OK

FIREWALL -> Advanced Settings -> Windows Firewall Properties ->

karta Domain Profile -> Protected Network Connection - Customize -> Local Area Connection - odškrtnout -> OK

karta Private Profile -> Protected Network Connection - Customize -> Local Area Connection - odškrtnout -> OK

karta Public Profile -> Protected Network Connection - Customize -> Local Area Connection - odškrtnout -> OK -> OK

Vzdálený přístup ze SERVERu na PC

Start -> remote -> Remote Desktop Connection -> vloží se IP PC Windows 7 -> Connect – na varovné hlášení odpovědět YES… na další dotaz YES

Z PC na SERVER stejným způsobem

Restrikce hesel : GPO – Default Domain Policy resp. Politika1 resp. politika organizační jednotky

Expedice, pokud existuje - pravé tlač. EDIT

![[Pasted image 20240420111111.png]]

Chceme-li zmírnit pravidlo pro nastavování hesel zvolí se DISABLED pro “Password must meet complexity…” a upraví se “Minimum password length” na menší hodnotu. V opačném případě se parametr

COMPLEXITY nechá na ENABLED a miinimální délka hesla se zvětší.

![[Pasted image 20240420111139.png]]

Vynucení změny politiky - CMD – GPUPDATE /FORCE