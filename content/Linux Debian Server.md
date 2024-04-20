# Instalace
- Graphic Install -> lokalita: czechia -> vše ostatní americký
- Hostname podle zddání, do první tečky je hostname
- Heslo a uživatel ze zadání
- Partition -> manual -> dvojklik na disk -> free space -> create new partition -> dám 7 GB a na začátek(beginning) -> pokud jsou nastavený parametry v zadání = mount options -> done setting up partition
- nastavím takhle všechno podle zadání
- Druhá partition -> změním na swap, pak finish partitioning
- Další média neskenuju
- Network mirror -> yes -> czechia -> merlin fit (nebo fyzicky nejbližší)
- http proxy nedávám
- Popularity contest -> no
- Žádný desktop environment neinstaluju, viz obrázek:

- ![[Pasted image 20240420083426.png]]

- Grub boot loader -> yes -> /dev/sda
- Na serveru dělám vše jako ROOT

---
# MidnightCommnder
- Instalace:
```bash
cd /etc/apt/
```
- Pokud při instalaci přes apt bude požadovat CD nebo instalační médium: 
```bash
cd /etc/apt
nano sources.list
```
- Zakomentářuju (#hashtagem) první řádek viz obrázek (cd rom)

- ![[Pasted image 20240420084314.png]]

- V midnighCommander si přes options (F9 o menu, a pak vyberu options, pak se řídím podle menu dole), options -> panel options, zapnu si Lynx-like motion

- ![[Pasted image 20240420084452.png]]

--- 

# SSH
- Zjistit IP pomocí: 
```bash
hostname -l
```
### Server
- Instalace: 
```bash
apt install openssh-server
```
- Konfigurace: 
```bash
/etc/ssh
> ssh.config - klient
> shhd.config - server(démon)
```
- Listen adres: 1 povolená adresa, můžu to napsat vícekrát - zatím nefunguje
- Zakázat roota:
	- Najdu si v `/etc/ssh/sshd.config` > `PermitRootLogin`
	- Můžu dát `yes/prohibit-password/no` > já  dám no
	- Pokud se chci přihlásit přes ssh jako root > přihlásím se jako uživatel su
- Přihlásit se může pouze určitá skupina
	- Allow Groups (název skupiny) - není v texťáku

### Klient
- Stáhnout putty, zjistím si adresu vmwaru, připojím se přes putty
- Vytvořit uživatele/skupiny: 
	- `adduser [login]`
- Listen adress - server bude poslouchat pouze na určené adrese
```bash
/etc/hosts.deny > sshd: ALL – nikdo se nesmí připojit k ssh
/etc/hosts.allow > sshd: 192.168.11.0/24 – tahle síť se smí připojit
```

--- 

# DNS
- Nainstaluju 
```bash
apt install net-tools (ifconfig)
apt install dnsmasq
```

Všechny IP adresy dávám do `/etc/hosts`
Adresu zjistím přes: `hostname -l`

- ![[Pasted image 20240420090304.png]] 

- Ze zadání doména a adresa, píšu takhle:
	- Musím uložit, jinak nefunguje
```bash
systemctl restart dnsmasq
systemctl status dnsmasq
```

- Na klientovi nastavení -> možnosti adaptéru -> nastavím DNS

---

# DHCP
- taky dnsmasq
`/etc/dnsmasq.conf`, tam si najdu dhcp-range
- Zadávám:
`dhcp-range= začátek adres, konec ares, délka trvání`
- ![[Pasted image 20240420102606.png]]
- Definované adresy:
`dhcp-host= mac adresa, ip`
- ![[Pasted image 20240420102713.png]]

---

# Statická IP
`/etc/network/interfaces`
- ![[Pasted image 20240420102810.png]]

---

#  Časový server
`apt install ntp`
- Komunikace pouze s interní sítí: router je nastavený tak, že nepustí nic dovnitř (automaticky) 
- (Kdyby se někdo ptal) - specifikovat server -> `/etc/ntpsec/ntp.conf` -> server *názevDomény*
- ![[Pasted image 20240420103126.png]]
- Nastavím ntp i na windows

- WWW server
- Instalace -> `apt install apache2`
- `/etc/apache2` - dělí se na available a enabled
- Available znamená nainstalovaný, enabled je i aktivovaný

- `systemctl status apache2` - kontrola, že běží
- Pokud nefunguje - ip tables z prezentace
- Nainstaluju php, příkaz z prezentace
- V praktické budeme muset i otestovat php

- VirtualHost patri do `/etc/apache2/sitesEnabled` podle prezentace